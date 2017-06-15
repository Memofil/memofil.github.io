---
layout: default
title:  "Référencer son site statique sous Jekyll"
date:   2017-06-15 10:09:36 +0200
categories: Github Pages Jekyll javascript referencement
---



<h1>Comment bien référencer son site sous Jekyll</h1>

Jekyll utilise des templates  pour gérer la mise en page des articles et pages. Ces templates se trouvent généralement dans le dossier <code>_layouts</code> situé à la racine de votre site.
Par défaut, le dossier <code>_layouts</code>  devrait contenir le template <code>defaul.html</code>, mais vous pouvez aussi créer autant de templates souhaités. Pour pouvoir les utiliser, il faut alors modififer la ligne "layout" au tout début des articles et pages (markdown). Par exemple, pour un nouveau template <code>_layouts/homepage.htlm</code>, utilisé pour la page d'accueil, "index.md" deviendra simplement :

{% highlight ruby %}
---


layout: homepage
# On précise la langue de la page.
lang: fr
---

{% endhighlight %}


En regardant de plus près le contenu des templates, vous remarquerez alors qu'ils contiennent les balises `<meta>`,`<title>`...necessaires au référencement. Ces templates contiennent aussi toutes les autres informations necessaires à l'affichage ( Barre de navigation, Header, content, Footer, ...).Or selon la complexité de votre site, le template peut rapidement contenir une grande quantité de lignes rendant la lecture difficile. Heureusement, Jekyll utilise le langage de template Liquid, grace à ce dernier, il est possible de décomposer n'importe quel fichier htlm en sous-fichier html qui seront appelés par l'emploi des accolades <code> `{{...}}`</code>. Cette fonctionnalité est vraiment pratique et permet de limiter beaucoup les erreurs en allégeant l'esprit. Nous allons l'utiliser à la suite.

<h3> Création d'un fichier <code>_includes/meta.htlm </code>  </h3>

```html
<meta charset="utf-8" />
<meta content='text/html; charset=utf-8' http-equiv='Content-Type'>
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<meta name='viewport' content='width=device-width, initial-scale=1.0, maximum-scale=1.0'>

{% raw %}{% if page.excerpt %}{% endraw %}
  <meta name="description" content="{% raw %}{{ page.excerpt| strip_html }}{% endraw %}" />
  <meta property="og:description" content="{% raw %}{{ page.excerpt| strip_html }}{% endraw %}" />
{% raw %}{% else %}{% endraw %}
  <meta name="description" content="{% raw %}{{ site.description }}{% endraw %}">
  <meta property="og:description" content="{% raw %}{{ site.description }}{% endraw %}" />
{% raw %}{% endif %} {% endraw %}
  <meta name="author" content="{% raw %}{{ site.title }}{% endraw %}" />

{% raw %}{% if page.title %}{% endraw %}
  <meta property="og:title" content="{% raw %}{{ page.title }}{% endraw %}" />
  <meta property="twitter:title" content="{% raw %}{{ page.title }}{% endraw %}" />
 {% raw %}{% endif %}{% endraw %}
```

Une fois le fichier créé, on l'intègre dans le layout choisi sachant qu'en définitive il est préférable de modifier tous les layouts de la même manière ( à moins bien sur que l'on souhaite proposer volontairement des templates différents).
Dans notre cas, nous allons modifier le fichier <code> _layouts/homepage.html <code>. Après avoir mis en commentaires ou supprimé les balises `<meta>` déjà présentes, nous ajouterons juste en dessous de `<head>` la ligne : 

```html
{% raw %}
{% include meta.html %}
{% endraw %}
```

```html
<ul>
  {% raw %}{% for post in site.posts %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
```