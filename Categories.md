---
layout: defaultBootstrap
title: Catégories
menu: main
weight: 10
permalink: /categories/

---
<div class="cardBox">

<div class="card">
<ul class="card">
<li class="card" markdown="1">
![Logo Jekyll]({{site.url}}/assets/images/categories/jekyll-logo.png )
</li>
{% for post in site.posts limit:6 %}
{% if post.categories contains 'Jekyll' %}
<li class="card">
<p class="card">
<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
</p>
</li>
{% endif %}
{% endfor %}
</ul>
</div>
<div class="card">
<ul>
<li class="card" markdown="1">
![Logo raspberry]({{site.url}}/assets/images/categories/rpi-logo.png )
</li>
{% for post in site.posts limit:6 %}
{% if post.categories contains 'Raspberry' %}
<li class="card">
<p class="card">
<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
</p>
</li>
{% endif %}
{% endfor %}
</ul>
<div class="card">
<ul>
<li class="card" markdown="1">
![Logo raspberry]({{site.url}}/assets/images/categories/linux-crystal-Tux.png )
</li>
{% for post in site.posts limit:6 %}
{% if post.categories contains 'Linux' %}
<li class="card">
<p class="card">
<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
</p>
</li>
{% endif %}
{% endfor %}
</ul>
</div>
</div>
<div >
{% assign tags = site.tags | sort %}
{% for tag in tags %}
 <span class="site-tag">
<a href="/tag/{{ tag | first | slugify }}/"
style="font-size: {{ tag | last | size  |  times: 4 | plus: 80  }}%">
{{ tag[0] | replace:'-', ' ' }} ({{ tag | last | size }})
</a>
</span>
{% endfor %}
</div>
</div>
