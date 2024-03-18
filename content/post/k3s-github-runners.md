---
title: "Faire tourner des runners GitHub sur k3s"
date: 2024-02-21T12:34:13+01:00
cover:
#    image: "/public/engin-akyurt-A9_IsUtjHm4-unsplash.jpg"
    alt: "Nuage dans ciel bleu"
    caption: "source: https://unsplash.com/fr/photos/nuvole-bianche-e-cielo-blu-durante-il-giorno-A9_IsUtjHm4"
    relative: false
tags: ["GitHub", "self-hosted", "runners", "kubernetes"]
---

GitHub Actions permet l'exécution de workflow de développement logiciel automatisé dans votre référentiel de code (`repository`). Vous allez pouvoir exécuter différents workflows (exécution de tests unitaires ou fonctionnels, déploiement, ...).
Un workflow Github Actions est un fichier YAML à placer dans le répertoire `.github/workflows` de votre dépôt GitHub et ressemble à ça : 

```
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v4
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```
(source: https://docs.github.com/fr/actions/quickstart)

Par défaut, les workflows vont être exécutés sur des `runners` (/des serveurs) qui sont gérés par GitHub. Dans l'exemple ci-dessus, GitHub nous met à dispo une machine `ubuntu` pour exécuter nos jobs.

Pour les dépôts publics, l'exécution de workflow est gratuite.

Si tous vos projets sont publics ou open-source, a priori, jusque là tout se passe bien. 

Si vos projets sont privés, GitHub vous alloue un certain nombre de minutes en fonction de votre abonnement.

Si GitHub est utilisé au sein de votre entreprise, vous avez sûrement un abonnement associé à une organisation. 
Dans l'entreprise où je travaille, GitHub nous alloue 50 000 minutes par mois.

Parfois, vous avez également besoin que vos runners puissent accéder à votre infrastructure. Vous pourriez autoriser les IPs de l'infrastructure de GitHub à accéder à votre infrastructure. Je ne vous le recommande pas... 

La solution préconisée par GitHub est d'exécuter des runners GitHub dans votre infrastructure. On parle de `self-hosted runners`.

Pour faire tourner des `self-hosted runners`, GitHub propose différentes approches.
L'approche la plus simple est de dédier une VM à cet usage et installer l'outillage de GitHub afin que votre VM devienne un `self-hosted runner`. C'est assez rapide à faire.

Vous installez une VM et vous lancer l'installation des outils de GitHub. C'est assez bien documenté. Rapidement, cela consiste en l'exécution de cette commande:

``` 
./config.sh --url https://github.com/octo-org --token example-token 
```

Pour exécuter le job sur ce self-hosted runner, vous devriez modifier votre workflow en mettant quelque chose ressemblant à : 

``` 
runs-on: self-hosted
``` 

Cette approche est rapide à mettre en oeuvre mais elle a quelques inconvénients: 

* Lors de l'exécution d'un job GitHub sur un self-hosted runner, vous n'avez pas les droits pour installer des outils. Une solution sera de Dockeriser toutes les commandes.
* Entre l'exécution de 2 jobs, les fichiers créés par le premier job ne sont pas nécessairement supprimés. Il y a un risque de sécurité. Une solution est de mettre en place un job de nettoyage à la fin de vos workflows.
* Entre l'exécution de 2 jobs, des process peuvent rester résidents. Comme pour  le point précédent, une solution est de mettre en place un de job de nettoyage à la fin de vos workflows.

Une autre solution est d'installer les runners en mode "ephemeral" : 

```
./config.sh --url https://github.com/octo-org --token example-token --ephemeral
```

> The GitHub Actions service will then automatically de-register the runner after it has processed one job. You can then create your own automation that wipes the runner after it has been de-registered.

Néanmoins, c'est à vous de mettre en place le mécanisme de nettoyage. Il ne sera pas mis en place par défaut.

Un autre point est que la DX (Developer eXperience) n'est pas du tout la même entre un job tournant sur des runners GitHub et des self-hosted runners. Sur un runner GitHub, vous avez la possibilité d'installer des outils manquants via le gestionnaire des paquets. Sur un `self-hosted runner`, cela ne sera pas possible. Dans la plupart des cas, la solution que vous retiendrez est de containeriser votre application.

J'aimerais vous proposer une solution qui permettra de palier aux problèmes mentionnés plus hauts.

## Faire tourner vos self-hosted runner dans k3s

GitHub proposer de faire tourner vos runners GitHub dans un cluster Kubernetes (https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller).




