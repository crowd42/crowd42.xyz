---
layout: post
title:  "Astuce : lister les dépendances d’un paquet"
date:   2014-03-17 21:15:00
categories:
    - blog
    - astuce
tags:
    - apt
    - debian
    - ubuntu
    - fedora
    - astuce
    - GNU/Linux
---

Un petit billet écrit à la va-vite pour partager vous cette astuce que je viens de découvrir, bien que je sois quasi certain qu’elle est déjà connue par mal de personne. Pour faire court, elle s’agit d’une commande APT qui permet de lister les paquets qui dépendent d’un paquet donné en argument.

Comme le signale l’auteur du blog où j’ai découvert cette commande pour la première fois, elle peut être très utile pour lister les applications qui dépendent d’un paquet en qui on vient de découvrir une vulnérabilité. La récente faille GNUTLS est un excellent exemple.

Sur Debian GNU/Linux et dérivés, la commande à exécuter est :
~~~
apt-cache rdepends libgnutls26
~~~
Pour Fedora et Centos
~~~
rpm -q --whatrequires openssl
~~~

