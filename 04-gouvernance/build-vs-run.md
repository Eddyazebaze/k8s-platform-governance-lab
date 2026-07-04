# Build vs Run — Le point de friction n°1 des plateformes internes

> Modèle de répartition + pièges observés sur le terrain (offre Kubernetes, secteur énergie).

## Le constat

La majorité des tensions sur une plateforme partagée ne viennent pas d'un manque de compétence
technique. Elles viennent d'un partage Build/Run **implicite** : chaque équipe suppose que l'autre
couvre une zone, jusqu'au jour où un incident révèle que personne ne la couvrait.

## Le modèle de répartition

| Sujet | Build (équipe plateforme) | Run (équipe plateforme) | Run (équipe applicative) |
|---|---|---|---|
| Infrastructure cluster (nœuds, réseau, stockage) | ✅ Conception | ✅ Exploitation | — |
| Namespace / isolation logique | ✅ Provisioning | ✅ Quotas, politiques | ✅ Usage quotidien |
| CI/CD (pipeline générique) | ✅ Fourniture du template | ✅ Maintenance du template | ✅ Adaptation applicative |
| Observabilité (stack) | ✅ Mise à disposition | ✅ Disponibilité de la stack | ✅ Instrumentation applicative |
| Alerting | ✅ Fourniture des règles types | ⚠️ Zone grise fréquente | ⚠️ Zone grise fréquente |
| Certificats / secrets | ✅ Mécanisme de rotation | ✅ Exploitation du mécanisme | ✅ Utilisation correcte |
| Scaling applicatif | — | ✅ Capacité plateforme | ✅ Dimensionnement applicatif |
| Sécurité des images | ✅ Scan automatisé | ✅ Blocage si non conforme | ✅ Correction des vulnérabilités |

## Les 3 pièges observés sur le terrain

**1. L'alerting orphelin.** Une alerte remonte, mais ni la plateforme ni l'équipe applicative ne
sait qui doit l'analyser en premier. Résultat : elle est ignorée jusqu'à l'incident. La correction
n'est pas technique — c'est nommer un propriétaire par type d'alerte, pas par outil.

**2. Le "ça marchait avant".** Une équipe applicative modifie un comportement qui dépend d'une
configuration plateforme (quota, policy réseau) sans le signaler. Quand ça casse, chacun pointe
l'autre. La correction : toute dépendance à une configuration plateforme doit être documentée côté
applicatif, pas seulement connue de mémoire.

**3. Le support qui devient du Run déguisé.** L'équipe plateforme dépanne ponctuellement une
équipe applicative "pour aller vite". Six mois plus tard, c'est devenu une dépendance permanente et
non budgétée. La correction : toute intervention récurrente doit soit être formalisée dans le RACI,
soit être refusée et redirigée vers de la documentation en self-service.

## Le test simple pour vérifier que ton partage Build/Run est sain

Pose cette question à trois personnes différentes (plateforme, applicatif, manager) sur un même
sujet — par exemple "qui redémarre un pod qui crash-loop en boucle un vendredi soir" — et compare
les réponses. Si elles ne convergent pas, le partage n'est pas défaillant sur le papier : il est
défaillant dans les têtes, ce qui est plus dangereux.

---
*Extrait du K8s Platform Governance Lab — [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
