---
layout: post
title:  "Astuce afficher les astérisques quand vous saisissez un mot de passe dans un Terminal"
date:   2014-04-26 21:15:00
categories:
    - blog
    - astuce
tags:
    - astuce
    - blog
    - GNU/Linux
    - Terminal
---
Pour des raisons de sécurité, quand on tape un mot de passe dans un Terminal, rien de ce qu’on saisit ne s’affiche. Cela à pour but d’empêcher ceux qui pourraient se glisser derrière vous et essayer de compter le nombre de caractère de votre mot de passe (information très utile pour un brut force par exemple).

Malgré cela, j’ai remarqué lorsque j’aidais des copains à installer une distribution GNU/Linux pour la première fois, que quelques-uns parmi eux souhaitent tout de même désactiver cette option (y en a même un qui m’a appelé à 2 heure du matin pour me demander ça !).

Après une énième demande, j’ai donc pensé que ce serait utile de partager sur le blog cette astuce, peut-être qu’il y a d’autre personnes qui cherchent à savoir comment faire pour afficher les astérisques.

Tout d’abord, exécutez cette ligne de commande :
~~~
sudo visudo
~~~
Ensuite, cherchez la ligne ci-dessous :
~~~
Defaults env_reset
~~~
Enfin, placez vous à la fin de la ligne et ajouter “pwfeedback” :
~~~
Defaults env_reset,pwfeedback
~~~
Sauvegardez et quitter l’éditeur (:x si celui par défaut est Vim par exemple ou ctrl+x pour nano). Maintenant que vous allez saisir un mot de passe, vous verrez ça :

![screenshot terminal]({{ site.baseurl }}/images/posts/2014/terminal-afficher-asterisques.png "screenshot terminal")
