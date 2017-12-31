---
layout: page
title: Videogame Portfolio
permalink: /VideogamesPortfolio/index.html
toc: true
---

This is a list of the games I have done in gamejams or as personal projects with friends.

<div>
<ul>
{% for post in site.posts %}
    {% if post.category == 'Videogames' %}
        <li><a href="{{site.url}}{{ post.url }}index.html">{{ post.title }}</a></li>
    {% endif %}
{% endfor %}
</ul>
</div>
