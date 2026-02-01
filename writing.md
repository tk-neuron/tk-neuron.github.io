---
layout: page
title: "Writing"
permalink: /writing/
---

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

{% if site.posts.size == 0 %}
記事を準備中です。[note](https://note.com/mybrain_record)もご覧ください。
{% endif %}
