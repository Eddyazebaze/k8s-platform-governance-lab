# Build vs Run - Le point de friction n°1 des plateformes internes

> Modèle de répartition, zones grises et test de maturité, issu de retours terrain sur des plateformes Kubernetes en environnement contraint.

## Le constat

La majorité des tensions sur une plateforme partagée ne viennent pas d’un manque de compétence technique.

Elles viennent d’un partage Build / Run **implicite**.

Chaque équipe suppose que l’autre couvre une partie du service, jusqu’au jour où une alerte ou un incident révèle qu’aucun propriétaire n’était réellement identifié.

Un service n’est donc pas réellement passé en Run lorsque son statut change dans un outil ou qu’une réunion de transfert a eu lieu.

Il l’est lorsque son exploitation ne dépend plus exclusivement de la mémoire de ceux qui l’ont construit.

Le modèle ci-dessous constitue un point de départ. Il doit être adapté à l’organisation, mais le principe reste le même :

> Une responsabilité partagée doit être explicitée par activité, et non simplement attribuée à une équipe ou à un outil.

## Le modèle de répartition

| Sujet | Build - Équipe plateforme | Run - Équipe plateforme | Run - Équipe applicative |
|---|---|---|---|
| Infrastructure du cluster | Conçoit l’architecture, les standards et les mécanismes de provisioning | Exploite les nœuds, le réseau, le stockage et la capacité du cluster | N/A |
| Namespace et isolation logique | Définit les standards et automatise le provisioning | Administre les quotas, politiques et mécanismes d’isolation | Utilise le namespace conformément aux standards |
| CI/CD | Fournit les templates, contrôles et parcours de déploiement | Maintient les composants, templates et intégrations de la chaîne | Adapte le pipeline aux besoins de l’application |
| Observabilité | Met à disposition la stack et les standards d’instrumentation | Garantit la disponibilité, la capacité et la rétention de la stack | Instrumente l’application et maintient ses dashboards |
| Alerting | Fournit les mécanismes, conventions et règles types | Traite les alertes relatives à la plateforme | Définit et traite les alertes applicatives |
| Certificats et secrets | Met à disposition les mécanismes approuvés de gestion et de rotation | Exploite les composants et automatismes associés | Utilise correctement les mécanismes et reste responsable des secrets applicatifs |
| Scaling | Fournit les capacités et mécanismes de scaling | Garantit la capacité globale de la plateforme | Définit les ressources, seuils et règles de scaling de l’application |
| Sécurité des images | Met en place le scan automatisé et les politiques de conformité | Applique les contrôles et blocages définis | Corrige les vulnérabilités et maintient les images applicatives |
| Sauvegarde et restauration | Fournit les mécanismes et standards de sauvegarde | Exploite les composants techniques de sauvegarde | Définit les exigences RPO / RTO et valide les procédures de restauration |
| Incidents | Définit le circuit d’escalade et les interfaces entre équipes | Prend en charge les incidents liés à la plateforme | Prend en charge les incidents liés au comportement applicatif |
| Documentation et runbooks | Définit les modèles et exigences minimales | Maintient la documentation d’exploitation de la plateforme | Maintient les procédures propres à l’application |

## Les trois pièges les plus fréquents

### 1. L’alerting orphelin

Une alerte remonte, mais ni l’équipe plateforme ni l’équipe applicative ne sait clairement qui doit l’analyser en premier.

L’alerte est transférée, mise en attente ou ignorée jusqu’à ce qu’un incident confirme qu’elle était pertinente.

Le problème n’est généralement pas l’outil.

Le propriétaire a été défini par composant ou par équipe, mais pas par **type d’alerte**.

**La correction :**

- identifier un premier niveau de prise en charge pour chaque catégorie d’alerte ;
- définir les critères d’escalade ;
- documenter les actions attendues et les délais de réaction.

### 2. Le « ça marchait avant »

Une application dépend d’un quota, d’une Network Policy, d’un secret, d’un certificat ou d’un comportement particulier de la plateforme.

Cette dépendance est connue de quelques personnes, mais elle n’est pas formalisée.

Lorsqu’une configuration évolue ou qu’un changement applicatif intervient, chaque équipe considère que le problème relève de l’autre.

**La correction :**

Toute dépendance à une configuration ou à un service de la plateforme doit être :

- identifiée ;
- versionnée ;
- documentée côté applicatif ;
- testée avant la mise en production.

Une dépendance connue uniquement de mémoire constitue déjà une dette opérationnelle.

### 3. Le support qui devient du Run déguisé

L’équipe plateforme intervient ponctuellement pour aider une équipe applicative à résoudre un problème.

L’intervention est justifiée par l’urgence ou par la volonté d’aller vite.

Quelques mois plus tard, cette aide ponctuelle est devenue une activité récurrente, non formalisée, non dimensionnée et dépendante de quelques experts.

**La correction :**

Toute intervention récurrente doit être :

- formalisée dans le RACI ;
- intégrée à une offre de service ;
- automatisée ;
- ou réorientée vers de la documentation et du self-service.

Ce qui reste exceptionnel peut être traité comme du support.

Ce qui devient récurrent est déjà du Run.

## Le minimum à valider avant le go-live

Avant de considérer qu’un service est prêt à passer en Run, les réponses aux questions suivantes doivent être connues et partagées :

- Qui supervise le service ?
- Qui reçoit et qualifie chaque type d’alerte ?
- Qui prend en charge le premier diagnostic ?
- Qui décide d’un rollback ou d’une action de remédiation ?
- Qui corrige une vulnérabilité applicative ?
- Qui maintient les dashboards et les règles d’alerte ?
- Où se trouvent les logs et les runbooks ?
- Quel est le circuit d’escalade ?
- Les procédures de restauration ont-elles été testées ?
- Le service peut-il être exploité sans dépendre exclusivement de ceux qui l’ont construit ?

Une réponse écrite ne suffit pas.

Elle doit être comprise de la même manière par les équipes concernées.

## Le test simple

Posez la même question à trois personnes différentes :

- un membre de l’équipe plateforme ;
- un membre de l’équipe applicative ;
- un manager ou responsable de service.

Par exemple :

> « Qui prend en charge le diagnostic lorsqu’un service reste indisponible ou qu’un pod demeure en CrashLoopBackOff un vendredi soir ? »

Comparez ensuite les réponses.

Si elles ne convergent pas, le partage Build / Run n’est pas seulement imparfait sur le papier.

Il n’est pas réellement compris par l’organisation.

Et c’est souvent plus dangereux qu’un RACI incomplet, car chaque équipe agit selon une représentation différente des responsabilités.

## Le principe à retenir

Le Build ne doit pas uniquement produire un service déployable.

Il doit produire un service :

- observable ;
- maintenable ;
- documenté ;
- sécurisé ;
- exploitable par une organisation qui évoluera.

Les équipes changent.

Les organisations se transforment.

Le service, lui, doit continuer à tenir.

> Le go-live prouve que l’on sait déployer.  
> Le Run prouve que l’on sait durer.

---

*Extrait du [K8s Platform Governance Lab](https://github.com/Eddyazebaze/k8s-platform-governance-lab) - Eddy Azebaze.*