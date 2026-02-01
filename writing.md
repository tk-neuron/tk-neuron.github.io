---
layout: page
title: "Writing"
permalink: /writing/
---

技術ノート、実装メモ、思考の記録。

noteから移行した記事と新規記事を混在。

---

## 最新記事

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
      <h3 class="post-link">
        <a href="{{ post.url }}">{{ post.title }}</a>
      </h3>
      {% if post.excerpt %}
        <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      {% endif %}
    </li>
  {% endfor %}
</ul>

---

## アーカイブについて

- noteからの移行記事は随時追加
- 技術的な学びや実装メモを中心に
- Markdown形式で長期保存
