---
layout: page
title: 
permalink: /
---

*I'm a freelancing software engineer with strong algorithmic skills and in depth experience
with C# and C++.*

This blog presents a selection of my past and present work as well as some hands-on
solutions to problems I encountered.

<div style="margin-bottom: 5em;"> </div>

---

<div class="post-list">
{% for post in site.posts %}

<small>{{ post.date | date_to_string }}</small>
<h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
<p>{{ post.excerpt }}</p>
<hr />
{% endfor %}
</div>
