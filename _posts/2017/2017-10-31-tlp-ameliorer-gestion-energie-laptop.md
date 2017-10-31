---
layout: post
title:  "Améliorer la gestion d'énergie de votre laptop avec TLP"
date:   2017-10-31 08:01:00
categories:
    - blog
tags:
    - linux
    - batterie
    - alimentation
    - tlp
---

Après avoir fait une nouvelle installation d'Arch Linux sur mon vieux Thinkpad X220, je m'apprêtais à installer le paquet  [laptop-mode-tools \[0\]][0] et sa relativement pénible configuration, quand je suis tombé par une pure coïncidence (et un peu de curiosité quand même) sur [TLP \[1\]][1]. La différence entre les deux est de grande taille : [TLP \[1\]] [1] ne nécessite aucune configuration, mais vraiment aucune, vous installez trois ou quatre paquets et c'est tout et l'économie d'énergie est très significative, j'ai gagné entre 30 et 45 minutes si ce n'est plus.

#### Installation
Pour installer TLP c'est très simple, sur Arch Linux il suffit d'exécuter la commande suivante :
~~~
# pacman -S tlp tlp-rdw
~~~

Pour compléter l'installation, il faut activer les services systemd pour tlp et [tlp-rdw \[2\]][2]:
 ~~~
systemctl enable tlp.service
systemctl enable tlp-sleep.service
systemctl enable NetworkManager-dispatcher.service
~~~

Sur Ubuntu, les deux paquets sont présents dans les dépôts officiels mais il vaut mieux ajouter le PPA suivant pour avoir la version la plus récentes des deux paquets :
~~~
$ sudo add-apt-repository ppa:linrunner/tlp
$ sudo apt-get update
$ sudo apt-get install tlp tlp-rdw
~~~

Si votre ordinateur portable est un Thinkpad, alors il vous faut en plus de de tlp et tlp-rdw installer [tm-smapi \[3\]] [3] et [acpi-call \[4\]][4]. Sur Arch Linux :
~~~
# pacman -S tlp tlp-rdw
~~~

Et sur Ubuntu:
~~~
$ sudo apt-get install tp-smapi-dkms acpi-call-dkms
~~~

Maintenant, vous pouvez lancer TLP : 
~~~
sudo tlp start
~~~

Comme je l'ai dit au début de cet article, tlp ne nécessite aucune configuration, celle par défaut est vraiment optimisée, cependant si vous le souhaitez vous pouvez la modifier en éditant le fichier de configuration /etc/default/tlp, le [site web du projet \[5\]][5] propose des explications de tout les paramètres de configuration.

### Liens
~~~
[0]: https://www.archlinux.org/packages/?name=tlp
[1]: https://aur.archlinux.org/packages/laptop-mode-tools/
[2]: https://www.archlinux.org/packages/?name=tlp-rdw
[3]: https://www.archlinux.org/packages/?name=tp_smapi
[4]: https://www.archlinux.org/packages/?name=acpi_call
[5]: http://linrunner.de/en/tlp/docs/tlp-configuration.html
~~~
[0]: https://www.archlinux.org/packages/?name=tlp
[1]: https://aur.archlinux.org/packages/laptop-mode-tools/
[2]: https://www.archlinux.org/packages/?name=tlp-rdw
[3]: https://www.archlinux.org/packages/?name=tp_smapi
[4]: https://www.archlinux.org/packages/?name=acpi_call
[5]: http://linrunner.de/en/tlp/docs/tlp-configuration.html
