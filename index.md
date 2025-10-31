---
layout: default
title: Home
---

# Learning Log

Welcome. This blog captures hands-on experiments and notes so I can revisit hard-earned lessons. Recent entries appear below; use the archive for older work.

<ul class="post-list">
  {% for post in site.posts %}
  <li>
    <span class="post-meta">{{ post.date | date: "%d %b %Y" }}</span>
    <h2><a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p>{{ post.excerpt | strip_html | truncate: 140 }}</p>
  </li>
  {% endfor %}
</ul>

[View all notes]({{ "/archive/" | relative_url }})
