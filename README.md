# K8s Platform Governance Lab

Ce lab rassemble des démonstrateurs Kubernetes concrets et des artefacts de gouvernance issus
du pilotage d'une offre Kubernetes critique en production (secteur énergie, on-prem + AWS).
Une plateforme techniquement robuste peut rester organisationnellement fragile : ce lab traite
les deux dimensions : **rendre Kubernetes concret, et le rendre gouvernable, auditable et adoptable.**

Maintenu par [Eddy Azebaze](https://github.com/Eddyazebaze), Product Owner d'une offre Kubernetes
critique. Tous les artefacts de gouvernance sont anonymisés et réutilisables pour toute plateforme
interne (cloud, data, IA).

---

## 🎯 À qui s'adresse ce lab

- **DSI / managers / responsables plateformes** : comprendre Kubernetes sans jargon, et savoir
  comment le gouverner
- **Platform leaders / PO plateforme** : structurer l'offre et les responsabilités
- **RSSI / risques** : traduire NIS2 et DORA en pratiques opérationnelles sur K8s
- **Équipes projets / chefs de projet / PMO** : comprendre comment consommer une plateforme
  interne proprement

---

## 📂 Contenu

### 1. [`01-visual-explorer/`](https://github.com/Eddyazebaze/kubernetes-lab-by-eddy/tree/main/01-visual-explorer) : Comprendre Kubernetes visuellement
Démo interactive orientée DSI/managers : Control Plane vs Workers, composants cliquables,
sans prérequis technique. [Voir la démo](https://eddyazebaze.github.io/kubernetes-lab-by-eddy/01-visual-explorer/)

### 2. [`02-bootcamp/`](https://github.com/Eddyazebaze/kubernetes-lab-by-eddy/tree/main/02-bootcamp) : Bootcamp Kubernetes (1 jour)
Programme, checklist et notes de montée en compétences : installer un cluster local, déployer
une app simple, comprendre namespaces/RBAC/NetworkPolicies.

### 3. [`03-manifests/`](https://github.com/Eddyazebaze/kubernetes-lab-by-eddy/tree/main/03-manifests) : Manifests réutilisables
Base de manifests prêts à l'emploi : namespaces (dev/prod/monitoring), RBAC (roles/rolebindings),
NetworkPolicies (segmentation et sécurité).

### 4. [`04-gouvernance/`](https://github.com/Eddyazebaze/kubernetes-lab-by-eddy/tree/main/04-gouvernance) : Qui décide quoi
| Artefact | Description |
|---|---|
| `raci-plateforme.md` | RACI type d'une plateforme K8s : demandes, MEP, incidents, certificats, alerting |
| `build-vs-run.md` | Le point de friction n°1 des plateformes internes : modèle de répartition + pièges observés |
| `gitops-controle-gouvernance.md` | Pourquoi GitOps est un contrôle d'auditabilité, pas seulement un pipeline |
| `gouvernance-des-demandes.md` | Processus d'onboarding et d'arbitrage des demandes projets |
| `catalogue-de-services.md` | Template de catalogue : offre lisible, prérequis, délais, responsabilités post-MEP |

### 5. [`05-reseau-et-multi-tenancy/`](https://github.com/Eddyazebaze/kubernetes-lab-by-eddy/tree/main/05-reseau-et-multi-tenancy) : Gouvernance réseau partagé
| Artefact | Description |
|---|---|
| `gateway-api-gouvernance.md` | Qui gouverne le routage et l'exposition réseau sur une plateforme mutualisée |

### 6. [`06-ia-plateforme/`](https://github.com/Eddyazebaze/kubernetes-lab-by-eddy/tree/main/06-ia-plateforme) : Gouverner l'IA en production
| Artefact | Description |
|---|---|
| `vllm-gouvernance-ia.md` | Qui valide, qui paie, qui trace un déploiement de modèle IA sur une plateforme partagée |

---

## 🧭 Le fil conducteur

Les organisations n'ont pas seulement besoin de plus de technologie. Elles ont besoin de
plateformes qu'elles peuvent **comprendre, gouverner, auditer et faire évoluer**. Ce lab illustre
les deux moitiés de cette phrase : la partie technique (dossiers 1-3) et la partie gouvernance
(dossiers 4-6), issues du même terrain.

---

Projet Augmenté® : Eddy AZEBAZE (PMP®, CISM®)
[LinkedIn](https://linkedin.com/in/eddy-azebaze-pmp-cism) · [Prendre 30 min](https://calendly.com/eddy-azebaze-proton/30min)
# kubernetes-lab-by-eddy
Rendre Kubernetes concret : démos interactives, manifests essentiels, guides terrain. Projet Augmenté®
