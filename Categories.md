---
layout: defaultBootstrap
title: Catégories
menu: main
weight: 10
permalink: /categories/

---
<div class="cardBox">
<div >
<ul>
{% for post in site.tags[page.tag] %}
  {% if post.lang %}
  <li lang="{{post.lang}}">
  {% else %}
  <li>
  {% endif %}
  	<a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
  	{{ post.description }}
  	<!-- Tags: {{ post.tags | join: ", " }} -->
  </li>
{% endfor %}
</ul>
</div>
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
