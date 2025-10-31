---
layout: page
title: Archive
permalink: /archive/
---

## All Notes

{% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
{% for year in posts_by_year %}
### {{ year.name }}
<ul>
  {% for post in year.items %}
  <li>
    <span class="post-meta">{{ post.date | date: "%d %b" }}</span>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  </li>
  {% endfor %}
</ul>
{% endfor %}
