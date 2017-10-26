---
layout: post
title: "5 astuces pour sécuriser ses comptes sur les réseaux sociaux"
date:   2017-10-26 00:00:00
categories:
    - blog
tags:
    - sécurité informatique
    - infosec
    - mot de passe
    - réseaux sociaux
---

Sécuriser son compte sur les réseaux sociaux n'est pas vraiment une tache qui demande trop de compétences techniques, à vrai dire elle n'en nécessite aucune, tout ce dont vous avez besoin c''est un peu de bon sens et moins de fainéantise.

Dans ce billet, je vais vous présenter cinq astuces qui vont vous permettre de vous éviter des mauvaises surprises [comme celle la par exemple \[0\]][0].

#### 1- Mots de passe longs, compliqués et uniques
Quand vous choisissez un mot de passe, tachez qu'il soit assez long (une vingtaine de caractères) comportant des lettres majuscules et minuscules et des caractères spéciaux, et surtout utilisez un mot de passe par compte. Comme ça, même si un de vos compte est compromis les autres seront épargnés. Bien évidemment en adoptant cette approche, il vous sera impossible de vous vous rappeler de tout vos mots de passe, c'est pourquoi je vous encourage à utiliser un gestionnaire de mots de passe ([keePass2 par exemple \[1\]][1]).

#### 2- Activez la double authentification
Bien que ça fait des années et des années que la double authentification a été implémenté sur les réseaux sociaux, beaucoup d'utilisateurs ne l'ont toujours pas activée. Pire encore, y en a qui ne sommes même pas au courant de son existence !

La double authentification vous permet d'associer un numéro de téléphone à votre compte, en le faisant vous recevez un sms qui contient un code pin que vous devez saisir quand vous vous connectez pour la première depuis un nouvel appareil (ordinateur, smartphone...).
Donc même en cas de leak de votre adresse email et mot de passe, votre compte ne sera pas compromis (mais ça ne veut pas dire que vous ne devrez pas les changer si ça arrive hein !)

#### 3- Vérifiez en permanence l'activité de votre compte
Quand vous vous connectez à votre compte sur réseau social, ce dernier vous envoie une notification, il le fait aussi pour vous avertir en cas d'échec de connexion, ça peut être vous qui s'est trompé de mot de passe ou quelqu'un d'autre qui essaie de deviner votre mot de passe. Veuillez donc à garder un œil sur votre boite email pour vérifier s'il y a pas une activité soupçonneuse 

#### 4- Vérifiez les liens avant d'y cliquer
Je me souviens il y a 4 ou 5 ans d'une vague de piratage des comptes Twitter, les pirates envoyaient un message privé (DM) contenant un lien qu'il les redirigé vers une fausse page de connexion qui demandait aux victimes de saisir leur pseudo et mot de passe. Ça peut vous paraitre trop gros pour passer mais vous serez étonnés de voir le nombre de comptes qui se sont fait avoir. Conclusion, ne cliquez pas à l'aveugle sur tout les liens qu'en vous envoie, même la personne qui vous les a envoyé est de confiance, si c'est une page de connexion, vérifiez dans la barre de navigation la validité de l'url, si c'est un fichier qu'on vous envoie, scannez le d'abord sur [Virustotal \[2\]][2] avant de l'ouvrir.

#### 5- Vérifiez les applications que vous autorisez à accéder à votre compte
Il y a moins d'un an, une application dont je ne me souviens plus de son nom s'est fait piraté, ce qui avait permet au pirate de publier des tweets depuis les comptes qui utilisaient l'application. Comment est-ce possible ? C'est très simple, quand vous ajoutez une application à votre compte sur un réseau social, ce dernier vous demande si vous souhaitez autoriser ladite application à effectuer certaines actions (lire, écrire...), et malheureusement les gens sont peu regardants quand ils cliquent sur "Autoriser" sur les permissions qu'ils accordent à ces applications.

### Liens
~~~
[0]: https://crowd42.github.io/blog/coup-de-gueule-coinhive/
[1]: https://keepass.info
[2]: http://virustotal.com
~~~
[0]: https://crowd42.github.io/blog/coup-de-gueule-coinhive/
[1]: https://keepass.info
[2]: http://virustotal.com
