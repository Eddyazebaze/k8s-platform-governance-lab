# RACI Plateforme : Offre Kubernetes

> Modèle type, issu du pilotage d'une offre Kubernetes critique (secteur énergie, on-prem + AWS).
> Anonymisé et réutilisable pour toute plateforme interne (cloud, data, IA).

## Pourquoi ce document

Sur une plateforme partagée, la première source de friction n'est presque jamais technique :
c'est l'absence de réponse claire à trois questions simples, **qui décide, qui exécute, qui est informé**.
Ce RACI couvre les 4 flux qui, sur le terrain, concentrent le plus d'ambiguïté.

| Lettre | Anglais | Français |
|---|---|---|
| **R** | Responsible | **Réalisateur**, exécute la tâche, sous la direction d'un A. Chaque ligne a au moins un R. |
| **A** | Accountable | **Approbateur**, rend des comptes, valide en dernier ressort. C'est le véritable responsable, un seul par ligne. |
| **C** | Consulted | **Consulté**, expert sollicité avant décision ; l'A reste libre de suivre son avis ou non. |
| **I** | Informed | **Informé**, tenu au courant après décision, même sans intervenir directement. |

> Le piège classique : traduire *Responsible* par "responsable" en français. C'est trompeur, le
> véritable responsable au sens décisionnel est l'**Approbateur (A)**, pas le Réalisateur (R).

---

## 1. Demandes d'accès / provisioning

| Activité | Équipe plateforme | Équipe demandeuse | Sécurité/RSSI | Manager plateforme |
|---|---|---|---|---|
| Soumettre une demande de namespace/cluster | I | R | I | I |
| Valider la conformité de la demande | C | I | R | A |
| Provisionner les ressources | R | I | I | A |
| Notifier la mise à disposition | R | I | I | I |

## 2. Mise en production (MEP)

| Activité | Équipe plateforme | Équipe applicative | Sécurité/RSSI | Manager plateforme |
|---|---|---|---|---|
| Préparer le déploiement | C | R | I | I |
| Valider les critères de sécurité (scan image, secrets, policies) | C | R | A | I |
| Autoriser le passage en production | I | C | C | A |
| Exécuter le déploiement | R | C | I | I |
| Rollback en cas d'incident | R | C | I | A |

## 3. Gestion des incidents

| Activité | Équipe plateforme | Équipe applicative | Sécurité/RSSI | Manager plateforme |
|---|---|---|---|---|
| Détecter l'incident (alerting) | R | I | I | I |
| Qualifier la sévérité | R | C | C | A |
| Résoudre l'incident (niveau plateforme) | R | I | I | A |
| Résoudre l'incident (niveau applicatif) | C | R | I | I |
| Post-mortem / capitalisation | R | R | C | A |

## 4. Certificats & secrets

| Activité | Équipe plateforme | Équipe applicative | Sécurité/RSSI | Manager plateforme |
|---|---|---|---|---|
| Émettre un certificat | R | I | I | I |
| Définir la politique de rotation | C | I | R | A |
| Détecter une expiration imminente | R | I | I | I |
| Renouveler / révoquer | R | C | A | I |

---

## Ce que ce RACI ne remplace pas

Un RACI figé sans revue devient obsolète en quelques mois. Deux règles d'usage :

- **Un seul Approbateur (A) par ligne.** Si deux équipes se disputent l'approbation, c'est le
  signal qu'une clarification managériale est nécessaire, pas une case à cocher.
- **Revue trimestrielle.** Les responsabilités évoluent avec la maturité de la plateforme
  (self-service croissant, nouvelles équipes consommatrices). Un RACI non révisé masque les
  dérives plutôt qu'il ne les prévient.

Il n'est pas rare qu'une même personne cumule plusieurs rôles sur une même activité (par exemple
A et R), elle est alors son propre approbateur sur cette tâche, ce qui est acceptable tant que
ça reste l'exception, pas la norme sur les activités à enjeu.

---
*Extrait du K8s Platform Governance Lab : [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
