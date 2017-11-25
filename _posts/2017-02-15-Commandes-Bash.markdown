---
layout: default
title:  "Commandes Bash"
date:   2017-02-15 8:30:00 +0200
categories: Linux Bash
tag: Linux Ubuntu Bash
---

# La Commande `bc` pour faire des calculs

Pour le calcul des factorielles : 

```SHELL
echo "Entrer un entier: "
read n
 
## on définit la fonction factorielle
fact="define f (x) {
i=x
fact=1
while (i &gt; 1) {
fact=fact*i
i=i-1
}
return fact
}"
 
## On appelle la fonction fact définie avec un n en paramètre et on fait un pipe avec bc
factorial=`echo "$fact;f($n)" | bc -l`
 
echo "$n! = $factorial"

```
Bc permet aussi de calculer les nombres décimaux :

```SHELL
a=0.1
b=2
for((j=0;j&lt;=10;j++))
do
  for((k=0;k&lt;=10; k++))
    do
    b=$(echo "($b+$a)" | bc ) 
    echo $b
  done
done
```

# Utiliser un script Bash en argument d'un autre script

Script 1 :
```
echo "Script 1 avec les arguments:"
echo "$1" & echo "$2"
echo "$#"
./script2.sh "$1" "$2"
```

Script 2 :
```
echo "Voici les arguments reçus depuis le script 1:"
echo "$1"
echo "$2"
echo "$#"
```
