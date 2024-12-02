---
layout: default
title: GXC.LA
---

Hi there, I  am an open-source enthusiast, an [Open Source][oss] enthusiast. This site is
dedicated to providing information about [me](resume.html) and [what I do](/work).

I am a screencastr at <https://GXC.LA>.


<p><br /><b>My Note:</b></p>
  <ul class="posts">
    {% for post in site.posts %}{% if post.category == "default" %}
      <li><span>{{ post.date | date: "%Y-%m-%d" }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}{% endfor %}
  </ul>

<p><b>Find me on:</b></p>

<ul>
<li><a href="https://github.com/gxcla/">Github</a></li>
</ul>
<p><br /><b>What's up:</b></p>

<blockquote><p>山高万仞，只登一步！</p></blockquote>

[oss]:http://en.wikipedia.org/wiki/Open_source
