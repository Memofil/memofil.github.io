---
layout: post
title:  "Configurer un theme pour son site statique avec Github page et Jekyll"
date:   2017-05-31 00:09:36 +0200
categories: github page jekyll theme 
---


<h3>Configurer un theme pour son site statique avec Github page et Jekyll</h3>




<h3>Exemples de scripts avec le module os </h3>


<p> Imprimer le chemin "pwd" : </p>
{% highlight ruby %}
import os
os.system("pwd")
{% endhighlight %}
    
<p> Créer un dossier "mkdir" : </p>
{% highlight ruby %}
import os
os.system("mkdir " + 'dossier')
{% endhighlight %}

<h3>Exemples de scripts avec le module subProcess</h3>




<p> Imprimer le chemin "pwd" : </p>
{% highlight ruby %}
import subprocess
subprocess.call("pwd")
{% endhighlight %}
    
<p> Créer un répertoire "mkdir" </p>
{% highlight ruby %}
import subprocess
subprocess.check_call(['mkdir', 'dossier'])
{% endhighlight %}
    
<p> Copier un fichier "cp" </p>
{% highlight ruby %}
import os
subprocess.call('cp -r ./dossier1/fichier.txt ./dossier2/', shell=True)
{% endhighlight %}
    
<p> Copier l'intégralité d'un dossier "cp" </p>
{% highlight ruby %}
import os
subprocess.call('cp -r ./dossier1/* ./dossier2/', shell=True)
{% endhighlight %}


<p> Executer un programme contenant des arguments / Exemple avec  "arecord" :  </p>
{% highlight ruby %}
import os
Enregistrement = 'arecord -d 10 test.wav'
subprocess.Popen(Enregistrement, shell=True)
{% endhighlight %}

ou encore ( avec l'Enregistrement qui se fait au niveau du home) : 

{% highlight ruby %}
import os
Enregistrement = 'arecord -d 10 ~/test.wav'
subprocess.Popen(Enregistrement, shell=True)
{% endhighlight %}
    
<h3>Sources :</h3>

<ul>
<li>
<a href="https://help.github.com/articles/creating-a-github-pages-site-with-the-jekyll-theme-chooser/" target="_blanck">https://help.github.com/articles/creating-a-github-pages-site-with-the-jekyll-theme-chooser/</a>
</li>
<li>
<a href="https://docs.python.org/2/library/subprocess.html#subprocess.call" target="_blanck">https://docs.python.org/2/library/subprocess.html#subprocess.call</a>
</li>
<li>
<a href="https://www.cyberciti.biz/faq/python-execute-unix-linux-command-examples/" target="_blanck">https://www.cyberciti.biz/faq/python-execute-unix-linux-command-examples/</a>
</li>
</ul>

{% include footer.html %}

