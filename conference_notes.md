---
layout: page
title: Conference Notes
---

Notes from the conferences I have attended.

<ul>
  {% for post in site.notes %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> | {{ post.where }}
    </li>
  {% endfor %}
</ul>