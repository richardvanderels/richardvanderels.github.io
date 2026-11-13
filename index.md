---
layout: default
title: Blogs
---

<div class="home">

<section class="intro">
  <p class="eyebrow">Tech Blog · Richard van der Els</p>
  <h1>Microsoft Entra, Intune and Security</h1>
  <p class="lead">{{ site.description | strip }}</p>
</section>

{% assign latest = site.posts.first %}
{% if latest %}
<article class="featured">
  <p class="eyebrow">Latest post</p>
  <h2><a href="{{ latest.url | relative_url }}">{{ latest.title | escape }}</a></h2>
  <p class="meta">{{ latest.date | date: "%d-%m-%Y" }} · {{ latest.categories | join: ", " }}</p>
  {% if latest.description %}<p>{{ latest.description | escape }}</p>{% endif %}
</article>
{% endif %}

<div class="grid">
  {% for post in site.posts offset: 1 %}
  <article class="card">
    <p class="meta">{{ post.date | date: "%d-%m-%Y" }} · {{ post.categories | join: ", " }}</p>
    <h2 class="card-title"><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h2>
    {% if post.description %}<p class="card-summary">{{ post.description | escape }}</p>{% endif %}
  </article>
  {% endfor %}
</div>

</div>
