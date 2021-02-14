---
layout: page
title: "Music"
permalink: /music/
---

This is where I would share some thoughts on acoustic guitar playing. 

<ul>
    {% for post in site.categories.music %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>