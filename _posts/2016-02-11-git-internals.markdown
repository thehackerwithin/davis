---
layout: post
title: Git Internals
author: Michael Hannon
category: upcoming
tags: meeting git bash python
---

## Attending

Anyone interested in learning a bit more about what makes the version control
system, Git, tick.

## Git Internals with Michael Hannon

As I noticed the haphazard computing practices at the company, I tried to bring
to the company the gospel of Duncan, leading to my giving an introductory talk
about `git`, which I had been using rather casually for a number of years. That
exercise piqued my interest in `git`.  Where do those monstrous ID numbers come
from in the first place?  Where do the files *really* go when you make a new
commit or switch to a new branch?  What is this `HEAD` thing that keeps popping
up in discussions of `git`.

This talk is basically a `core dump` of my brief exploration of those kinds of
questions.

### Short bio

My educational background is in physics, with an emphasis on computational
physics.  Through a circuitous route, I wound up managing a small
computer-support group in the UCD Physics department, which I did until
I retired.

I got interested in computational statistics when I accompanied my wife (a
research scientist with a group in the Stanford medical school, applying
statistics to genetics) to one of Duncan Temple Lang's classes.  There
I discovered that (a) the material was interesting, and (b) and lot of my
background was relevant to the topics.

I currently have a cheesy, hourly job at Stanford, supporting my wife's
computing efforts.  I'm also an unpaid consultant to a small, start-up company
in Davis.  (It pays to stay in school ;-)

### Prerequisites

You should have basic familiarity with
[Git](https://en.wikipedia.org/wiki/Git_%28software%29) and/or other version
control systems. Additionally, we will be using basic
[BASH](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) commands and some
[Python](https://en.wikipedia.org/wiki/Python_%28programming_language%29)
scripts, so basics in programming will be helpful. Be sure to install the
needed software shown below before coming to the tutorial.

### Installation

The linked installation instructions will setup a basic environment on your
operating system of choice (Windows, Mac, Linux) that will give you access to
BASH, Python, Git, and R. In addition, you will need an up-to-date web browser.

[Software Carpentry Standard Installation]({{ site.url }}/swc-installation.html)

### Materials

[https://github.com/DavisDaddy/hacker-talks/tree/master/internals](https://github.com/DavisDaddy/hacker-talks/tree/master/internals)

## Lightning Talks

Please let us know if you'd like to give and informal 3-5 minute lightning
talk. Post and issue or a pull request at:

[https://github.com/thehackerwithin/davis](https://github.com/thehackerwithin/davis)

### 6:00 PM: Automated Image Recognition [Carl Stahmer]

### 6:05 PM: Introduction to Stan, a probabilistic programming language for Bayesian inference. [Matt Espe]

Stan is an open source, simple programming language for creating probabilistic models and conducting inference via several methods (Hamiltonian Monte Carlo, variational inference, and optimization). Runs in C++, with interfaces to many popular analysis programs (R, Python, Julia, command-line, Stata, etc.).

[http://mc-stan.org/](http://mc-stan.org/)

## Meeting Materials

[materials](https://github.com/thehackerwithin/davis/tree/gh-pages/meeting-materials/2016-02-11)
