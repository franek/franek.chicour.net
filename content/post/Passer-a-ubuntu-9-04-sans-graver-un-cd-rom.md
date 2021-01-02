---
date: 2009-04-27T19:08:00+02:00
title: "Passer à ubuntu 9.04 sans graver un cd-rom"
author: ["franek"]
aliases: [/post/2009/04/27/Passer-%C3%A0-ubuntu-9.04-sans-g%C3%A2cher-un-cd-rom]
tags: ["geek", "9.04", "jaunty jalope", "ubuntu", "upgrade"]
lastmod: 2009-04-27T20:03:13+02:00
---
La dernière version de Ubuntu (Jaunty Jalope 9.04) est sortie le jour de mon anniversaire. Voici les commandes à exécuter si vous souhaitez mettre à jour rapidement votre version sans passer par apt. Perso., j'utilise toujours cette manip' qui est bien plus rapide.

1\. [Télécharger](http://www.ubuntu-fr.org/telechargement?methode=) l'iso du CD alternate de Ubuntu et placer le fichier sur votre bureau. 2. Si l'iso est présente sur votre bureau, exécuter les commandes suivantes en ligne de commande :

`sudo mount -o loop ~/Desktop/ubuntu-9.04-alternate-i386.iso /media/cdrom0`

3\. Une boite de dialogue vous invitant à mettre à jour votre ubuntu devrait s'ouvrir. 4. Suivez les instructions présente à l'écran.

Si la boite de dialogue n'apparait pas automatiquement, vous pouvez lancer la commande suivante en ligne de commande (ou via Alt+F2) :

`gksu "sh /cdrom/cdromupgrade"`

Toutes les infos sont sinon présentes sur les [sites officiels de Ubuntu](http://www.ubuntu.com/getubuntu/upgrading) et de la[ communauté française](http://doc.ubuntu-fr.org/installation).
