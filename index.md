---
layout: default
title: Home
---

<div class="hero">
  <h1>Jesse Houston</h1>
  <p>Game Industry Veteran | CEO | Board Member</p>
</div>

## Welcome

Welcome to my personal website. I'm a long-time veteran of the video game industry, currently serving as Co-Founder and CEO of Critical Path Games.

Throughout my career, I've had the privilege of working on beloved franchises like Mass Effect, League of Legends, and co-founding Phoenix Labs where we created Dauntless and Fae Farm.

## Recent Posts

<ul class="post-list">
{% for post in site.posts limit:3 %}
  <li>
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="post-meta">{{ post.date | date: "%B %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </li>
{% endfor %}
</ul>

[View all posts &rarr;]({{ '/blog' | relative_url }})
