---
layout: default
title: GXC.LA
---
<ul>{% for post in site.posts %}{% if post.category == "article" %}
<li>{{ post.date | date: "%Y-%m-%d" }} &raquo; <a href="{{ post.url }}" target="_blank">{{ post.title }}</a></li>
<p>{{ post.description }}</p>
{% endif %}{% endfor %}</ul>
