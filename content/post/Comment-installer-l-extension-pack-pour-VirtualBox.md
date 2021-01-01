---
date: 2012-02-11T15:13:00+01:00
title: "Comment installer l'extension pack pour VirtualBox ?"
author: "franek"
aliases: [/post/2012/02/11/Comment-installer-l-extension-pack-pour-VirtualBox]
tags: ["geek", "extensionpack", "virtualbox"]
lastmod: 2012-02-11T15:39:06+01:00
---
J'oublie toujours comment installer l'extension pack pour [VirtualBox](https://www.virtualbox.org/). Je le note donc ici :

1\. Télécharger l'extension pack :

```

$ wget http://download.virtualbox.org/virtualbox/4.1.8/Oracle_VM_VirtualBox_Extension_Pack-4.1.8.vbox-extpack
```

2\. Installer :

```

$ VBoxManage extpack install --replace Oracle_VM_VirtualBox_Extension_Pack-4.1.8.vbox-extpack
```

Il sera nécessaire de renseigner le mot de passe de l'utilisateur connecté pour valider l'installation.

source : [documentation de virtualbox](https://www.virtualbox.org/manual/ch08.html#vboxmanage-extpack)
