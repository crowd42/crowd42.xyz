---
layout: post
title:  "8 conseils pour les entreprises pour se défendre contre les ransomware"
date:   2017-01-10 00:30:00
categories:
    - blog
tags:
    - ransomware
    - infosec
---
### Sommaire
{:.no_toc}

* toc
{:toc}

#### Introduction
Dans un précédent billet, je vous ai parlé de l'initiative [No More Ransom
\[0\]][0], qui aspire à aider les victimes des ransomware à reprendre le
contrôle de leurs ordinateurs infectés. Une initiative très louable mais qui a malheureusement ses limites.

D'abord, parce que No More Ransom n'est pas une solution miracle qui marchera
contre tout les ransomware et il ne le sera jamais. Malgré tout le efforts des
gens et entreprises derrière cette initiative, il y aura toujours des malins qui vont développer des nouveaux malwares (oui, un
ransomware n'est d'autre qu'un malware). Tout comme les anti-virus n'ont pas
réussi à offrir une protection à 100% contre les virus.

Deuxièmement, les ransomware sont un peu comme les [payloads \[1\]][1],
    l'infection est le résultat de l'exécution d'un [exploit \[\2\]][2] ou d'une campagne de
phishing. Dès lors la meilleure protection contre les ransomware c'est d'adopter une
approche pro-active. Prévenir vaut mieux que guérir, n'est-ce pas ?

Alors qu'ils sont les actions qu'une entreprise doit prendre pour éviter d'être
la prochaine victime des ransomware ?

#### 1. Backup, backup et backup

C'est AMHA la meilleure défense qui existe contre les ransomware,
    malheureusement il existe encore des entreprises, surtout des PME, qui n'ont
    toujours pas pris conscience de l'importance d'avoir des sauvegardes à jour de
    leurs données. Et même quand c'est fait, on peut pas dire que les bonne
    pratiques ont été respecté : des backup sur des CD/DVD ou clé USB, zéro
    vérification de l'intégrité de la sauvegarde, etc.

Je conseille toujours à mes clients de faire des sauvegardes quotidiennes de
leurs données sensibles (par exemple la base de données de l'ERP si elle est
        hébergée localement), et les données les moins sensibles de manière
hebdomadaire et de garder trois copies minimum des sauvegardes dans des endroits
différents :

* une sur un disque externe :
* une autre sur un [NAS \[3\]][3] ;
* une dernière sur un service de stockage en ligne, de préférence une solution hébergée
sur un serveur de l'entreprise.

Certains ransomware infectent aussi les disques durs externes connectés aux
ordinateurs victimes, donc une fois que votre sauvegarde est terminée, songez à
le retirer de l'ordinateur. 

Enfin, il ne faut surtout pas oublier de vérifier l'intégrité de vos sauvegardes, qu'il n'y a pas eu d'altération
(volontaire ou non) des données. Le mot clé est de ne jamais faire confiance aux programmes. Testez vos backup au moins une fois par mois.

#### 2. Security Awareness Training

Tous les rapports et études réalisés par les sociétés spécialisées le disent : le
phishing et le social-engineering restent les vecteurs les plus utilisés pour
infecter les entreprises. <br />
Je sais que les patrons et entreprises marocaines ne sont pas habitués à ça,
   mais ce genre de formation n'est pas un luxe dont ils peuvent
   s'en passer de nos jours. 

   Ces formations et ateliers permettent à vos employés d'acquérir des réflexions qui vont leurs permettre de distinguer par
   exemple un email légitime d'un autre malicieux, de savoir comment repérer un
   [mail spoofing \[4\]][4]. Dans une attaque de type [Spear Phishing \[5\]][5],
   l'attaquant peut par exemple usurper l'identité et envoyer un email qui va
   paraitre légitime à un employé (genre nomDuN+1@entreprise.com), d'où
   l'utilité de toujours scanner les fichiers joints que vous recevez, même
   s'ils sont envoyés par des adresses de confiance.

Les réseaux sociaux sont un autre vecteur dans les attaques phishing, au lieu de
les censurer (vos employés trouveront toujours un moyen de contourner ce blocage), essayez plutôt
de les sensibiliser à l'usage des réseaux sociaux.

#### 3. Gestion des correctifs logiciels

Les exploit kits qui sont d'ailleurs le moyen préféré des hackers pour délivrer
leurs exploits et payloads, profitent des vulnérabilités dans les
logiciels installés sur les machines des victimes pour les infecter, d'où
l'intérêt d'avoir une politique de gestion de correctifs au sein des
entreprises.

Une bonne politique de gestion de correctifs doit impérativement inclure non
seulement les mises à jour du système d'exploitation et les applications métiers
critiques, mais aussi tout les logiciels tiers, notamment les addons et plugins
installés sur les navigateurs web à commencer par [flash \[6\]][6] et java. N'oubliez pas,
    les blackhats n'ont besoin que d'une application vulnérable sur une seule
    mqchine pour compromettre tout votre système d'information.

#### 4. Antivirus, malware et firewalls

Là encore c'est fou le nombre des utilisateurs qui s'obstinent à installer des
antivirus et anti-malware sous prétexte que ça ralenti leurs machines ! Si un
jour quelqu'un vous fourni ce conseil, vous pouvez lui foutre une claque, vous
avez ma bénédiction. 

Cependant, installer un antivirus et payer une petite fortune annuellement pour les
licences de votre parc informatique sans les jamais mettre à jour est une
aberration. Assurez vous toujours d'appliquer les mises à jour que vous proposent
votre antivirus. L'utilisation d'un firewall ajoutera une autre couche de
sécurité non négligeable, idem pour le système de [détection d'intrusion (IDS)
\[7\]][7].

#### 5. Liste blanche des applications autorisées

Une autre pratique qui a prouvé son efficacité, c'est d'établir une liste blanche des applications
autorisées à s'exécuter sur les machines de l'entreprise. Je recommande souvent
à mes clients de privilégier cette méthode au blacklisting (liste noir), tout
simplement parce qu'il est plus facile de déterminer les applications et
logiciels qu'on veut voir s'exécuter sur nos machines que de mettre en place une
liste des applications à bloquer, chose qui est tout simplement impossible à
réaliser.

Cette technique peut s'étendre aussi au plugin flash, si vous en avez besoin au
travail, vous pouvez alors l'autoriser seulement sur les sites web de confiance
et le bloquer sur les autres.

Depuis 2015 on sait qu'il est possible qu'un [ransomware se propage en via les
publicités sur les sites web \[8\]][8] que vous visitez. Installez un adbloack (je
        vous recommande uBlock origin), c'est gratuit et vous protégera d'autres
risques.

Les fichiers avec des macros dedans (.docm par exemple) sont aussi à surveiller
de très près et devront être scanner et filtrer par votre serveur mail avant
d'être délivrer. Idem pour le fichiers exécutables.

#### 6. Gestion des droits et permissions

La majorité des taches que vos employés exécutent sur leurs machines (lecture et
        envoie des emails, navigation web, édition de documents...) ne requirent
pas des droits qui leurs permettront de démarrer ou d'arrêter des services,
    d'éditer des clés du registre Windows, d'installer des programmes, etc. Inutile donc qu'ils aient
    des droits très élevés sur leurs ordinateurs alors qu'ils
    n'en ont pas besoin. Le cas le plus flagrant est sans doute toutes machines
    Windows dont l'utilisateur par défaut est le compte administrateur créer au
    moment de l'installation !
    
Pour comprendre les risquent que ça peut engendrer, il faut savoir que la plupart 
des programmes malveillants (malwares, virus, ransomware...) s'exécutent en
utilisant les droits et permissions de l'utilisateur connecté. Si cet
utilisateur est un administrateur, alors le malware va lui aussi s'exécuter 
avec les droits administrateur.

#### 7. Network segmentation

Une autre méthode de résister aux attaques c'est que les administrateurs réseaux
de votre entreprise appliquent une [segmentation de leurs réseau \[\9\]][9]Au lieu de laisser tout vos
employés accéder aux fichiers depuis un seul serveur et réseau, le mieux serait
de les séparer en groupes, ainsi si un serveur ou réseau se fait compromettre,
   ça n'affectera pas tout le monde.

#### 8. Tests d'intrusion
Enfin, il est bon d'avoir d'auditer le système informatique de votre entreprise
en réalisant des [test d'intrusion \[10\]][10]. Ils vont vous permettre
d'identifier les failles potentielles dans votre système d'information et les
corriger avant qu'elles soient exploité par un attaquant malveillant.

#### Conclusion
Voilà, c'est loin d'être une liste exhaustive de toutes les actions à prendre
pour se défendre contre les ransomware, mais j'espère quand même qu'elle va vous
aider. Dans un prochain billet, je vais vous parler des actions et démarches à
faire si vous êtes infectés par un ransomware.

Si vous avez des questions, remarques ou besoin d'aide, vous pouvez me contactez
ici en laissant un commentaire, par email ou via [Twitter \[11\]][11] et
j'essaierai de vous répondre dans les plus bref délais.

### Liens
~~~
[0]: {{ site.baseurl }}blog/no-more-ransom
[1]: https://en.wikipedia.org/wiki/Payload_(computing)#Security
[2]: https://en.wikipedia.org/wiki/Exploit
[3]: https://en.wikipedia.org/wiki/Network_Attached_Storage
[4]: https://en.wikipedia.org/wiki/Mail_spoofing
[5]: https://fr.wikipedia.org/wiki/Spear_phishing
[6]: https://www.recordedfuture.com/top-vulnerabilities-2015/
[7]: https://en.wikipedia.org/wiki/Intrusion_Detection_system
[8]: http://arstechnica.com/security/2016/03/big-name-sites-hit-by-rash-of-malicious-ads-spreading-crypto-ransomware/
[9]: https://fr.wikipedia.org/wiki/Segmentation_r%C3%A9seau
[10]: https://fr.wikipedia.org/wiki/Test_d'intrusion
[11]: https://twitter.com/crowd42
~~~

[0]: {{ site.baseurl }}blog/no-more-ransom
[1]: https://en.wikipedia.org/wiki/Payload_(computing)#Security
[2]: https://en.wikipedia.org/wiki/Exploit
[3]: https://en.wikipedia.org/wiki/Network_Attached_Storage
[4]: https://en.wikipedia.org/wiki/Mail_spoofing
[5]: https://fr.wikipedia.org/wiki/Spear_phishing
[6]: https://www.recordedfuture.com/top-vulnerabilities-2015/
[7]: https://en.wikipedia.org/wiki/Intrusion_Detection_system
[8]: http://arstechnica.com/security/2016/03/big-name-sites-hit-by-rash-of-malicious-ads-spreading-crypto-ransomware/
[9]: https://fr.wikipedia.org/wiki/Segmentation_r%C3%A9seau
[10]: https://fr.wikipedia.org/wiki/Test_d'intrusion
[11]: https://twitter.com/crowd42

