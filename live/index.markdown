---
layout: default
title: Live
---


<p><br /><b>My Note:</b></p>
  <ul class="posts">
    {% for post in site.posts %} {% if post.category == "live" %}
      <li><span>{{ post.date | date: "%Y-%m-%d"  }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}{% endfor %}
  </ul>
