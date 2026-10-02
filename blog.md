---
layout: default
title: Blog
---

<div class="catalogue">
  {% for post in site.posts %}
    <a href="{{ post.url | prepend: site.baseurl }}" class="catalogue-item">
      <div>
        <time datetime="{{ post.date | date: '%Y-%m-%d' }}" class="catalogue-time">{{ post.date | date: "%B %d, %Y" }}</time>
        <h2 class="catalogue-title">{{ post.title }}</h2>
        <p>{{ post.content | strip_html | truncatewords: 30 }}</p>
      </div>
    </a>
  {% else %}
    <p>No posts yet — check back soon.</p>
  {% endfor %}
</div>
