# Gouvernance des demandes - Onboarding et arbitrage

> Comment une équipe qui découvre la plateforme sait-elle par où commencer, et comment sont
> arbitrées les demandes qui sortent du cadre standard.

## Le problème que ce document résout

Une plateforme peut avoir toute la documentation technique du monde : si le **premier pas** n'est
pas clair, chaque équipe invente sa propre façon d'entrer en contact, et la charge retombe sur les
personnes les plus disponibles de l'équipe plateforme - pas sur un processus.

## Le parcours standard (à afficher, littéralement, quelque part de visible)

1. **Découverte** - l'équipe demandeuse consulte le catalogue de services (voir
   `catalogue-de-services.md`) pour savoir si son besoin est déjà couvert.
2. **Qualification** - un formulaire ou ticket type recense : type de besoin, criticité,
   échéance, contact référent côté équipe demandeuse.
3. **Triage** - l'équipe plateforme classe la demande en 3 catégories (voir tableau ci-dessous).
4. **Traitement** - selon la catégorie, délai et interlocuteur diffèrent, et c'est communiqué
   dès le triage, pas découvert après relance.

## Les 3 catégories de demandes (et pourquoi les distinguer change tout)

| Catégorie | Exemple | Délai type | Qui traite |
|---|---|---|---|
| **Standard** | Nouveau namespace, quota par défaut | Self-service ou < 2 jours | Équipe plateforme, sans arbitrage |
| **Spécifique** | Exception à une policy réseau, ressources hors norme | Revue sous 1 semaine | Équipe plateforme + validation manager |
| **Structurante** | Nouveau cas d'usage impactant l'architecture (multi-cluster, nouvelle intégration) | Revue de roadmap | Comité plateforme, arbitrage priorisé |

Sans cette distinction écrite, toutes les demandes atterrissent dans la même file, et une demande
structurante urgente pour une équipe finit traitée avec la même priorité qu'un simple ajustement de
quota - ou l'inverse, une demande standard attend une revue de comité qui n'était pas nécessaire.

## Le piège le plus fréquent

**La demande informelle qui contourne le processus.** Une personne connaît quelqu'un dans l'équipe
plateforme et obtient satisfaction plus vite que le circuit officiel. À court terme ça rend service.
À moyen terme, ça décrédibilise le processus documenté et concentre la charge sur des individus
plutôt que sur une équipe. La règle simple : toute demande traitée hors circuit doit être
rétroactivement enregistrée dans le même système que les demandes officielles - sinon le circuit
officiel devient la voie lente par construction.

## Ce qu'il faut mesurer pour savoir si la gouvernance des demandes fonctionne

- Délai moyen de traitement, par catégorie (pas une moyenne globale, qui masque les écarts)
- Part des demandes traitées hors circuit officiel
- Taux de demandes mal catégorisées à l'origine (signal que la grille de triage doit être clarifiée)

---
*Extrait du K8s Platform Governance Lab - [github.com/Eddyazebaze](https://github.com/Eddyazebaze)*
