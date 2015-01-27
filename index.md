---
layout: default
title: THW -  U. Wisconsin-Madison Branch
---

The Hacker Within, began as a student organization at the University of
Wisconsin-Madison, and is now reborn as a collection of such chapters around
the world.

=====================
Next Meeting
=====================

* Date: Jan 20, 2015
* Time: 12-1 PM
* Location: [2188 Mechanical Engineering][me_map]
* Topic: Jekyll for Github Markdown (maybe)

===================
Posts
===================

{% for post in site.posts %}
{{ post.date | date: "%B %e, %Y" }}     [{{ post.title }}]({{ site.url }} {{ post.url }} )
{% endfor %}


================
Other chapters:
================

  * [U. California-Berkeley](http://thehackerwithin.github.io/berkeley) (USA)
  * [U. Melbourne](http://thehackerwithin.github.io/melbourne) (Australia)

[me_map]: http://map.wisc.edu/s/4olvug5e
