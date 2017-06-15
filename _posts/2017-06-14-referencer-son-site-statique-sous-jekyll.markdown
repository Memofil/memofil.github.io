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
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: homepage
---

{% endhighlight %}


En regardant de plus près le contenu des templates, vous remarquerez alors qu'ils contiennent les balises `<meta>`,`<title>`...necessaires au référencement. Ces templates contiennent aussi toutes les autres informations necessaires à l'affichage ( Barre de navigation, Header, content, Footer, ...).Or selon la complexité de votre site, le template peut rapidement contenir une grande quantité de lignes rendant la lecture difficile. Heuresement, Jekyll utilise le langage de template Liquid, grace à ce dernier, il est possible de décomposer n'importe quel fichier htlm en sous-fichier html qui seront appelés par lemploie des accolades <code> {{...}}</code>. Cette fonctionnalité est vraiment pratique et permet de limiter beaucoup les erreurs en allégeant l'esprit. Nous allons l'utiliser à la suite.

<h3>Création d'un fichier <code>_includes/meta.htlm<code></h3>

