---
layout: layout
title: Upcoming Topics
---

<section class="content">

Upcoming Topics
================

**Spring 2015**

<ul class="listing">
{% assign upcoming = (site.posts | where: "category", "upcoming") %}
{% for post in upcoming reversed %}
<li><span>{{ post.date | date: "%B %e, %Y" }}</span> <a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>

</section>
