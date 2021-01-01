---
date: 2011-09-20T14:48:00+02:00
title: "Post-it : Synology partage d'un scanner sur le réseau"
author: "franek"
aliases: [/post/2011/09/20/Post-it-%3A-Synology-partage-d-un-scanner-sur-le-r%C3%A9seau]
tags: ["geek", "ds-211", "hp", "network", "PSC-1100", "réseau", "scanner", "synology", "ubuntu"]
lastmod: 2011-09-24T13:11:16+02:00
---
En branchant son imprimante 2-en-1 (dans mon cas HP PSC-1100 All-in-one) sur un synology (dans mon cas, DS-211+), Il est possible de facilement partager son imprimante sur le réseau.

Le partage du scanner est un peu moins documenté (à moins que votre imprimante all-in-one supporte le protocole MFP). Pour une liste d'imprimantes compatibles avec le Synology, vous pouvez référer à la [liste disponible sur le site du constructeur](http://forum.synology.com/wiki/index.php/User_Reported_Compatible_USB_Printers "Imprimante compatible avec Synology").

Dans notre cas, nous allons devoir bidouiller ("Hackability is fun !"...)

Les tutoriaux suivants sont une bonne base :

- [partage d'un scanner sur le réseau sur ubuntu.com](https://help.ubuntu.com/community/ScanningHowTo)
- [Attaching a scanner to my Synology Diskstation 107](http://arnoutboer.nl/weblog/?p=223)

On va utiliser sane pour partager le scanner. Par défaut, sane ne dispose pas des drivers HP. Il va donc falloir les installer et lui dire qu'ils ont été installés !

1- Installer, de mémoire, les paquets suivants via ipkg :

```

$ ipkg install hplip libusb libieee1284 sane-backends xinetd
```

2- L'astuce dans mon cas est d'ajouter le support des drivers HP à sane :

```

sudo echo "hpaio" >> /opt/etc/sane.d/dll.conf
sudo echo "hpaio" > /opt/etc/sane.d/dll.d/hplip
```

3- On vérifie que le scanner est bien reconnu :

```

sane-find-scanner
```

Cela doit retourner quelque chose comme :

```

found USB scanner (vendor=0x03f0 [Hewlett-Packard], product=0x3011 [psc 1100 series]) at libusb:001:003
```

Si le scanner n'a pas été reconnu, passer votre chemin.

4- Si le scanner a été reconnu, on va vérifier la compatibilité avec sane :

```

scanimage -L
```

Cette ligne doit retourner quelque chose comme :

```

device `hpaio:/usb/psc_1100_series?serial=MY369160GQB0' is a Hewlett-Packard psc_1100_series all-in-one
```

Si elle ne retourne pas ce type d'information, vérifier la configuration de sane et notamment les fichiers dll.conf et hplip.

Votre scanner devrait fonctionner sur le réseau. Pour qu'il fonctionne sur le réseau, il faut s'assurer de 2-3 petites choses.

Vérifier que dans le fichier /opt/etc/xinetd.conf votre sous-réseau est bien présent :

```

    only_from = localhost 10.0.0.0/8 172.16.0.0/12 192.168.0.0/16
```

ainsi que dans le fichier /opt/etc/sane.d/saned.conf :

```

192.168.0.0/16
```

Configurer sane

```

vi /opt/etc/xinetd.d/sane-port
```

Ajouter :

```

service sane-port
{
    port = 6566
    socket_type = stream
    wait = no
    user = root
    group = root
    server = /opt/sbin/saned
}
```

Vérifier que le fichier /etc/services contient bien :

```

  sane-port         6566/tcp        # SANE network scanner daemon
```

Vous pouvez ensuite démarrer sane :

```

/opt/etc/init.d/S10xinetd
```

Sur le poste client, une seule modification :

```

sudo vi /etc/sane.d/net.conf
```

Remplacer **# localhost** par l'**ip de votre serveur**.

Depuis votre poste client, scanimage -L devrait renvoyer quelque chose comme :

```

device `net:<votre ip>:hpaio:/usb/psc_1100_series?serial=MY369160GQB0' is a Hewlett-Packard psc_1100_series all-in-one
```

Voilà, ce sont quelques notes rapides qui seront peut-être utiles à d'autres.

[EDIT](https://franek.chicour.net/post/2011/09/20/EDIT "EDIT")Bon, parfois, le scanner n'est pas accessible depuis le client. J'ai résolu ce problème en supprimant le fichier de PID de dbus et en relançant le process dbus :

```

$ rm /opt/var/run/dbus/pid
$ /opt/etc/init.d/S20dbus start
```

(source : http://forum.synology.com/enu/viewtopic.php?f=27&amp;t=14801)
