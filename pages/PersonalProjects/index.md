---
layout: page
title: Personal Projects
permalink: /PersonalProjects/index.html
---

This is a list of the post about mi personal projects and some events I participated.


<div>
<ul>
{% for post in site.posts %}
    {% if post.category == 'Personal' %}
        <li><a href="{{site.url}}{{ post.url }}index.html">{{ post.title }}</a></li>
    {% endif %}
{% endfor %}
</ul>
</div>
