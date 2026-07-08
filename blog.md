---
layout: default
title: Blog
---

# Blog

**My newly started blog**... Though I'm not really a blogger so it's just occasionally updated

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <small> — {{ post.date | date: "%B %d, %Y" }}</small>
    </li>
  {% endfor %}
</ul>
