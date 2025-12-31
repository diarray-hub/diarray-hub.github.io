<style>
  /* Profile Picture */
  .profile-container {
    text-align: center;
    margin-bottom: 2rem;
  }
  .profile-pic {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    object-fit: cover;
    border: 2px solid #eee;
  }

  /* Timeline Container */
  .timeline {
    position: relative;
    max-width: 800px;
    margin: 2rem 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
  }

  /* The vertical line */
  .timeline::before {
    content: '';
    position: absolute;
    left: 105px; /* Adjust based on year width */
    top: 0;
    bottom: 0;
    width: 2px;
    background: #e1e4e8;
  }

  .timeline-item {
    position: relative;
    margin-bottom: 40px;
    display: flex;
    align-items: flex-start;
  }

  /* Year Label */
  .timeline-year {
    width: 90px;
    text-align: right;
    font-size: 0.9rem;
    color: #6a737d;
    padding-top: 4px;
    flex-shrink: 0;
  }

  /* The Dot */
  .timeline-dot {
    width: 12px;
    height: 12px;
    background-color: #e1e4e8;
    border: 2px solid #fff;
    border-radius: 50%;
    position: absolute;
    left: 100px; /* Aligned with vertical line */
    top: 8px;
    z-index: 1;
  }

  /* Content Area */
  .timeline-content {
    margin-left: 40px;
    display: flex;
    align-items: flex-start;
  }

  .timeline-logo {
    width: 100px;
    height: 100px;
    margin-right: 15px;
    flex-shrink: 0;
  }

  .timeline-logo img {
    width: 100%;
    border-radius: 4px;
  }

  .timeline-text {
    font-size: 1rem;
    line-height: 1.5;
  }
</style>

<div class="profile-container">
  <img src="./assets/blue_bird.png" alt="blue_bird" class="profile-pic">
</div>

Hi, I'm Yacouba Diarra (**diarray** on the internet) and I care about stuffs like having a [blog]() to post about, well... [stuffs](). By the way this website was created with [markdown](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll), what a great framework to create a [motherfucking website](https://motherfuckingwebsite.com/)!

Right now? I'm doing research on speech recognition at RobotsMali [AI4D](https://idrc-crdi.ca/en/initiative/artificial-intelligence-development) Lab. If you want to know more about me check my ChatGPT biography @ [whoami](./whoami.md), I'll try to update it maybe once every leap year. Here are some of the stuffs I have worked on and places you can find them (I'll update this more often):

---

## Projects

<div class="timeline">

  <div class="timeline-item">
  <div class="timeline-year">2024 - 2026</div>
  <div class="timeline-dot"></div>
  <div class="timeline-content">
    <div class="timeline-logo">
      <img src="./assets/Robotsmali.png" alt="RobotsMali">
    </div>
    <div class="timeline-text">
      <b>Research Lead on Speech Recognition</b> @ <a href="https://huggingface.co/RobotsMali">RobotsMali AI4D Lab.</a>
      I lead the lab's efforts in building robust speech technologies for Malian languages, managing the full pipeline from data collection to edge deployment.
      <ul>
        <li><b>Dataset & Models (2025):</b> Spearheaded the release of two landmark ASR datasets: 
          <a href="https://huggingface.co/datasets/RobotsMali/afvoices">African Next Voices</a> (612 hours, currently the largest open Bambara corpus) and 
          <a href="https://huggingface.co/datasets/RobotsMali/kunkado">Kunkado</a> (160 hours of radio speech). This dataset are designed to move beyond "clean" speech by capturing real-world disfluencies, background noise, and the heavy code-switching typical of present-day Bambara.
        </li>
        <li><b>An be Kalan:</b> My team developed and deployed ASR models at the edge for the 
          <a href="https://github.com/RobotsMali-AI/an-be-kalan">An be Kalan</a> literacy apps 
          (<a href="https://play.google.com/store/apps/details?id=org.robotsmali.literacy_app&hl=en">Play Store</a>). A major part of this work was ensuring functionality in low-connectivity environments through on-device inference.
        </li>
        <li><b>Open Source:</b> Authored <a href="https://github.com/diarray-hub/bambara-normalizer">bambara-normalizer</a>, the first Python package dedicated to normalizing Bambara text for NLP. I still update it whenever I hit a new edge case while preparing a dataset for training.</li>
        <li><b>Future Focus:</b> Shifting focus toward real-world applications of our models, particularly in <b>Fintech</b> to drive financial inclusion in Mali.</li>
      </ul>
    </div>
  </div>
</div>

<div class="timeline-item">
  <div class="timeline-year">2022 - Present</div>
  <div class="timeline-dot"></div>
  <div class="timeline-content">
    <div class="timeline-logo">
      <img src="./assets/laptop.png" alt="Personal Projects">
    </div>
    <div class="timeline-text">
      <b>Personal Projects & ML Journey</b>
      <br>I’m a Pythonista at heart and a fan of community service. Before the lab was created, I was volunteering on different RobotsMali activities, notably I was a Python trainer at RobotsMali STEM camps in 2023.
      <ul>
        <li><b>Deep Learning from Scratch:</b> Back in the "pre-ChatGPT era," I became obsessed with implementing neural nets and DL technique from scratch after reading <a href="http://neuralnetworksanddeeplearning.com">Nielsen’s book</a>. It was all struggle and learning, but it feels so good when the math is finally mathing. In early 2023, I apply these codes to <a href="https://github.com/diarray-hub/covid_classification">classifying COVID patients</a> and publish them on github (I bet you had forgotten about COVID-19, didn't you?) </li>
        <li><b>Undergrad Research:</b> For my undergrad project, I dove into <a href="https://github.com/diarray-hub/predicting-loans-defaults">loan default prediction</a>, exploring multi-process computing and <a href="https://ieeexplore.ieee.org/document/7344858">Deep Feature Synthesis</a> to handle massive Home Credit databases and compare ML classification algorithms.</li>
        <li><b>Robotics & ROS:</b> Participated in the 2023 Panafrican Robotics Competition (PARC) with Team RobotsMali. We won the bronze medal, and I gained valuable skills in <a href="https://www.ros.org/">ROS</a> and computer vision.</li>
        <li><b>Teaching & Mentorship</b> In 2022, I wrote a series of notebooks in French as an intro to Python for... a dude (bro asked and I simply said ok). In 2024, I released those resources as <a href="https://github.com/diarray-hub/Intro2Python">Intro2Python</a>—four notebooks with a uniquely light tone covering just the basics</li>
        <li><b>Space:</b> Currently reconnecting with a childhood passion for space, exploring how ML can accelerate discovery in astronomical data.</li>
      </ul>
    </div>
  </div>
</div>

</div>

---

## Publications

