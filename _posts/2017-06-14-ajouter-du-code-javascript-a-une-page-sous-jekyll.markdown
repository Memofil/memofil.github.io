---
layout: default
title:  "Ajouter du code javascript à une page sous Jekyll"
date:   2017-06-14 00:09:36 +0200
categories: Github Pages Jekyll javascript
---

<h3>Javascript, Jekyll et Github Page</h3>


Notre site web est un site web static sous Jekyll et heberger par Github Page. Nous allons voir comment intégrer du javascript à nos pages.



1) Pour cela, nous allons tout d'abord choisir une bibliotheque javascript pour notre projet. Dans notre cas nous utiliserons jQuery.Il existe deux manières integrer cette librairie à notre site, Soit nous téléchargeons le code source pour le placer à la racine du site, soit nous utilisons la version en ligne (mise à disposition par google), qui sera chargée à chaque chargement de notre page. Dans notre cas, nous allons choisir la deuxième solution qui a le mérite d'etre "généralement" mis à jour, cela nous evite aussi de surcharger notre dépot git..
Ainsi, pour que javascript soit compris par le navigateur il faudra ajouter au template html "default.html" (mais aussi n'importe lequel autre) et pour plus de clarté entre les balises <link> et <title> : 
{% highlight ruby %}
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
{% endhighlight %}

2) Ensuite nous allons créer un sous-répertoire "_scripts" dans le dossier "_includes" situé à la racine de notre site. 

{% highlight ruby %}
mkdir -p _includes/_scripts
{% endhighlight %}

3) Nous pouvons maintenant enregistrer notre script "mon_script.js" dans ce nouveau répertoire. 
Pour la démonstration, nous allons prendre un exemple de script ( provenant de <a href="https://www.w3schools.com/html/html_scripts.asp" target="_blanck" >w3schools.com</a> :


{% highlight ruby %}


<h1>Mon premier JavaScript</h1>

<button type="button"
onclick="document.getElementById('demo').innerHTML = Date()">
Cliquez pour afficher la date et l'heure.</button>

<p id="demo"></p>
{% endhighlight %}


Pour insérer un script dans un template html : 

4) Enfin, nous ajoutons l'adresse de ce script au temple html choisi pour cette page.
Dans notre cas, nous voulons que ce script s'affiche dans le footer de toutes les pages associés aux template sélectionné.
Ainsi, dans le répertoire "_layout", nous ouvrons "default.htlm" et ajoutons entre les balises <footer>...</footer> la ligne suivante :
{% highlight ruby %}
{% include _scripts/monScript.js %}
{% endhighlight %}

Jekyll utilise les templates <a href="https://shopify.github.io/liquid/" target="_blanck">Liquid</a> pour organiser les pages. Dans ce formalisme, l'appel d'un script est particulier, on ne va pas utiliser les balises <script> propre au langage html. Jekyll se chargera alors de transformer le code en html pour q'il soit compris par la navigateur.

<h3>Pour insérer un script javasript dans un post.</h3>
Les articles Jekyll utilisent le langage markdown.  écrire : 
{% highlight ruby %}
{% include _scripts/monScript.js %}
{% endhighlight %}
ce qui va nous donner : 

{% include _scripts/monScript.js %}

 