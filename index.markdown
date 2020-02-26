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

{% for post in site.posts %}

### [{{ post.title }}]({{ post.url }})
<p>{{ post.excerpt }}</p>
---
{% endfor %}
