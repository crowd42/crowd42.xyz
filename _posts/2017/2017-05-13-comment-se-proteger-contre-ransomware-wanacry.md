---
layout: post
title: "Comment se protéger contre le ransomware Wannacry"
date:   2017-05-13 00:00:00
categories:
    - blog
tags:
    - ransomare
    - infosec
    - smb
    - wannacry
    - Windows
---
Si vous suivez l'actualité infosec un petit peu, vous avez alors surement entendu
parler du [ransomware Wannacry \[0\]][0] qui vient d'infecter plusieurs hôpitaux en Grande
Bretagne.

Pour l'instant on connait pas exactement le vecteur d'attaque, même
s'il y a plusieurs rumeurs/théories qui circulent sur le Web et Twitter
particulièrement. Parmi elles, la très classique attaque phishing avec une pièce jointe, on parle aussi d'un ordinateur portable infecté qui s'est connecté un réseau pas très sécurisé d'un hôpital et de là le [ransomware \[1\]][1] s'est propagé.

<div>
	<img src="{{ site.baseurl }}/images/posts/2017/wcry.jpg" style="width:75%;" />
</div>
<br />



Ce dont on est sûr par contre c'est que l'attaquant ou les attaquants ont
exploité la vulnérabilité MS17-010 et le [protocole SMBv1 (Server Message Block)\[2\]][2] activé sur les
machines qui ont été infectées.

Pour rappel, la vulnérabilité MS17-010 une fois exploité permettra à un
attaquant malveillant d'exécuter un code à distance. [Microsoft a publié le 14 mars dernier un correctif pour cette faille de sécurité \[3\]][3].

Pour ne pas être la prochaine victime du ransomware Wannacry ou tout autre virus
qui utilise le même mode opératoire, je vous recommande de suivre ces trois
conseils :

- Appliquer en toute urgence les correctifs MS17-010 si ce n'est toujours pas
fait ;
- Désactiver le protocole SMBv1 et bloquer les ports TCP 139, 445 et les ports
UDP 137, 138 ;
- Désactiver les macros !

Pour désactiver SMBv1 sur Windows 7, Windows Server 2008 R2, Windows Vista, and Windows Server 2008 il vous faut exécuter cette ligne Powershell :

~~~
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 -Force
~~~

Pour Windows 8 and Windows Server 2012 :

~~~
Set-SmbServerConfiguration -EnableSMB1Protocol $false
~~~

Pour en savoir plus sur comment désactiver le protocole SMB dans ses trois
versions, [rendez vous sur cette page \[4\]][4]

P.S : j'ai écrit cet article tard la nuit dernière, en me connectant ce matin
j'ai découvert que ce ransomware a infecté plusieurs entreprises dans différent pays.

### Liens
~~~
[0]:https://en.wikipedia.org/wiki/WannaCry_ransomware_attack 
[1]: https://crowd42.github.io/blog/comment-entreprise-preparer-contre-ransomware/
[2]: https://en.wikipedia.org/wiki/Server_Message_Block
[3]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx#ID0ERPAG
[4]: https://support.microsoft.com/en-us/help/2696547/how-to-enable-and-disable-smbv1,-smbv2,-and-smbv3-in-windows-vista,-windows-server-2008,-windows-7,-windows-server-2008-r2,-windows-8,-and-windows-server-2012
~~~
[0]: https://en.wikipedia.org/wiki/WannaCry_ransomware_attack
[1]: https://crowd42.github.io/blog/comment-entreprise-preparer-contre-ransomware/
[2]: https://en.wikipedia.org/wiki/Server_Message_Block
[3]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx#ID0ERPAG
[4]: https://support.microsoft.com/en-us/help/2696547/how-to-enable-and-disable-smbv1,-smbv2,-and-smbv3-in-windows-vista,-windows-server-2008,-windows-7,-windows-server-2008-r2,-windows-8,-and-windows-server-2012

