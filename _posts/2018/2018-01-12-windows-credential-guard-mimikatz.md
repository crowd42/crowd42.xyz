---
layout: post
title: Windows Credential Guard et Mimikatz
date: 2018-01-11 4:23:12
categories:
    - blog
tags:
    - infosec
    - mimikatz
    - windows
    - windows credential guard
    - pentest
---

Demandez à n'importe quel penetration tester son top 10 des outils dont il ne peut pas s'en passer et vous aurez de fortes chances de voir [Mimikatz \[0\]][0] figurez dans le haut de son classement. C'est un outil extrêmement qui permet entre autres l'extraction des mots de passe d'un système d'exploitation Windows, de récupérer les mots de passe en clair ou l'injection des bibliothèques, les certificats ainsi que leurs clés privées, etc.


Afin de mitiger les risques que posent ce genre de logiciels, Microsoft a introduit une nouvelle fonctionnalité dans Windows 10 et Windows Server 2016 : [Credential Guard \[1\]][1]. Cette fonctionnalité permet de stocker les secrets dans un environnement protégé et isolé, inaccessible pour l'utilisateur normal.

Credential Guard s'appuie sur la technologie [Virtual Secure Mode \[\2\]][2] (Sécurité basée sur la virtualisation). Cette dernière se base sur les fonctionnalités de virtualisation qu'offrent les nouveaux CPU. La combinaison des deux permet d'offrir un espace mémoire isolé pour stocké les secrets et qui ne sont pas accessibles au reste du système d'exploitation, en d'autres mots, l'espace mémoire isolé est protégé contre les tentatives de lecture et écriture de la part des autres processus de l'espace mémoire normal utilisé par le système d'exploitation. Pour mieux comprendre comment fonctionne Credential Guard [je vous invite à lire cet article \[3\]][3].
<iframe src="https://mva.microsoft.com/en-US/training-courses-embed/deep-dive-into-credential-guard-16651/Video-Credential-Theft-Lateral-Traversal-cfGBPlIyC_9404300474" width="636" height="480" allowFullScreen frameBorder="0"></iframe>

Credential Guard est un excellent moyen de se défendre contre des outils comme Mimikatz qui permettent d'extraire les hashs pour exécuter des attaques de type [pass the hash \[4\]][4], tant que l'attaquant ne dispose des droits administrateurs ([des droits qu'on peut obtenir plus facilement que vous pouviez l'imaginer \[5\]][5]).

Un des moyens par lesquels Windows gère le processus d'authentification des utilisateurs est [Architecture de l’interface du fournisseur (Security Support Provider) SSP \[6\]][6], par défaut Windows embarque de nombreux modules (NTLM, Kerberos...), mais il est possible d'installer ses propres modules SSP.

Et c'est là que (r)entre en action Mimikatz. En effet ce dernier a dans son arsenal un module SSP (memssp) qui une fois exécuté va être appelé à chaque fois un utilisateur va ouvrir une session et il sauvegardera les identifiants et les mots de passe dans un fichier (`C:\Windows\System32\mimilsa.log`).

D'abord il faut exécuter mimikatz avec en tant qu'administrateur, ensuite il faut activer le mode `debug privilege `

~~~
mimikatz # privilege::debug
Privilege 20 'ok'
~~~

<div>
	<img src="{{ site.baseurl }}/images/posts/2018/mimikatz_debug.png" style="width:75%;" />
</div>
<br />

Puis on injecte le module memssp avec cette commande :
~~~
mimikatz # misc::memssp
Injected =>
~~~

Maintenant préparez vous un café et attendez que des utilisateurs se connectent à la machine, dès qu'un deux va le faire, Mimikatz va intercepter son mot de passe et va l'enregistrer dans le fichier mimilsa.log, vous pouvez consulter ce fichier en l'éditant avec notepad ou en tapant la commande suivante :
~~~
PS C:\Windows\System32> type .\mimilsa.log
~~~
<div>
	<img src="{{ site.baseurl }}/images/posts/2018/mimikatz_ssp.png" style="width:85%;" />
</div>
<br />
Sympa non ? C'est à la fois une des limites de Credential Guard et points forts de Mimikatz et explique pourquoi cet outil est si populaire parmi les pentester :-).

<div>
	<img src="{{ site.baseurl }}/images/posts/2018/34134313-2658eb0e-e45a-11e7-9ded-0229b6da174a.gif" style="width:85%;" />
</div>
<br />

### Liens
~~~
[0]: https://github.com/gentilkiwi/mimikatz
[1]: https://docs.microsoft.com/en-us/windows/access-protection/credential-guard/credential-guard
[2]: http://woshub.com/virtual-secure-mode-vsm-in-windows-10-enterprise/
[3]: https://blogs.technet.microsoft.com/ash/2016/03/02/windows-10-device-guard-and-credential-guard-demystified/
[4]: https://en.wikipedia.org/wiki/Pass_the_hash
[5]: https://crowd42.github.io/comment-jai-pu-gagner-acces-administrateur-serveur-windows-grace-google/
[6]:https://en.wikipedia.org/wiki/Security_Support_Provider_Interface
~~~
[0]: https://github.com/gentilkiwi/mimikatz
[1]: https://docs.microsoft.com/en-us/windows/access-protection/credential-guard/credential-guard
[2]: http://woshub.com/virtual-secure-mode-vsm-in-windows-10-enterprise/
[3]: https://blogs.technet.microsoft.com/ash/2016/03/02/windows-10-device-guard-and-credential-guard-demystified/
[4]: https://en.wikipedia.org/wiki/Pass_the_hash
[5]: https://crowd42.github.io/comment-jai-pu-gagner-acces-administrateur-serveur-windows-grace-google/
[6]: https://en.wikipedia.org/wiki/Security_Support_Provider_Interface
