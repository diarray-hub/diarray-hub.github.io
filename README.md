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
    width: 50px;
    height: 50px;
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

Hi, I'm Yacouba Diarra (**diarray** on the internet) and I care about stuffs like have a blog to post about, well... [stuffs](). By the way this website was created with [markdown](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll), what a great framework to create a [motherfucking website](https://motherfuckingwebsite.com/)!

Right now? I'm doing research on speech recognition at RobotsMali [AI4D](https://idrc-crdi.ca/en/initiative/artificial-intelligence-development) Lab. If you want to know more about me check my ChatGPT biography @ [whoami](./whoami.md), I'll try to update it maybe once every leap year. Here are some of the stuffs I have worked on and places you can find them (I'll update this more often):

---

## Timeline

<div class="timeline">

  <div class="timeline-item">
    <div class="timeline-year">2024 - </div>
    <div class="timeline-dot"></div>
    <div class="timeline-content">
      <div class="timeline-logo">
        <img src="./assets/Robotsmali.png" alt="RobotsMali">
      </div>
      <div class="timeline-text">
        I am a researcher at <b>RobotsMali</b> working on speech recognition...
      </div>
    </div>
  </div>


</div>