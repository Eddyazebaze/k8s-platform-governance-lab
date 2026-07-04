# Déployer un LLM en production : le vrai sujet est la gouvernance, pas le modèle

> Angle : déployer un LLM (type vLLM) sur une plateforme Kubernetes est un problème d'infrastructure
> bien documenté. Le gouverner en entreprise en est un autre, rarement traité. Ce document couvre
> les questions qui se posent une fois le déploiement technique résolu.

## Ce que la technique résout, et ce qu'elle ne résout pas

Des outils comme vLLM répondent bien à des questions d'infrastructure : comment servir un modèle à
l'échelle, comment gérer le batching des requêtes, comment dimensionner les GPU. Ce sont des
problèmes d'ingénierie, largement documentés.

Ce qu'ils ne répondent pas : **qui a le droit de déployer quel modèle, qui paie le coût GPU associé,
et comment prouver a posteriori qu'un usage était conforme.** Sur une plateforme partagée par
plusieurs équipes, ces questions se posent dès le premier cas d'usage IA en production — pas après.

## Les 4 questions de gouvernance à trancher avant la mise en production

**1. Qui valide le passage d'un POC IA à un déploiement de production ?**
Un POC qui fonctionne sur un notebook n'a pas les mêmes exigences (sécurité, disponibilité, coût)
qu'un service en production. Sans validation formelle à ce stade, le POC devient production par
glissement — et personne n'a évalué le risque.

**2. Qui porte le coût GPU d'un cas d'usage ?**
Un modèle déployé sans propriétaire budgétaire clair devient une ligne de coût invisible jusqu'à ce
qu'elle soit trop grosse pour être ignorée. La question FinOps doit être posée à la demande de
déploiement, pas à la facture trimestrielle.

**3. Peut-on tracer quelle version de modèle a produit quelle réponse, à quel moment ?**
C'est l'équivalent, côté IA, de l'auditabilité qu'on demande à un pipeline GitOps : sans traçabilité
version/date/entrée-sortie, il est impossible de répondre à un audit sur une décision assistée par
IA — ce qui devient une exigence croissante sous l'AI Act pour les usages à risque.

**4. Qui est informé quand un modèle est mis à jour ou remplacé ?**
Un changement de modèle peut changer le comportement d'un service sans changement de code
applicatif visible. Les équipes consommatrices doivent être informées comme elles le seraient
d'un changement d'API — pas découvrir la différence en production.

## La checklist minimale avant tout déploiement LLM sur une plateforme partagée

| Question | Répondu ? |
|---|---|
| Un propriétaire budgétaire du coût GPU est identifié | ☐ |
| Un processus de validation POC → production existe et est suivi | ☐ |
| La version du modèle et ses changements sont tracés | ☐ |
| Les équipes consommatrices sont notifiées des changements de modèle | ☐ |
| Une revue de conformité (AI Act, usage à risque) a eu lieu si applicable | ☐ |

## Le vrai enseignement

L'infrastructure IA (vLLM, GPU scheduling, autoscaling) est un sujet résolu par l'écosystème
Kubernetes/Cloud natif. Le sujet qui reste ouvert dans la plupart des organisations n'est pas
technique : c'est de savoir qui décide, qui paie, et qui peut prouver que l'usage était maîtrisé.
C'est exactement le sujet que l'IA en entreprise devient : **un sujet de plateforme, pas seulement
un sujet de modèle.**

---
*Extrait du K8s Platform Governance Lab — [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
