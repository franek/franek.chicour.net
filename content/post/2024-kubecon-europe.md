---
title: "Retour sur la KubeCon et CLoudNativeCon Europe 2024"
date: 2024-03-31T11:34:13+01:00
cover:
    image: "/public/kubecon-2024/entrance.jpg"
    alt: "Entrée de la Kubeconf"
    caption: "Entrée de la Kubeconf"
    relative: false
tags: ["Kubernetes", "CNCF", "conférence"]
---

Grâce à mon gentil [employeur](https://www.arte.tv/), j'ai participé pour la première fois à la [KubeCon + CloudNativeCon + other CNCF Events Europe](https://events.linuxfoundation.org/kubecon-cloudnativecon-europe/). Cette édition avait lieu à Paris à Porte de Versailles.

Cette conférence est dédiée à l'écosystème Kubernetes et aux projets incubés auprès de la [CNCF](https://www.cncf.io/) (Cloud Native and Computing Foundation). On retrouve au sein de la CNCF des projets comme bien entendu Kubernetes mais également Prometheus, OpenTelemetry, OpenFeature, Backstage, Keda, Helm, ... (et [bien d'autres](https://landscape.cncf.io/))

Cette édition était découpée en 4 jours : 
* une première journée dédiée aux projets de la CNCF "colocated events": il y avait beaucoup moins de monde, c'était principalement une journée dédiée aux *mainteneurs* des projets incubées par la CNCF. C'était un bon moyen de découvrir les lieux et comprendre comment l'évènement aller fonctionner.
* trois grosses journées qui sont vraiment le coeur de l'évènement avec des keynotes de 2h, un étage dédié avec les stands de tous les gros acteurs et des conférences thématiques.

Cette année, les organisateurs ont annoncé qu'il y avait **12 000 personnes**. Par le passé, j'ai beaucoup participé aux conférences "[Forum PHP](https://event.afup.org/forum-php-2023/)" ou "[Paris Web](https://www.paris-web.fr/)" que je trouvais déjà assez importantes en nombre de visiteurs. Cet évènement ne joue clairement pas dans la même catégorie. Retrouver les copains après chaque conférence est extrêmement difficile.

La Kubecon Europe tourne entre les différents pays européens (Valence en Espagne l'an passé, Amsterdam aux Pays-Bas l'année précédente). L'évènement est donc beaucoup plus cosmopolitain. Toutes les conférences sont en anglais et dans les couloirs, on croise énorméments d'Américains, d'Espagnols, d'Allemands, d'Anglais, ... Les Français sont au final assez peu représentés (20% peut-être ?).

Durant les 3 jours principaux, il y a parfois une dizaine de tracks en parallèle.  Je n'ai toujours pas le don d'ubiquité et c'est parfois extrêmement difficile de faire le bon choix. Dans d'autres cas, en raison du monde, c'est frustrant de ne pas pouvoir assister à la conférence que l'on souhaite absolument voir.

Un des intérêts majeurs de l'évènement est à mon sens de valider les solutions techniques du moment. Actuellement, mes sujets du moment tournent autour de Kubernetes, OpenTelemetry, Prometheus, OpenFeature, Backstage, Keda, ... Ces technos étaient assez bien representées, elles semblent être validées par la communauté et c'est plutôt rassurant.

Certaines équipes ne souhaitent pas comprendre comment fonctionne Kubernetes, ils veulent simplement déployer leurs applications. Une de mes missions est d'abstraire cette complexité en donnant accès à des abstractions. Spotify expliquait bien tout cela [lors d'une très belle conférence](https://www.youtube.com/watch?v=Iw5Tox2H87A). 

![](/public/kubecon-2024/spotify.jpg)


Je ne ferai pas de compte-rendu de toutes les conférences que j'ai pu voir. Les [replays](https://www.youtube.com/@cncf/playlists) sont déjà disponibles.

Quelques outils ou remarques qui ont attirés mon attention :
* Bientôt la SNCF fera tourner des clusters Kubernetes dans leur train grâce à [k3s](https://k3s.io/) ![](/public/kubecon-2024/sncf.jpg)



* [k8s-shredder](http://opensource.adobe.com/k8s-shredder/) développé par Adobe qui implémente la notion de "Parked" node
* WebAssembly semble vraiment une techno à suivre et nous pourrons bientôt faire tourner du WebAssembly dans nos clusters Kubernetes grâce par exemple à [SpinKube](https://www.spinkube.dev/)
* En terme de sécurité des clusters k8s, [Kyverno](https://kyverno.io/) et [Falco](https://falco.org/) sont des outils à suivre/expérimenter. Kyverno va permettre d'appliquer des politiques de sécurité sur le cluster. Falco va permettre de détecter des problèmes de sécurité.
* Une solution de Load Balancer de haut-niveau "A cloud native Kubernetes Global Balancer" est en train de voir le jour grâce à [k8gb](https://www.k8gb.io/docs/) qui peut interagir avec nombreuses solutions DNS (Route53, Cloudflare, Azure, ....)
* [APIClarity](https://www.apiclarity.io/), un outil développé par CISCO, qui  permet de génerer une spec OpenAPI à partir du trafic détecté au niveau du cluster.
* [OpenFGA](https://openfga.dev/), pour rendre agnostique la gestion des autorisations et des permissions au niveau du cluster
* [Karmada](https://karmada.io/), un projet à suivre pour faire du multi-clusters/multi-clouds
* [Slim](https://github.com/slimtoolkit/slim), pour réduire la taille d'une image Docker
* Le hashtag #IA était bien entendu présent. [Kubeflow](https://www.kubeflow.org/) semble être la solution qui sort du lot pour faire touner des traitements d'intelligence artificielle.
* En solution alternative à Backstage, [OpsLevel](https://www.opslevel.com/) semble chouette. J'ai également découvert que des sociétés proposaient du BackStage managé: [Roadie](https://roadie.io/)
* ... (et plein d'autres choses qu'il est difficile de résumer dans cet article)

Pour conclure, j'ai passé un super moment. Ce fut aussi l'occasion de sortir de mon quotidien et de voir d'autres choses. Je recommande ;)

Si vous souhaitez en savoir plus sur l'évènement, d'autres personnes ont été beaucoup plus prolixes que moi : 
* L'inarrêtabble [Zwindler](https://blog.zwindler.fr/2024/03/19/kubecon-eu-2024-mardi-colocated/)
* [Rémi Verchère](https://www.vrchr.fr/posts/2024/2024-03-24-kubecon-eu/)
* [cockpit.io](https://blog.cockpitio.com/events/kubecon-eu-paris-2024/)
* ...
