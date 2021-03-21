---
layout: page
title: "Coding"
permalink: /coding/
---

This is where I would share some thoughts on programming. Might be some thoughts on how to solve challenges on HackerRank, or notes about Machine Learning, Web Development and so on.  


<ul>
    {% for post in site.categories.coding %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>