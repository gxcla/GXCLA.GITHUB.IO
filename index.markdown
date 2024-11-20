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

<blockquote>
<p>没有人可以回到过去，但是任何人都可以重新开始；</p><p>如果没有天赋，那么请你一直重复；</p><p>你要相信所有的事与愿违，都是未来惊喜的铺垫；</p><p>向目标奔跑，何必在意折翼的翅膀；</p><p>只要信心不死，定能看见前进的方向；</p><p>人生的道路其实什么都不可怕，</p><p>可怕的是你自己投降！</p>
</blockquote>

[oss]:http://en.wikipedia.org/wiki/Open_source
