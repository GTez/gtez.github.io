---
layout: default
title: Blog
permalink: /blog/
description: Jesse Houston's blog on game development, leadership, building teams, and the gaming industry. Insights from a veteran CEO and co-founder with experience at BioWare, Riot Games, and Phoenix Labs.
keywords: game development blog, gaming industry insights, leadership, team building, Jesse Houston blog, video game development
image: /assets/images/jesse-houston.jpg
---

# Blog

<ul class="post-list">
{% for post in site.posts %}
  <li>
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="post-meta">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </li>
{% endfor %}
</ul>
