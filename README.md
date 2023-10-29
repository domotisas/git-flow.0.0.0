# Gitflow

> By [Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/) Ce modèle a été conçu en 2010, il y a maintenant plus de 10 ans, et peu de temps après la création de Git lui-même. Au cours de ces 10 années, git-flow (le modèle de branchement présenté dans cet article) est devenu extrêmement populaire dans de nombreuses équipes de logiciels, au point que les gens ont commencé à le traiter comme une sorte de standard – mais malheureusement aussi comme un dogme ou une panacée. 

## Diagram

![diagram gitflow](./images/git-model@2x.png)


## Liste des branches

> 2 branches persistantes [master, develop], 3 branches temporaires [hotfix, features, releases]

| persistantes | temporaires |
| ------------ | ----------- |
| master       | hotfix: ```hotfix/FIX-<ticket>``` |
| develop      | features: ```features/WEB-<ticket>```| 
|              | releases: ```releases/v.<major.minor.patch>``` |

## master

> La branche master corresponds au miroir de la production.

- On ne développe pas directement sur master
- Elle contient l’historique officiel des versions
- Un tag est créé lors de chaque livraison d’une version

## hotfix

> Les branches hotfix sont utilisées pour corriger rapidement des problèmes critiques dans la branche de production : **master**.

1. On part de la branche master. Le nom de la branche hotfix doit commencer par "hotfix/" suivi du numéro de ticket correspondant à la correction.
1. On corrige le bug.
1. On merge dans master et develop.
1. On supprime la branche.

## develop

> La branche develop corresponds au miroir de l'environnement de preprode (pré-production).

- On ne développe pas directement sur develop
- Elle contient l’historique officiel des versions
- Un tag est créé lors de chaque livraison d’une version

## features

> Les branches features sont utilisées pour développer de nouvelles fonctionnalités pour la prochaine ou les prochaines versions.

1. On part de la branche develop. Le nom de la branche feature doit commencer par **"features/"** suivi du numéro de ticket correspondant à la fonctionnalité.  
```git switch develop && git pull && git switch -c feature/<numéro-de-ticket>```
1. On développe la fonctionnalité.
1. On merge dans develop. Il est généralement recommandé de **fusionner les branches features dans la branche develop**, plutôt que dans la release qui est spécifique. Cela permet de s'assurer que toutes les fonctionnalités sont testées et validées avant d'être incluses dans une release.  
    > Deux solutions de fusion. Le squash est préférable. Toutefois il préférable de garder une trace des étapes du développement de la feature et de pouvoir revenir en arrière si besoin.
    1. merge --no-ff conserve les ci
      - ```git switch develop && git pull && git merge --no-ff feature/<numéro-de-ticket>```
    2. merge --squash tous les ci fusionnés en un seul.
      - ```git switch develop && git pull && git merge --squash features/<numéro-de-ticket> &&  git commit -m "Merge branch 'feature/<numéro-de-ticket' into develop. Ticket Jira : <en-deux-mots-le-sujet>"```
1. On supprime la branche.

## releases

> Les branches releases sont utilisées pour préparer une nouvelle version de production.

1. On part de la branche develop. Le nom de la branche release doit commencer par **"releases/v."** suivi du numéro de version.  
```git switch develop && git pull && git switch -c releases/v.<major.minor.patch>```
1. Mise en preprode. On corrige les bugs.
1. On merge dans master et develop.

## vocabulaire

- ci - commit
- VCS - Version Control System
- CVS - old centralized version control system, while Git is distributed (VCS).
