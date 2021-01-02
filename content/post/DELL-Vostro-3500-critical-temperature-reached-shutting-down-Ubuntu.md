---
date: 2014-04-26T13:30:00+02:00
title: "DELL Vostro 3500 - \"critical temperature reached, shutting down\" - Ubuntu"
author: ["franek"]
aliases: [/post/2014/04/26/DELL-Vostro-3500-critical-temperature-reached%2C-shutting-down-Ubuntu]
tags: ["geek", "dell", "i8k", "linux", "temperature", "ubuntu", "ventilateur", "Vostro 3500"]
lastmod: 2014-04-26T13:30:00+02:00
---
Il arrive que mon portable "DELL Vostro 3500" s'arrête de manière inopinée. En étudiant les logs (/var/log/kern.log), j'ai ce type de messages :

> kern.log:Apr 23 14:56:04 franek-vostro-3500 kernel: \[ 678.813696\] thermal thermal\_zone0: critical temperature reached(100 C),shutting down

Manifestement, le PC s'arrête car le processeur a atteint une température trop élevée. Le ventilateur (ce portable ne contient qu'un seul ventilateur) ne joue plus correctement son rôle.

Un nettoyage du ventilateur avec de l'air pulvérisé permet de lui redonner une petite jeunesse (Il est également possible de le [démonter entièrement](http://how-i-fixed-it.blogspot.fr/2013/05/laptop-dell-vostro-3500-turns-itself.html)).

Néanmoins, il [est](http://en.community.dell.com/support-forums/laptop/f/3518/t/19385413.aspx) [avéré](http://forum.notebookreview.com/dell-latitude-vostro-precision/512075-vostro-3300-3400-3500-overheating.html) que ce modèle de portable chauffe énormément. Les réglages, par défaut, du démarrage du ventilateur selon la température du processeur ne semblent pas optimisés. Il est possible d'optimiser la gestion du ventilateur grâce au module i8k du noyau. Pour cela, il faut installer le [paquet i8kutils](http://doc.ubuntu-fr.org/i8kutils) :

```
sudo apt-get install i8kutils

```

Ce paquet installe les utilitaires suivants :

- i8kctl : permettant de contrôler le ventilateur
- i8kfan : idem
- i8kmon : démon qui va contrôler la vitesse du ventilateur selon la température du processeur.

Il est possible de modifier la configuration de i8kmon en ajoutant/modifiant le fichier /etc/i8kmon.conf. Personnellement, le fichier contient :

```
# Temperature thresholds: {fan_speeds low_ac high_ac low_batt high_batt}
set config(0)   {{- 0}  -1  40  -1  45}
set config(1)   {{- 1}  30  55  35  60}
set config(2)   {{- 2}  45  80  50  80}
set config(3)   {{- 2}  70 128  70 128}

```

Après la modification du fichier de configuration, il convient de redémarrer le démon :

```
sudo service i8kmon restart

```

Personnellement, ces modifications ont résolu (pour un temps) mes problèmes. Le PC semble moins chauffer et l'ordinateur semble plus silencieux.

Pour aller plus loin :

- [Configuration du Vostro 3500 chez ArchLinux](https://wiki.archlinux.org/index.php/Dell_Vostro_3500)
