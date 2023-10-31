---
title: "Cloud Nord 2023"
date: 2023-10-31T21:34:13+01:00
cover:
    image: "/public/engin-akyurt-A9_IsUtjHm4-unsplash.jpg"
    alt: "Nuage dans ciel bleu"
    caption: "source: https://unsplash.com/fr/photos/nuvole-bianche-e-cielo-blu-durante-il-giorno-A9_IsUtjHm4"
    relative: false
tags: ["Cloud Nord", "Lille", "conférence"]
---

[Cloud Nord](https://www.cloudnord.fr/) est une journée de conférence dédiée aux Clouds et outils associés (culture devops).

Ce cycle de conférences a lieu tous les ans à Lille sur le site d’Euratechnologie, un incubateur de start-ups. C’est une conférence organisée par des bénévoles et soutenu par de nombreux partenaires (Les Tilleuls, OPEN, Ippon Technologie, …).

4 tracks ont lieu au même moment. N’ayant pas le don d’ubiquité, je n’ai pu participer qu'à une partie infime des conférences. C’est parti pour une petite synthèse.

# Laissez tomber vos Dockerfile, adoptez un buildpack !

[Julien Wittouck](https://juwit.github.io/) ([slides](https://juwit.github.io/talks/cloudnord2023-talk-laissez-tomber-vos-dockerfile-adoptez-un-buildpack.pdf)) nous a présenté [buildpacks](https://buildpacks.io/), une technologie, initialement développée par Heroku, qui a été offerte à la communauté. Depuis peu, elle a rejoint la Cloud Native Computing Foundation (CNCF).

Buildpacks est utilisé par la plupart des Cloud Providers (GCP pour son Google App Engine ou son Cloud Function, Scalingo, Azure, …) afin d’accélérer le déploiement d’applications.

Le principe de Buildpacks est à partir d’un dossier contenant les sources d’un projet (PHP, NodeJS, Java, …), Buildpacks va détecter la technologie du projet et créer une image Docker optimisée avec les sources du projet.

Les recettes de Buildpacks (les scripts qui permettent de construire les images) sont publiques.
Lors de la création d’une image Docker en utilisant Buildpacks, vous spécifiez le répertoire contenant les sources, la bibliothèque de builder que vous souhaitez utiliser, éventuellement des options de configuration et c’est parti…

Un ensemble de builders de confiance est disponible : 

```
> pack config trusted-builders list
Fix config to .config ? [y:Yes, n:No, a:Abord, e:Edit]n
Trusted Builders:
  gcr.io/buildpacks/builder:v1
  heroku/builder:22
  heroku/buildpacks:20
  paketobuildpacks/builder-jammy-base
  paketobuildpacks/builder-jammy-buildpackless-static
  paketobuildpacks/builder-jammy-full
  paketobuildpacks/builder-jammy-tiny 
```

Tous les builders ne supportent pas toutes les technologies. En fonction de votre projet, vous allez choisir l’un ou l’autre des builders. Les builders sont maintenus pas la communauté. Un des plus connus est Paketo : https://github.com/paketo-buildpacks

L’intérêt de Buildpacks est de ne plus avoir à supporter des Dockerfiles dans les différents projets. Ces Dockerfiles sont souvent copiés-collés d’un projet à l’autre et la qualité n’est pas toujours à la hauteur (écrire un Dockerfile optimisé respectant les bonnes pratiques de sécurité n’est toujours trivial).

Buildpacks va permettre d’unifier la configuration des images sur l’ensemble des projets,  en se basant sur une configuration qui a déjà été éprouvée par d’autres.

Buildpacks va également permettre de générer un fichier SBOM (Software Bill of Materials). Le SBOM est un format standardisé permettant de décrire l’ensemble des composants logiciels présents dans un système. Dans le cadre de la mise en place d’une politique de sécurité, ces SBOM pourraient être utilisés pour générer une base de données de l’ensemble des composants et leurs versions d’un SI. On verra plus tard que c’est utilisé par plein d’autres projets.

# Continuous Container Checkup - Et si on regardait ce qu'il y a dans nos conteneurs ?

Louis et Vincent sont 2 développeurs Go travaillant pour Ubisoft.

Ils nous ont présenté l’outil Continous Container Checker qu’ils ont développé en interne et envisagent de rendre open-source.

Cet outil alimenté à partir d’un export SBOM de leurs containers va permettre de visualiser les containers qui contiennent des failles de sécurité au niveau des logiciels, comme des dépendances ou de l'OS.

Le SBOM du container est généré à partir de syft : https://github.com/anchore/syft

La détection des failles de sécurité s’appuie sur grype: https://github.com/anchore/grype

L’ensemble des informations sont stockées dans un Prometheus et enrichis via des APIs ouvertes comme https://endoflife.date/, par exemple.

# Démystifions les composants internes de Kubernetes

Denis Germain, Senior SRE chez Deezer, nous accompagne pas à pas dans l’installation d’un cluster k8s afin de mieux nous faire comprendre les rouages d’un cluster. C’est super pédagogique et on apprend plein de choses.

Les slides : https://blog.zwindler.fr/talks/2023-demystifions-kubernetes/index.html

# ZenML, le dagger.io des pipelines ML !

François Serra d’ADEO (Leroy Merlin) nous entraine dans une présentation rapide du framework ZenML. [ZenML](https://www.zenml.io/home) est un framework écrit en python permettant de simplifier la mise à l'échelle d’une pipeline de Marchine Learning. On pourra facilement passer de l’exécution d’un pipeline sur le poste du développeur à une pipeline plus robuste chez les principaux Cloud Providers ou sur un cluster Kubernetes. 

Je ne fais pas de Machine Learning mais la présentation de ZenML donne envie de l’essayer.

# It works on my machine

Edouard Cattez nous fait un retour d’expérience sur [Dagger.io](dagger.io), un framework développé par des anciens de Docker permettant d’écrire ces scripts de CI/CD “As Code”.

L’intérêt est ensuite de pouvoir exécuter sa CI en local ou dans Gitlab/Github Actions.

# Buildez vos images OCI correctement avec un meta build system

Nicolas Bernard travaille pour [S3NS](https://www.s3ns.io/), une joint-venture développée par Thales et Google visant à lancer une solution de Cloud Confiance en France basée sur les technologies de Google (GCP).

Après une petite introduction aux outils de meta build system (Make, Bazel, Buck), Nicolas présente Nix, une solution qui a le vent en poupe permettant de décrire via des scripts Nix son environnement. 

C’est particulièrement intéressant pour reproduire des environnements identiques sur un poste de développement par exemple. A l’arrivée d’un nouveau collègue, on transmet le fichier install.nix et on est certain que le nouveau aura les bonnes versions des différents logiciels.

A nouveau, à partir de Nix, il sera possible de générer un SBOM (le terme SBOM était définitivement à la mode cette année).

[Nix](https://nixos.org/) est installable sous Linux comme sous MacOS. Il existe également une distribution NixOS.

# Conclusion

Je n'ai résumé succinctement qu'une partie des conférences.
Sur le fond, Cloud Nord a totalement rempli ses objectifs. La qualité des interventions et le choix des sujets étaient tops.
Sur la forme, des progrès sont encore à réaliser pour rivaliser avec le Forum PHP, Paris Web ou d'autres conférences. Par exemple: 
* je trouve dommage que les speakers ne soient pas introduits au début de chaque conférence, 
* il manquait des badges avec le nom des participants. 
* A la fin de la dernière conférence, on aurait pu s'attendre à un remerciement pour les sponsors et les bénévoles. 
* ...

Des détails qui pourraient améliorer la qualité de l'évènement mais qui restent secondaires si la sélection des intervenants reste de bonne facture. A l'année prochaine.
