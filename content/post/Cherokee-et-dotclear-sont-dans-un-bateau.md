---
date: 2010-05-28T18:48:00+02:00
title: "Cherokee et dotclear sont dans un bâteau..."
author: ["franek"]
aliases: [/post/2010/05/28/Cherokee-et-dotclear-sont-dans-un-b%C3%A2teau...]
tags: ["développement web", "cherokee", "dotclear", "installation"]
lastmod: 2011-10-16T21:34:54+02:00
---
Ce [blog](http://franek.chicour.net/) et [une partie de ces satellites](http://www.chicour.net/) (migration en cours) tournent désormais sur [cherokee](http://www.cherokee-project.com/), un serveur web léger concurrent de Apache, Lighthttpd, nginx,... Je n'ai pas trouvé de ressources sur la configuration de dotclear avec Cherokee donc voici quelques notes. J'espère que cela pourra aider certains d'entre vous. J'essaierai de détailler si besoin.

Installation de cherokee 
-------------------------

Je vous invite à lire la [documentation du projet](http://www.cherokee-project.com/doc/)qui est relativement complète.

La version 1.0 de Cherokee est depuis peu disponible dans la branche testing de Debian.   
Si vous utilisez une debian stable, vous pouvez utiliser le [système de Pinning](http://wiki.debian.org/AptPreferences) en utilisant les dépôts testing :   
```
apt-get install cherokee -t testing
```

  
Il faudra également que vous installiez le paquet php5-cgi ainsi que mysql. Il y a plein de tutos sur le net sur ce sujet.  
Configuration de Dotclear
-------------------------

Je vous invite à suivre la [procédure habituelle](http://fr.dotclear.org/documentation/2.0/admin/clean-install). Dans mon cas, dotclear est installé dans le répretoire /usr/share/dotclear-2.1.7. J'ai un lien symbolique dotclear2 qui pointe sur dotclear-2.1.7 (qui permet de switcher d'une version à l'autre).  
  
J'ai un répertoire /usr/share/dotclear2-all-blogs qui contient les thèmes et les plugins communs à l'ensemble des blogs hébergés.  
  
J'utilise dotclear en multiblog. Chaque blog dispose dispose des plugins communs. Les thèmes ne sont pas partagés. Chaque blog dispose de son sous-domaine :   
exemple : user1.domain.net, user2.domain.net  
  
Ces blogs sont hébergés dans /var/www/  
Exemple :   
- /var/www/domain.net/user1/public\_html pour user1.domain.net
- /var/www/domain.net/user2/public\_html pour user2.domain.net

Dans chaque répertoire public\_html, j'ai donc un fichier index.php dont l'identifiant du blog a été modifié et dont le chemin du require a été modifié :   
```
<p><?php<br></br>define('DC_BLOG_ID','user1'); # identifiant du blog<br></br>require '/usr/share/dotclear2/inc/public/prepend.php';</p>
```

Dans le fichier de configuration, j'ai ajouté les lignes suivantes afin de charger les thèmes dans les profils utilisateurs :  
```
<p>// Modification de la configuration du blog lors de l'initialisation<br></br>// cf. http://forum.dotclear.net/viewtopic.php?id=33875<br></br>$__top_behaviors[] = array('coreBlogConstruct','modifConfig');<br></br><br></br>function modifConfig($blog) {<br></br>  $blog->themes_path = '/var/www/domain.net/'.$blog->id.'/public_html/themes';<br></br>  $blog->public_path = '/var/www/domain.net/'.$blog->id.'/public_html/public';<br></br>}</p>
```

Tous les blogs sont configurés en mode PATH\_INFO.  
Configuration de cherokee
-------------------------

La configuration de cherokee est ultra-basique. J'ai un v-servers pour l'ensemble des blogs hébergés.  
Des copies d'écran étant souvent plus parlantes que de longs discours, voici ma configuration :   
  
### Configuration générale du v-server

[![](https://franek.chicour.net/public/cherokee/.cherokee_configuration_basics_m.jpg "cherokee_configuration_basics.png, mai 2010")](https://franek.chicour.net/public/cherokee/cherokee_configuration_basics.png)  
  
### Configuration des behaviors

  
Il est nécessaire d'ajouter au mininum 3 behaviors :   
- Un behavior PHP (afin de pouvoir traiter les requêtes PHP)
- Un behavior admin permettant d'accéder à l'interface d'administration. Le behavor sur le répertoire admin pointe sur /usr/share/dotclear2/admin.
- Modifier le behavior "Par défaut" afin qu'il agisse en tant que redirection vers le fichier index.php (gestion des URL en mode PATH\_INFO, suppression de index.php)

  
[![](https://franek.chicour.net/public/cherokee/.cherokee_configuration_behavior_m.jpg "cherokee_configuration_behavior.png, mai 2010")](https://franek.chicour.net/public/cherokee/cherokee_configuration_behavior.png)  
  
### Configuration du Behavior par défaut

  
Cette configuration est nécessaire si vous souhaitez supprimer le fichier index.php dans les URL et que vous utilisez le mode PATH\_INFO.  
  
[![](https://franek.chicour.net/public/cherokee/.cherokee_configuration_redirection_m.jpg "cherokee_configuration_redirection.png, mai 2010")](https://franek.chicour.net/public/cherokee/cherokee_configuration_redirection.png)  
  
Je n'ai pas encore configuré cherokee afin qu'il gère correctement le cache des contenus statiques (ajout de date d'expiration,...). Si ce n'est pas clair, n'hésitez pas à commenter, j'essaierai de compléter.  
  
