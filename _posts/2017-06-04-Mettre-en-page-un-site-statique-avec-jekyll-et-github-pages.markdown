---
layout: default
title:  "Mettre en page un site statique avec Jekyll et Github Pages"
date:   2017-05-22 00:09:36 +0200
categories: Github Pages Jekyll
---

<h3>Choisir un thème officiel compatible Github page</h3>

Github pages propose une liste de thèmes compatible à l'adresse : <a href="https://pages.github.com/themes/" target="_blanck">https://pages.github.com/themes/</code>
Afin de les utiliser, il faut suivre la procédure d'installation indiqué à l'adresse du dépot du theme choisi.

Dans notre cas, nous choisissons le theme tactile (un thème sobre et responsive) : <a href="https://github.com/pages-themes/tactile" target="_blanck"> https://github.com/pages-themes/tactile </a>

<h2>Installation du thème</h2>


1. Ouvrir le fichier "_config.yml" à la racine de votre site et ajouter le nom du thème :
{% highlight ruby %}
theme: jekyll-theme-tactile
{% endhighlight %}
2. Pour que le thème soit actif aussi en local, vous pouvez modifier le ".gemfile", en ajoutant : <code> gem "github-pages", group: :jekyll_plugins</code>, puis lancer <code>bundle update github-pages</code>
3.Il faut enfin ajouter ou modifier le fichier "_layouts/default.html" en faisant un copier/coller du template présent sur le dépot en ligne d thèmé choisit. 
Dans notre cas : <a href="https://github.com/pages-themes/tactile/blob/master/_layouts/default.html" target="_blanck">https://github.com/pages-themes/tactile/blob/master/_layouts/default.html</a> 

4. Le push une fois effectué, la page rafraichie et l'historique effacé, le nouveau thème devrait actif!

<stong>Remarques :</strong> Si le thème précédent était 'minima', le thème par défaut chargé à la création du site, ces procédures ne sont pas suffisantes 
<ul>
<li>
il faudra aussi effacer toute les références à "minima", que ce soit dans le config.yml, about.md et gemfile. 
</li>
<li>
Il faudra aussi modifier les premières lignes de tous les articles et pages déja écrites en remplacant <code>layout: post</code> par <code> layout: default</code>
</li>
<li>
On remarquera alors que la page d'accueil n'affiche plus les liens vers les articles, comme pouvez le faire minima. Nous allons voir par la suite, comment mettre en page son site et récupéper boutons et fonctionnalités.
</li>

<h2>Personnaliser la page d'accueil d'un site statique sous Jekyll</h2>

Le contenu de la page d'accueil se situe dans le fichier "index.md"


Afficher les derniers articles :
{% highlight ruby %}
<h1>Derniers Articles</h1>
{% for post in site.posts limit:1 %}
{% endhighlight %}

Sources : 

< a href="http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming" target="_blanck">http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming</a>