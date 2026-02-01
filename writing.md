---
layout: page
title: "Writing"
permalink: /writing/
---

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <time class="post-meta">{{ post.date | date: "%Y.%m.%d" }}</time>
      <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
