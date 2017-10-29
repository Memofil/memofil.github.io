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
<h3>
<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
</h3>
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
</div>
</div>
