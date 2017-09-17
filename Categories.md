---
layout: defaultBootstrap
title: Catégories
menu: main
weight: 10
permalink: /categories/

---
<div>
<div class="card">
<ul>
<li class="card" markdown="1">
![Logo Jekyll]({{site.url}}/assets/images/categories/jekyll-logo.png )
</li>
{% for post in site.posts limit:6 %}
{% if post.categories contains 'Jekyll' %}
<li class="card">
<h3>
<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}<small>{{ post.date | date_to_string }}</small></a>
</h3>
</li>
{% endif %}
{% endfor %}
</ul>
</div>
<div class="card">
<ul>
<li class="card" markdown="1">
![Logo Jekyll]({{site.url}}/assets/images/categories/jekyll-logo.png )
</li>
{% for post in site.posts limit:6 %}
{% if post.categories contains 'Jekyll' %}
<li class="card">
<h3>
<a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}<small>{{ post.date | date_to_string }}</small></a>
</h3>
</li>
{% endif %}
{% endfor %}
</ul>
</div>
<div>

<div class="container">
      <div class="row">
        <div class="col">
          1 of 2
        </div>
        <div class="col">
          1 of 2
        </div>
      </div>
      <div class="row">
        <div class="col">
          1 of 3
        </div>
        <div class="col">
          1 of 3
        </div>
        <div class="col">
          1 of 3
        </div>
      </div>
    </div>


