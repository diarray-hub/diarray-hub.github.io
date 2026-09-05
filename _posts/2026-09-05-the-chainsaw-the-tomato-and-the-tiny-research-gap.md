---
layout: post
title: "The chainsaw, the tomato, and the tiny research gap"
author: Yacouba Diarra
categories: technical
tags: machine-learning speech-recognition system-design research occams-razor
---

I have recently realized that one concept drives almost everything I enjoy doing in science: **elegance**.

This is funny because I am not really an appearances person. I do not spend much time trying to look elegant myself. But give me a machine-learning problem and suddenly I become extremely concerned with whether the solution feels natural, coherent, and minimally forced.

The question I now like to ask is:

> What is the smallest scientifically sound change I can make to the system so it understands the problem better?

Not the smallest model at any cost. Not the fewest lines of code. And definitely not "tiny" as a marketing adjective attached to a model that still needs a small power plant. I mean the smallest *idea* that expresses the missing structure of the problem.

Two recent projects made this preference obvious to me. The first is [Listen, Attend, Understand](https://arxiv.org/abs/2601.01121) (LAU), where we added a training-only semantic constraint to an end-to-end speech-translation model. The second is my [Parakeet SC-LID system](https://github.com/diarray-hub/parakeet-sc-lid) for the [Google WAXAL ASR Challenge](https://zindi.world/competitions/google-waxal-asr-challenge), where I added a small language-identification loop to a multilingual recognizer.

Both changes are tiny. That is the point.

## Occam's Razor, with an engineering clause

[Occam's Razor](https://plato.stanford.edu/entries/simplicity/) is usually summarized as a preference for the simpler explanation when competing explanations account for the evidence equally well. The "equally well" part matters. Simplicity is not permission to ignore half the problem and celebrate the clean code afterward.

For system design, my version is something like this:

> Do not multiply machinery beyond what the problem requires.

This is a heuristic, not a law of physics. A large pretrained model can be the simplest practical solution when it already contains what the task needs. A more elaborate architecture can also be justified when each component has a clear job. What I dislike is complexity used as a substitute for thinking about the structure of the problem.

If the failure is semantic drift, add a semantic constraint. If the recognizer is confused because it does not know which language it hears, let it model language identity. Do not immediately attach a general-purpose reasoning engine, three retrieval pipelines, and a prayer.

## Example one: giving speech translation a semantic pull

End-to-end speech translation maps speech in one language directly to text in another. In our case, the input is Bambara speech and the output is French text. That direct path avoids compounding errors across a low-resource ASR system and a low-resource machine-translation system, but it is difficult to train when the translations themselves have high variance (or annotation noise).

Two people can translate the same sentence correctly using very different French words. A sequence loss does not naturally understand that these alternatives can carry similar meaning: it mostly sees different target tokens. With only about 30 hours of non-professionally translated speech, the model does not have endless examples from which to average out that ambiguity.

LAU adds one shallow, training-only branch to the existing encoder-decoder architecture.

![Listen, Attend, Understand training and inference architecture]({{ '/assets/figures/lau-architecture.svg' | relative_url }})

*LAU architecture, redrawn from Figure 1 of the [paper](https://arxiv.org/abs/2601.01121). The amber semantic branch exists only during training. [Open the figure full-size]({{ '/assets/figures/lau-architecture.svg' | relative_url }}).*

The normal path remains intact:

1. A [FastConformer](https://arxiv.org/abs/2305.05084) encoder converts the speech into acoustic representations.
2. The hybrid TDT/CTC decoders learn to produce the French translation. TDT jointly predicts tokens and durations; its original formulation is described by [Xu et al.](https://arxiv.org/abs/2304.06795).
3. Their sequence losses train the primary speech-translation task.

The added path asks the encoder to preserve meaning:

1. The reference French translation goes through a frozen SentenceTransformer built on CamemBERT, producing a target semantic embedding.
2. The speech encoder's output goes through a shallow semantic head with two fully connected layers.
3. A cosine or mean-squared-error loss aligns that prediction with the frozen reference embedding.

The combined objective is simply:

`L_LAU = L_sequence + λ L_semantic`

The text-embedding model stays frozen. Gradients from the semantic loss update only the shallow head and the acoustic encoder, pulling the encoder toward a space where two lexically different but semantically related translations are less alien to each other.

Then comes my favorite part: **the semantic head is removed at inference**. Deployment uses the same encoder and decoder graph as the baseline. The regularizer changes how the model learns without adding inference cost.

The [LAU experiments](https://arxiv.org/abs/2601.01121) do not establish a universal solution to speech translation. They use one small Bambara-French corpus and a constrained compute budget and propose one targeted and simple fix to a real low-resource problem.

That is a modest contribution. A tiny research gap, even.

![A research gap meeting an older paper]({{ '/assets/memes/gap_literrature2.jpg' | relative_url }})

Every time I think I have a novel idea, a 30-year-old paper emerges from the darkness to humble me. When the gap survives the literature review, it usually looks approximately this big.

## Example two: let a multilingual recognizer identify its own language

When I read the [WAXAL challenge](https://zindi.world/competitions/google-waxal-asr-challenge/) description on zindi, my first thought was: *I am going to add a small language-classification head to Parakeet and train the smallest model I can.* So I did.

The challenge asks one ASR system to transcribe Lingala, Luganda, and Shona (three related Bantu languages). Language identity is useful context: even with one shared tokenizer and decoder, it changes which character and word sequences are plausible. But requiring the caller to supply a language label makes the system less autonomous and assumes the metadata is always correct.

The alternative I used is self-conditioning. Start with a 114.6M-parameter, 17-layer FastConformer model with hybrid RNN-T and CTC decoders, implemented in [NVIDIA NeMo](https://arxiv.org/abs/1909.09577). Then add two small linear layers.

![Self-conditioned language identification architecture]({{ '/assets/figures/sc-lid-architecture.svg' | relative_url }})

*The SC-LID path predicts a soft language distribution and feeds it back into every acoustic frame before decoding. [Open the figure full-size]({{ '/assets/figures/sc-lid-architecture.svg' | relative_url }}).*

Here is the complete loop:

1. The encoder produces frame-level features `H` with 512 channels.
2. Masked mean pooling collapses time while ignoring padded frames, giving one 512-dimensional summary per utterance.
3. A linear LID head maps `512 → 3`, producing logits for `lin`, `lug`, and `sna`.
4. Softmax converts those logits into a probability distribution rather than a hard language decision.
5. A second linear layer projects `3 → 512`.
6. That projected language vector is broadcast across time and added to every encoder frame before the RNN-T and CTC decoders see it.

For the best recorded run, the training objective in the configuration was:

`L_total = L_RNNT + 0.3 L_CTC + 0.2 L_LID`

This arrangement creates two useful gradient paths. The supervised cross-entropy loss teaches the head to identify the language, while the ASR losses can also shape the *soft* language signal according to what helps transcription. At inference, the model predicts that signal from the audio itself. The caller does not need to choose a language first.

Of course, I was not the first human to think of conditioning multilingual ASR on language identity. [Kashiwagi et al.](https://arxiv.org/abs/2406.12611) introduced a related encoder-prompting method within self-conditioned CTC and reported strong multilingual results. I was a little pissed when I found it—not because the work should not exist, but because there would be no paper coming out of my shitty competition idea :)

Still, independently converging toward an established idea felt important. It showed me that I am building research intuition: I saw the task, identified the missing variable, and arrived at a logically sound architectural change before searching for someone else's answer. The implementation may also be the first public version of this particular whole-utterance SC-LID pattern inside NeMo's hybrid Parakeet stack. I say *may* because absence-of-code searches are not proof, and somewhere on this planet a repository with four stars is always waiting to ruin your novelty claim.

## The results need a very large asterisk

My [best run](https://github.com/diarray-hub/parakeet-sc-lid) reached about **25.6% WER** and **100% LID accuracy** on my constructed public evaluation set, which combined the public competition test set with other public data. Those numbers are not results on Zindi's private test set, and 100% on that split is not evidence of universal language-identification perfection.

The reality check was a Lingala-speaking friend listening to five private, self-recorded utterances. Roughly 40% of those utterances contained at least one insertion, omission, or substitution. That is an utterance-level error incidence, **not** a properly computed 40% WER. It is at least in the same uncomfortable neighborhood as my final leaderboard score of **44.32% WER**.

I also have reservations about the WAXAL utterance alignment and, after the reported [Phase 2 test-set issue](https://zindi.world/competitions/google-waxal-asr-challenge/discussions/34268), about treating the private score as unquestionable ground truth.

Most importantly, I did not run the ablations needed for a scientific claim that SC-LID is better than naive multilingual training. I spent roughly **$50** on three rented A100 runs and then stopped. There is no baseline without LID, no controlled comparison with structured multilingual prompting, and experiment three changed class weighting alongside scheduler, learning-rate, and batch-size choices.

This is not "the best method." It is a small, underfunded experiment built around a good intuition, with enough evidence to say the intuition deserved a proper test—and not enough evidence to pretend the test was definitive.

## Why I call these systems elegant

LAU and SC-LID solve different problems, but they share a design pattern:

- **Name the missing information.** LAU is missing semantic stability; WAXAL ASR is missing language context.
- **Attach the constraint where it belongs.** Both additions act on the encoder representation, before the limited output vocabulary has thrown information away.
- **Reuse supervision already present.** LAU uses the reference translation; SC-LID uses the language label in each manifest.
- **Prefer an auxiliary objective to a second full system.** A small head can reshape a large shared encoder during training.
- **Keep deployment honest.** LAU deletes its training branch entirely. SC-LID retains only two tiny linear projections and does its own language selection.
- **Make the claim proportional to the experiment.** A clever architecture does not compensate for missing baselines, unreliable labels, or five-sample human evaluation.

The starter approach for the competition fine-tuned Gemma-3n-E2B-it, and large multimodal or language-model-based systems can absolutely work. With noisy data, their capacity may model the distribution better and win the leaderboard. I respect that.

I just do not find a multi-billion-parameter solution to a three-language ASR problem with barely 300 hours of speech especially elegant. To me, it feels like cutting tomatoes with a saw.

You technically *can* cut tomatoes with even a chainsaw. You may even finish first. I would still like to know whether a knife was enough.

## My current elegance test

When I face a new ML problem, these are the questions I want to ask before adding more machinery:

1. What precise information or constraint is the current model missing?
2. Can I express it as supervision, conditioning, or regularization instead of another full pipeline?
3. Where in the representation should that signal act?
4. Can the extra component disappear—or become negligible—at inference?
5. What is the smallest ablation that could prove the idea is doing real work?
6. Am I choosing simplicity because it fits the problem, or because I cannot afford the experiment that would challenge it?

That final question is important. Compute constraints can produce elegant thinking, but they can also produce elegant excuses. I have made both.

Elegance is not minimalism for its own sake. It is the discipline of making every added component earn its place. Sometimes that produces a publishable regularizer. Sometimes it produces a $50 competition experiment and a public repository that might help some person, somewhere.

And sometimes the literature gap is just your lack of understanding of the literature.

That is fine too. Read the 30-year-old paper, put down the chainsaw, and keep building!

## References and implementations

- Yacouba Diarra and Michael Leventhal, [*Listen, Attend, Understand: a Regularization Technique for Stable E2E Speech Translation Training on High Variance Labels*](https://arxiv.org/abs/2601.01121), 2026.
- Yosuke Kashiwagi et al., [*Rapid Language Adaptation for Multilingual E2E Speech Recognition Using Encoder Prompting*](https://arxiv.org/abs/2406.12611), Interspeech 2024.
- Dima Rekesh et al., [*Fast Conformer with Linearly Scalable Attention for Efficient Speech Recognition*](https://arxiv.org/abs/2305.05084), 2023.
- Hainan Xu et al., [*Efficient Sequence Transduction by Jointly Predicting Tokens and Durations*](https://arxiv.org/abs/2304.06795), 2023.
- [Parakeet SC-LID source, configuration, model card, and evaluation caveats](https://github.com/diarray-hub/parakeet-sc-lid).
