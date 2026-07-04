# Catalogue de services - Template

> Une plateforme n'a de valeur que si les équipes savent comment l'utiliser sans dépendre d'un
> héros disponible au bon moment. Ce template rend l'offre plateforme lisible en une page.

## Pourquoi un catalogue, et pas juste de la documentation technique

La documentation technique explique **comment** utiliser un service une fois qu'on sait qu'il
existe. Le catalogue répond à une question plus en amont : **quelles offres existent, pour qui,
avec quels prérequis, et qui est responsable après la mise en service.** Sans ça, une équipe qui
a un besoin ne sait même pas si la plateforme le couvre déjà.

## Le template - une fiche par service

```
## [Nom du service]

**Ce que ça couvre** : (1-2 phrases, en langage métier, pas technique)

**Pour qui** : (type d'équipe / cas d'usage type)

**Prérequis pour en bénéficier** :
- Prérequis 1
- Prérequis 2

**Comment y accéder** : (lien vers le formulaire / processus de demande -
voir gouvernance-des-demandes.md)

**Délai indicatif** : (ex : self-service immédiat / 2 jours / 1 semaine)

**Qui est responsable après la mise en service** :
- Plateforme : [ce qui reste de leur ressort]
- Équipe demandeuse : [ce qui devient de son ressort]
- (voir raci-plateforme.md pour le détail)

**Limites connues** : (ce que le service ne couvre pas, pour éviter les
attentes mal calibrées)
```

## Exemple rempli - Provisioning de namespace

```
## Provisioning de namespace applicatif

**Ce que ça couvre** : mise à disposition d'un espace isolé sur le cluster
partagé, avec quotas par défaut et politiques de sécurité de base.

**Pour qui** : toute équipe applicative ayant validé son architecture avec
la plateforme.

**Prérequis** :
- Architecture applicative revue avec un référent plateforme
- Estimation de charge (CPU/mémoire) fournie

**Comment y accéder** : formulaire de demande standard.

**Délai indicatif** : 2 jours ouvrés.

**Qui est responsable après la mise en service** :
- Plateforme : disponibilité du cluster, quotas, politiques réseau de base
- Équipe demandeuse : usage dans les quotas, sécurité applicative,
  instrumentation de ses propres alertes

**Limites connues** : ne couvre pas le dimensionnement au-delà des quotas
standard - voir catégorie "Spécifique" dans gouvernance-des-demandes.md.
```

## L'erreur à éviter en construisant ce catalogue

Vouloir tout documenter d'un coup. Un catalogue incomplet mais à jour est plus utile qu'un
catalogue exhaustif mais figé depuis six mois. La bonne pratique : démarrer avec les 3 à 5 services
les plus demandés, et ajouter une fiche uniquement quand une demande répétée le justifie - pas de
façon anticipative et théorique.

## Le test pour savoir si le catalogue fonctionne

Une nouvelle équipe qui rejoint le périmètre de la plateforme doit pouvoir répondre seule, à partir
du catalogue, à la question : *"Est-ce que mon besoin est déjà couvert, et si oui par où je
commence ?"* - sans avoir besoin de connaître quelqu'un dans l'équipe plateforme pour le savoir.

---
*Extrait du K8s Platform Governance Lab - [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
