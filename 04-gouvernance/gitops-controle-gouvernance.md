# GitOps comme contrôle de gouvernance - pas seulement un pipeline

> Angle : un pipeline CI/CD GitOps (Jenkins + Argo CD) n'est pas qu'un mécanisme de déploiement.
> Bien conçu, c'est un contrôle d'auditabilité au sens NIS2/DORA. Ce document explique pourquoi,
> sans Jenkinsfile ni YAML - c'est un sujet de gouvernance, pas un tutoriel.

## Le principe qui change tout

Dans une architecture GitOps, le dépôt Git des manifestes devient **la seule source de vérité**
de l'état attendu du cluster. Un contrôleur (type Argo CD) compare en continu cet état déclaré à
l'état réel, et corrige automatiquement tout écart (auto-remédiation).

Techniquement, c'est un mécanisme de synchronisation. Du point de vue gouvernance, c'est bien plus :
**toute modification manuelle en production devient une anomalie détectable, tracée et réversible
sans intervention humaine.**

## Pourquoi c'est exactement ce qu'un audit demande

Un audit NIS2 ou DORA pose rarement la question "avez-vous un pipeline de déploiement ?". Il pose :
*qui a changé quoi, quand, avec quelle validation, et pouvez-vous le prouver ?*

GitOps répond structurellement à cette question :

| Question d'audit | Réponse GitOps |
|---|---|
| Qui a autorisé ce changement ? | L'historique Git (commit, auteur, revue de PR) |
| Quand a-t-il été appliqué ? | Horodatage de synchronisation du contrôleur |
| L'état réel correspond-il à l'état déclaré ? | Détection de dérive automatique et continue |
| Un changement non autorisé a-t-il eu lieu ? | Toute modification hors Git est écrasée et journalisée |

Aucune de ces réponses ne nécessite un registre manuel tenu à jour par une équipe - c'est la
différence entre une conformité **déclarative** (un document qui dit qu'on respecte la règle) et
une conformité **structurelle** (une architecture qui rend la non-conformité difficile à produire
silencieusement).

## Le piège à éviter

GitOps ne garantit l'auditabilité que si une discipline minimale est respectée : aucun accès
`kubectl` direct en production pour modifier un état durable, et toute exception documentée comme
telle. Une équipe qui contourne le contrôleur "pour aller vite" recrée exactement le problème que
GitOps est censé résoudre - juste de façon moins visible.

## Ce que ça change pour un platform owner

La question à poser n'est plus "avons-nous automatisé le déploiement ?" mais **"notre pipeline
peut-il répondre à un auditeur sans préparation ?"**. Si la réponse nécessite de rassembler des
logs de plusieurs outils différents, l'architecture GitOps n'est pas encore un contrôle de
gouvernance - c'est encore juste un pipeline.

---
*Extrait du K8s Platform Governance Lab - [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
