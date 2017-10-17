---
layout: post
title: "Documentaire : Zero leaks"
date:   2017-01-14 00:00:00
categories:
    - movies
tags:
    - documentaire
    - infosec
    - stuxnet
---

Zero days (à ne pas confondre avec [Zero days: Security leaks for sale\[0\]][0]) est
documentaire réalisé par Alex Gibney, à qui on doit des documentaires comme "Taxi
to dark side", récompensé par un Oscar, ou encore "We steal secrets: The stroy
of Wikileaks". Dans son nouveau documentaire, Alex Gibney s'intéresse de plus
près à Stuxnet, le malware qui avait frappé les installations nucléaires
iranienne fin années 2000.
<div style="text-align: center;">
	<img src="{{ site.baseurl }}/images/posts/2017/stuxnet.png" style="width:70%;" />
</div>
<br />

Le Documentaire débute avec un récit détaillant les circonstances entourant
la naissance de stuxnet en commençant par raconter comment est né le programme
nucléaire iranien. On apprend (on le savait un peu déjà) que le malware a été
développé conjointement par États unis, Israël et le Royaume uni, dans un effort
d'arrêter la deuxième de frapper les installations iraniennes et déclencher une
énième guerre dans la région que personne ne voulait.

Stuxnet aurait pu continuer à saboter les centrifugeuses iraniennes sans que
personne ne se rend compte de son existence si les israéliens n'avait pas tout
gâché. En effet, Zero days nous révèle qu'il existait plusieurs versiona du
malware, la dernière était une variante développée par les services de
renseignement israélien, qui était plus agressive que ses précédentes et qui a
échapper à leur contrôle. C'est ainsi que stuxnet aurait infecté des machines et
systèmes SCADA dans les quatre coins du globe.

L'OSINT (pour Open Source Intelligence) a été d'une importance cruciale dans le
développement de stuxnet, c'est à partir des images et vidéos diffusées par la
télévision iranienne que les développeurs ont pu collecter des informations pour
écrire le malware. Grossière erreur des iraniens, qui non seulement a permis
l'attaque stxunet, mais elle a aussi conduit à l'assassinat d'un de leurs
scientifiques.

Ce que j'ai trouvé intéressant dans Zero days, c'est que le documentaire ne
s'est pas contenté raconter l'histoire de stuxnet, qu'on connaisse tous un peu,
mais qu'il a essayé d'explorer les ramifications et les conséquences qu'il aura
causé dans les années à venir et sur l'importance que constitue désormais la sécurité
offensive dans les stratégies des États.

Je ne veux pas tout vous dévoiler, mais il y a un truc que je n'ai toujours pas
compris. L'un des experts invité par Alex Gibney est Eric Chien, un membre de la
Security Response de Symantec. À un moment dans le documentaire, il explique
qu'est-ce qu'un exploit zero day, une tache qui ne devrait pas être compliquée
pour quelqu'un dont le travail consiste à disséquer et analyser les malware pour
une des plus grandes boites de sécurité dans le monde. Sa définition m'a laissé
sans voix, pour lui un zero day c'est code informatique qui permet au malware de
se propager sans qu'il ait besoin d'une action de la victime comme télécharger
un fichier ou l'exécuter ! J'ai dit revoir ce passage une dizaine de fois pour
être sûr de ce que j'ai entendu.

Le documentaire dure deux heures et je peux vous assurer que vous ne serez pas
déçus.


<iframe width="560" height="315" src="https://www.youtube.com/embed/7VgIayOpjEc" frameborder="0" allowfullscreen></iframe>


### Références
~~~
[0]: https://crowd42.github.io/movies/zero-days-security-leaks-for-sale/
~~~

[0]:{{ site.baseurl }}movies/zero-days-security-leaks-for-sale/
