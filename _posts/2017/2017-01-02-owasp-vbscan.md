---
layout: post
title:  "OWASP VBScan : un script pour auditer les forums VBulletin"
date:   2017-01-02 11:15:00
categories:
    - blog
tags:
    - penetration testing
    - test d'intrusion
    - owasp vbscan
    - vbulletin
---

VBulletin est un CMS pour forum assez populaire bien qu'il soit [propriétaire
[\0\]][0] et surtout pour ses nombreuses failles de sécurité : SQLI, code exec, XSS, remote file
inclusion et j'en passe. [OWASP VBScan \[0\]][0] est un outil écrit en perl qui vous permettra
d'automatiser l'audit des forums VBulletin et de découvrir s'ils sont
vulnérables ou pas.

#### Comment ça fonctionne

OWASP VBScan détecte la version de VBulletin utilisé par votre cible puis va lister toutes les vulnérabilités et
exploits disponibles pour cette version. La liste de ces vulnérabilités et
exploits sont sauvegardés dans le fichier `vbscan/exploit/vbscandb.txt`.

<div style="text-align: center;">
	<img src="{{ site.baseurl }}/images/posts/2017/vbscanpng.png" style="width:75%;" />
</div>
<br />


Ensuite, VBScan va exécuter un ensemble de scripts pour vérifier si des modules
sont à leurs tour vulénrables ou pas et s'il y a des fichiers qui peuvent leaker
des informations sensibles, genre un error_log, un fichier de backup ou de
configuration, etc.

<div style="text-align: center;">
	<img src="{{ site.baseurl }}/images/posts/2017/vbscan.png" style="width:75%;" />
</div>
<br />

Enfin, quand OWASP VBScan aura terminé son scan, il sauvegardera les résultats
dans un rapport sous deux formats, HTML et texte que vous pouvez trouver dans le
répertoire `reports`

#### Installer OWASP VBScan
Pour installer OWASP VBScan, il suffit de cloner le répertoire GIT du projet en
exécutant cette commande :

~~~
$ git clone https://github.com/rezasp/vbscan
$ cd vbscan && chmod +x vbscan.pl
~~~

Et pour le lancer :
~~~
$ ./vbscan votre_cible
$ ./vbscan example.com/forum
~~~
<iframe width="560" height="315" src="https://youtu.be/SirozqDYERA" frameborder="0" allowfullscreen></iframe>

### Liens
~~~
[0]: https://www.owasp.org/index.php/OWASP_VBScan_Project
~~~
[0]: https://www.owasp.org/index.php/OWASP_VBScan_Project

