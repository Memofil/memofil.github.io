---
layout: default
title: Catégories
menu: main
weight: 10
permalink: /categories/

---


<div>
<ul>
<li>
![Logo Jekyll]({{site.url}}/assets/images/categories/jekyll-logo.png)
</li>
<li>
<img src="{{site.url}}/assets/images/categories/jekyll-logo.png" />
</li>

{% for post in site.posts %} 
{% if post.categories contains "rpi" %}
 <li>{{ post.title }}</li> 
{% endif %}
{% endfor %}
</ul>
</div>
<div>
<ul>
<li>
![Logo Jekyll](/assets/images/categories/jekyll-logo.png)
</li>
{% for post in site.posts %} 
{% if post.categories contains "jekyll" %}
 <li>{{ post.title }}</li> 
{% endif %}
{% endfor %}
</ul>
</div>

