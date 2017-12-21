---
layout: post
title: "GG Microsft !"
date: 2017-12-21 10:45:20
categories:
    - blog
tags:
    - news
    - wtf
    - microsft
    - windows
    - keeper
    - infosec
    - coup de gueule
---

On me demande assez souvent pourquoi je n'utilise pas Windows comme le reste des communs des mortels, et quand on le fait je me lance dans des discours sur le le logiciel libre et des exposés avec arguments techniques à l'appui pour montrer à quel point GNU/Linux est bien supérieur au système d'exploitation de Microsft. Cela dit, je dois avouer que j'ai rarement convaincu mes interlocuteurs. Mais tout ça va changer je crois, grace à l'argument qui tue que j'ai découvert ce matin en lisant mes [flux RSS \[0\]][0].

Tout à commencer il y a plus d'un an, 16 mois pour être précis, quand Tavis Ormandy, le fameux chercheur en sécurité informatique au sein du [Google Project Zero \[1\]][1], a découvert une vulnérabilité très critique dans le gestionnaire des mots de passe Keeper. Cette faille permettait à des sites peu scrupuleux de voler les mots de passe via des techniques comme le [clickjacking \[2\]][2].

Jusqu'à la rien d'anormal, des bugs et failles dans des logiciels on en voit tous les jours. Mais c'était sans compter sur le génie de Microsft. En effet, le même Travis Ormandy a découvert que l'entreprise a embarqué Keeper dans les récentes versions de Windows 10 !
~~~
“I recently created a fresh Windows 10 VM with a pristine image from MSDN, and found that a password manager called “Keeper” is now installed by default,”
~~~

Pas de bol pour Microsft, la version de Keeper pré-installée dans Windows contient la même vulnérabilité que Travis avait découvert il y a 16 mois. Certains ~~trolls~~ pro-windows vont peut-être dire que ce n'est pas de la faute de Microsft et qu'elle n'est pas l'éditrice du logiciel en question; Pardon mais Microsoft n'est pas un petit geek dans sa chambre qui maintient une distro GNU/Linux, c'est une multinationale avec un budget de plusieurs milliards de dollars, elle pourrait quand même effectuer un audit de sécurité d'un logiciel venant d'une source tiers avant de l'inclure par défaut dans son système d'exploitation, ce n'est pas difficile non ? 

Travis Ormandy a remonté la faille aux développeurs de Kepper qui l'ont corrigé en 24 heures, [il avait donné un délai de 90 jours avant de rendre les détails du rapport de la faille publique \[3\]][3]:
~~~
I assume this is some bundling deal with Microsoft. I've heard of Keeper, I remember filing a bug a while ago about how they were injecting privileged UI into pages (   issue 917   ). I checked and, they're doing the same thing again with this version. I think I'm being generous considering this a new issue that qualifies for a ninety day disclosure, as I literally just changed the selectors and the same attack works.
~~~

Il a de même partagé un proof of concept où l'on voit qu'il a réussi à choper le mot de passe Twitter.

<div>
	<img src="{{ site.baseurl }}/images/posts/2017/windows_keeper.png" style="width:75%;"/>
</div>
<br />

Donc pour revenir à mon argument, je ne sais pas pour vous  mais moi je ne ferais pas confiance à une entreprise incapable de faire un code review d'une putaine extension pour navigateur web ! (bon, je sais que les genre n'ont rien à foutre de ça, mais je vais quand même à rêver dans mon coin )


### Liens
~~~
[0]: {{ site.baseurl }}/feed
[1]: http://googleprojectzero.blogspot.com
[2]: https://fr.wikipedia.org/wiki/D%C3%A9tournement_de_clic
[3]: https://bugs.chromium.org/p/project-zero/issues/detail?id=1481&desc=3
~~~
[0]: {{ site.baseurl }}/feed
[1]: http://googleprojectzero.blogspot.com
[2]: https://fr.wikipedia.org/wiki/D%C3%A9tournement_de_clic
[3]: https://bugs.chromium.org/p/project-zero/issues/detail?id=1481&desc=3

