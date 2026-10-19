---
layout: default
title: Blog
permalink: /blog/
---

<article class="page">
  <h1>Blog</h1>
  <p>Mostly notes on papers I read during my Ph.D. Time to revive it?</p>
  {% assign by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  {% for year in by_year %}
    <h2>{{ year.name }}</h2>
    <ul>
      {% for post in year.items %}
        <li><span class="post-date">{{ post.date | date: "%b %-d" }}</span> · <a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</article>
