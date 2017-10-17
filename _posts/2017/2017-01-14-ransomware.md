---
layout: post
title: "Les ransomware "
date:   2017-01-14 00:00:00
categories:
    - blog
tags:
    - ransomware
    - infosec
---

Quand les premiers virus informatiques ont fait leurs apparitions (quelques
        années avant celle du Web), les motivations des hackers qui l'ont développé étaient
très simple : montrer leurs compétences et prouesses techniques aux autres
membres de la communautés (et parfois pour [plaisanter et foutre la trouille aux
        membres de leurs familles et collègues du bureau \[0\]][0]).

Mais les choses ont vite changé. Des hackers se sont très vite rendu compte
qu'ils pouvaient se remplir les poches facilement et rapidement en usant de leur savoir technique.
Le Web et l'explosion de l'e-commerce dès le milieu des années
90s ont fait que les numéros de carte de crédit ont vite constitué la parfaite cible
pour eux.

Les blackhats comprenaient très bien qu'ils ne pouvaient pas utiliser les numéros
de carte de crédit qu'ils pirataient. Le risque qu'on remonte jusqu'à eux
était très grand, alors ils préféraient les vendre sur le marché noir à des bande de
criminels. Faire chanter leurs victimes était impossible aussi pour les mêmes
raisons.

Cependant, les choses ont commencé à évolué depuis deux ou trois ans. Les monnaies
électroniques, Bitcoin plus précisément, ont changé la donne. Il est possible
maintenant pour les hackers d'extorquer de l'argent directement de leurs
victimes sans craindre qu'on remonte jusqu'à eux.

Le modèle économique derrière les ransomware est très simple. Ces derniers
infectent les machines des victimes (des entreprises de préférences) et
effectuent des taches réversibles, comme chiffrer tout les fichiers qui y se
trouvent ou bloquer l'accès à ladite machine. Pour y accéder de nouveau et
déchiffrer les fichiers, la victime est invité à verser une somme d'argent
sous forme de bitcoin, dans un laps de temps défini par le pirate. Passé cette
durée (souvent quelques jours seulement), les fichiers chiffrées sont perdues
pour toujours.

D'après [une étude réalisée par IBM \[1\]][1] menée auprès
des entreprises et familles américaines, 70% des responsables des entreprises
qui ont été infecté par des ransomware ont accepté de payer la rançon demandée par les pirates pour
récupérer leurs données. Chez les parents de familles, 55% d'eux disent qu'ils
sont prêts à payer les pirates pour récupérer leurs photos.

<div style="text-align: center;">
	<img src="{{ site.baseurl }}/images/posts/2017/ibm-ransomware.jpg" style="width:65%;" />
</div>
<br />

On apprend aussi dans cette étude qu'au moins la moitié des rançons renversées
aux pirates dépassées les 10.000 $ chacune et une sur cinq était au moins de 40.000
$ !

Bien que les entreprises restent la cible privilégiée des hackers, ces derniers
cherchent tout le temps à diversifier leurs surface d'attaque, c'est ainsi
quelques jours avant la fin de l'année 2016, [un ransomware a infecté une smart
TV de LG \[2\]][2] (pas trop smart en fin de compte). Et avec tout ces foyers
qui s'équipent de plus en plus de ce que les marketeux appellent objets connectés
(Internet of things; IoT), on risque d'entendre parler beaucoup d'attaques similaires
dans les mois qui viennent.

Le modèle économique lui aussi est en train d'évoluer. Récemment des nouvelles
variantes de ransomware ont apparait et qui le font choisir entre payer ou de
forwarder un email à un de leurs contacts, si ce dernier se fait infecter et
décide de payer l'attaquant, la première victime retrouve ses données.

Pour fini, je tiens à rappeler que la meilleure défense contre les ransomware
reste la prévention, [dans mon précédent billet \[3\]][3] vous trouverez quelques pistes à
explorer pour vous préparer au pire :-)

### Liens
~~~
[0]: http://time.com/4068738/computer-virus-first-early/?xid=time_socialflow_twitter
[1]: https://www-03.ibm.com/press/us/en/pressrelease/51230.wss
[2]: https://www.hackread.com/lg-smart-tv-screen-android-ransomware-infection/
[3]: https://crowd42.github.io/blog/comment-entreprise-preparer-contre-ransomware/
~~~
[0]: http://time.com/4068738/computer-virus-first-early/?xid=time_socialflow_twitter
[1]: https://www-03.ibm.com/press/us/en/pressrelease/51230.wss
[2]: https://www.hackread.com/lg-smart-tv-screen-android-ransomware-infection/
[3]: {{ site.baseurl }}blog/comment-entreprise-preparer-contre-ransomware/

