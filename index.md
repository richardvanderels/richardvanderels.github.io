---
layout: default
title: Blogs
---

<h1>Blogs</h1>

<ul class="post-cards">
  {% for post in site.posts %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
    <p class="post-meta">{{ post.date | date: "%d-%m-%Y" }} · {{ post.categories | join: ", " }}</p>
    {% if post.description %}<p>{{ post.description | escape }}</p>{% endif %}
  </li>
  {% endfor %}
</ul>
