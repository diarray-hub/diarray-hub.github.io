---
layout: post
title: "So what? Notes from Deep Learning Indaba 2026"
author: Yacouba Diarra
categories: events
tags: africa ai community deep-learning-indaba research reflections
---

This was my third Deep Learning Indaba and, without a doubt, my best one in terms of connections and learning.

This post is arriving a month late. Between one badly needed week off, rebuilding my entire workspace, and catching up with activities at the lab, time simply disappeared. I already feel like I need another week off—this time to read the book I won there :)

Part of that came from the Baobab app, which I found wonderful. Part of it was simply that the whole experience felt clearer and more organized. But what stayed with me most was not a tutorial, a workshop, or even a research talk. It was a two-word question:

> So what?

![Deep Learning Indaba 2026]({{ '/assets/dli2026/dli2026.jpg' | relative_url }})

## The most expensive free advice I received

My mentorship session with Girmaw marked me in ways I did not expect. I found guidance, goodwill, and priceless advice, but the best advice was that question: **so what?**

It pushed me to reflect on the impact of my work in my community. I realized that I had become so obsessed with the idea of becoming a great scientist that I was focusing on metrics that do not really mean anything to me—or to Africa.

Suppose I succeed on that path. I publish the papers, collect the citations, and become very good at moving numbers on benchmarks.

So what?

What do I want to see when I look back at the impact of my life's work?

I am still reflecting on that one.

## Research in Africa is moving

During the Research in Africa days, I felt a shift in the African AI community's attention. For a long time, so much of the visible work seemed to revolve around collecting data and adapting foreign tools, with an almost total focus on language. Language matters—a lot—but Africa does not have only one problem.

In Lagos, I saw researchers building smaller neural models, designing new architectures, adapting systems for edge inference, and moving into other domains. Agriculture. Health. Logistics. Fraud. There are so many sectors where AI could be a game changer in Africa.

Before this Indaba, I had this painful feeling that pretty much everyone in African AI was working on the same problem: language. I left thrilled by how many different research directions were being explored.

I was also part of those Research in Africa days as a presenter. Our paper, *[Listen, Attend, Understand: a Regularization Technique for Stable E2E Speech Translation Training on High Variance Labels](https://arxiv.org/abs/2601.01121)*, was accepted into the DLI research track, and I presented it both orally and as a poster. The poster even won a prize: a copy of *Probability and Computing: Randomization and Probabilistic Techniques in Algorithms and Data Analysis*. Exactly my kind of prize, and a book I am eager to devour.

![Presenting at Deep Learning Indaba 2026]({{ '/assets/dli2026/poster-presentation.jpg' | relative_url }})

## Making the black boxes a little less dark

I used the tutorials this year to get in touch with some of my personal AI "black boxes." I did not expect to walk out as an expert. Going from level zero to one was enough.

The session on building faster transformers with Triton gave me a first look at GPU kernel programming and helped satisfy some of my curiosity about how accelerators actually work. The core difference I took away was the programming paradigm: with CUDA, you work at the scalar or thread level and manually manage how many individual threads cooperate inside a block. Triton lets you write programs that operate on blocks of data while the compiler handles much of the thread coordination and memory optimization.

There are still many things I did not quite grasp. Honestly, the more time passes while I write this, the more obscure spots appear. But, I guess the box is less dark now :)

The graph neural networks tutorial did something similar. It introduced the basic ideas, how GNNs differ from the models I know better, and how they are trained. Again: zero to one.

## Updating my mental image of AI safety

I joined the workshop on red-teaming AI systems because I needed to correct a caricature I had built in my head.

I knew AI safety existed and understood that it was important, but I imagined two kinds of people in the field:

1. Researchers doing actual scientific work and developing alignment methods such as RLHF.
2. The AI-pocalypse guys calling for an AI break every time a new LLM gets released.

The second group is significantly louder. If you care more about the scientific side, it is easy to fall into the false belief that AI safety is mostly crying wolf. I had fallen into that trap.

The hands-on red-teaming workshop grounded my mental image in the actual work people are doing to make AI systems safer. I already liked red-teaming as a concept from cybersecurity; I loved seeing it applied to AI, and I learned a lot.

Another workshop that caught my attention was GeoAI for climate resilience. GeoAI had been picking my interest since InstaDeep's 2025 hackathon on foundation models for Earth observation. One thing that struck me then was how few datasets are easy to find for geospatial AI tasks compared with language.

That is why I liked GeoAI Africa's effort to do for geospatial data something similar to what Lanfrica has done for language: make the data easier to find. Discovery sounds like a small problem until you try to build something. Making data findable is one of the first steps that drives innovation.

## Don't stop until we make it

"Don't stop until you're proud," Dr. Bayo of Data Science Nigeria told us. I want to extend that message to the whole Indaba community.

It is harder in Africa. Pretty much everything in AI is harder here because we have not even solved the infrastructure and energy problems. Let us not even start on funding. This community started with zero, and yet every day you are doing it. Considering the resources we have, you guys are doing miracles.

Sometimes it is awfully painful to see that even those miracles are not enough to convince funders—or our own governments. But I have faith in this community. The future depends on us refusing to give up, refusing the brain drain, and facing the challenges.

So please: **don't stop until we make it.**

![A group photo from Deep Learning Indaba 2026]({{ '/assets/dli2026/dli_team_picture.jpg' | relative_url }})

My first contact with the Indaba was at IndabaX Mali in 2023, where I co-organized a workshop. In 2024 and 2025, I was part of the IndabaX Mali organizing committee and attended the annual Indaba as an IndabaX poster presenter.

Remember the location: Mali. When I say we have it the hard way, trust that I know what I am talking about.

I am deeply grateful to the Indaba for the learning, the support, and the discoveries. That is also why I am particularly proud that I was able to bring two students with me this year, through RobotsMali AI4D Lab and support from the Indaba.

I almost dragged them there and said, "You'll thank me later."

They did thank me afterwards.

I want more people from my country to witness what I have witnessed, so the flowers of a brighter future can bloom in Mali.
