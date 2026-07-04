# Gateway API : qui gouverne le réseau sur une plateforme partagée

> Angle : Gateway API n'est pas qu'une évolution technique de l'Ingress Kubernetes. Sur une
> plateforme mutualisée par plusieurs équipes, c'est d'abord une question de **qui décide des
> règles de routage, d'exposition et de sécurité réseau**, pas de configuration YAML.

## Le changement de modèle

L'Ingress classique concentre toute la configuration réseau dans un objet unique, souvent géré par
une seule équipe. Gateway API sépare explicitement les rôles :

- **Le propriétaire de l'infrastructure** définit la `GatewayClass` et la `Gateway` (les points
  d'entrée globaux, la sécurité TLS, les limites d'exposition).
- **Les équipes applicatives** définissent leurs propres `HTTPRoute` pour router leur trafic, sans
  toucher à la configuration globale.

C'est un progrès réel : les équipes gagnent en autonomie. Mais l'autonomie sans gouvernance devient
vite un risque, c'est exactement le sujet que ce document traite.

## Les questions RACI qui se posent (et qui n'ont souvent pas de réponse écrite)

| Décision | Qui devrait trancher ? | Piège observé si non clarifié |
|---|---|---|
| Créer une nouvelle `Gateway` (point d'entrée) | Équipe plateforme uniquement | Multiplication de points d'entrée non inventoriés |
| Autoriser un `HTTPRoute` à s'attacher à une `Gateway` partagée | Politique d'attachement définie par la plateforme | Une équipe expose un service sans revue de sécurité |
| Définir les règles de rate-limiting / quotas | Plateforme, avec délégation possible par domaine | Une équipe sature la Gateway partagée pour toutes les autres |
| Gérer les certificats TLS au niveau Gateway | Plateforme (rotation centralisée) | Certificats gérés en doublon, source d'incidents |

## Le vrai risque du multi-tenancy réseau

Gateway API permet techniquement à plusieurs équipes de partager un même point d'entrée. Le risque
n'est pas que ça ne fonctionne pas, c'est que ça fonctionne **sans qu'aucune limite ne soit posée**,
jusqu'à ce qu'une équipe consomme toute la capacité ou expose une route non sécurisée sur une
Gateway partagée par des services critiques.

C'est le même schéma que le Build/Run : la technologie permet le self-service, mais le self-service
sans garde-fou devient du self-risk. La politique d'attachement (`ReferenceGrant`, namespaces
autorisés) est l'endroit exact où doit s'écrire la gouvernance, pas seulement la configuration.

## La question à se poser avant d'adopter Gateway API sur une plateforme partagée

Pas "cette techno est-elle plus moderne que l'Ingress ?" : la réponse est oui. Mais **"avons-nous
défini qui peut attacher une route, avec quelles limites, avant de l'ouvrir à plusieurs équipes ?"**.
Sans cette réponse écrite, la migration technique déplace le problème de gouvernance sans le
résoudre.

---
*Extrait du K8s Platform Governance Lab, [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
