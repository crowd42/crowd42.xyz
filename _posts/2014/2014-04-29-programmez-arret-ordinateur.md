---
layout: post
title:  "Astuce : programmez l'arrêt de votre ordinateur"
date:   2014-04-28 21:15:00
categories:
    - blog
    - astuce
tags:
    - astuce
    - linux
---

Vous avez lancé le téléchargement d’un fichier qui va prendre plus de temps que prévu et à cause d’un rendez-vous, vous ne pouvez pas attendre qu’il soit terminé pour éteindre votre ordinateur ? Pas grave, voilà une petite simple qui pourra vous être utile.

Supposons qu’il est 20h00 et que vous souhaitez que votre ordinateur s’éteint vers 20h20, nous avons deux solutions aussi simple l’une que l’autre. La première consiste à exécuter la commande “shutdown” avec en paramètre l’heure vers laquelle on veut que notre ordinateur s’arrête :
i
~~~
su -c 'shutdown 20:20'
~~~
Quant à la deuxième solution, on va utiliser la même commande “shutdown”, sauf que cette fois-ci, elle va prendre en paramètre le nombre de minute qui reste avant 20:20 :
~~~
su 'shutdown +20'
~~~
Maintenant que faire si vous avez décidé de ne plus, sortir ou que vous avez rentré plutôt que prévu et du coup plus besoin que votre ordinateur s’arrête à 20:20 ? fastoche, il suffit d’exécuter la ligne de commande suivante :
~~~
su -c ‘shutdown -c’
~~~
Enjoy it
