---
layout: page
title: Blog
---

{% for post in site.posts %}
<h2>{{ post.title}} </h2>
<span class="post-date">{{ post.date | date_to_string }}</span>

{{ post.excerpt }}

<a href="{{ post.url }}"><i>read more</i></a>
<hr>
{% endfor %}

<!-- <ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul> -->