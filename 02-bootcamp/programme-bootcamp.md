# Bootcamp Kubernetes (1 jour) — Programme détaillé

> Prérequis : Windows + Docker Desktop installé (voir section Installation).
> Public : profils techniques débutants sur Kubernetes, ou non-tech voulant
> pratiquer après avoir vu le `01-visual-explorer`.

## Objectifs de la journée

- Installer un cluster local fonctionnel
- Déployer une application simple de bout en bout
- Comprendre concrètement namespaces, RBAC, NetworkPolicies (pas juste en théorie)
- Savoir observer (logs / events) et diagnostiquer un problème simple

---

## Programme

### 9h00 – 10h00 : Installation et premier cluster

1. Installer Docker Desktop (si pas déjà fait) et activer Kubernetes dans les paramètres,
   ou installer `kind`/`minikube` en alternative.
2. Vérifier l'installation : `kubectl cluster-info` et `kubectl get nodes`.
3. Explorer la structure par défaut : `kubectl get namespaces`, `kubectl get pods -A`.

**Checkpoint** : le cluster répond, `kubectl get nodes` affiche au moins un nœud `Ready`.

### 10h00 – 11h30 : Déployer une app simple

1. Créer un namespace de test : `kubectl create namespace bootcamp-test`.
2. Déployer une app basique (ex : nginx) via un manifest `Deployment` + `Service`.
3. Exposer l'app localement (`kubectl port-forward`) et vérifier l'accès dans le navigateur.
4. Modifier le nombre de réplicas et observer le comportement (`kubectl scale`).

**Checkpoint** : l'app est accessible via le navigateur, et le scaling fonctionne visiblement.

### 11h30 – 12h30 : Namespaces, RBAC, NetworkPolicies — la pratique

Utiliser les manifests du dossier `03-manifests/` comme base :

1. Appliquer `namespaces.yaml` et observer les quotas (`kubectl describe resourcequota`).
2. Appliquer `rbac.yaml` : créer un utilisateur de test avec le rôle `app-developer`, vérifier
   qu'il ne peut pas agir en dehors de son namespace (`kubectl auth can-i`).
3. Appliquer `networkpolicies.yaml` sur le namespace `prod` et constater qu'une communication
   non autorisée échoue (test avec un pod de debug).

**Checkpoint** : compréhension concrète — "pourquoi ça bloque" plutôt que "ça bloque".

### 13h30 – 15h00 : Observer et diagnostiquer

1. Consulter les logs d'un pod (`kubectl logs`) et les events du namespace
   (`kubectl get events --sort-by=.lastTimestamp`).
2. Provoquer volontairement une erreur simple (image inexistante, quota dépassé) et
   diagnostiquer à partir des logs/events uniquement.
3. Nettoyer les ressources de test.

**Checkpoint** : capacité à diagnostiquer un problème simple sans aide.

### 15h00 – 16h00 : Bilan et mise en perspective

- Retour sur les notions vues dans la journée
- Lien avec la partie gouvernance du lab (`04-gouvernance/`) : ce qu'on vient de manipuler
  techniquement (RBAC, NetworkPolicies) est la traduction concrète de décisions de gouvernance
  (qui a accès à quoi, qui communique avec qui)
- Questions ouvertes / debrief

---

## Checklist de fin de journée

- [ ] Cluster local installé et fonctionnel
- [ ] Une app déployée et accessible
- [ ] Un namespace avec quota appliqué et vérifié
- [ ] Un rôle RBAC testé (accès refusé en dehors du périmètre)
- [ ] Une NetworkPolicy appliquée et son effet constaté
- [ ] Un diagnostic simple réalisé à partir de logs/events

## Notes de montée en compétences

Ce bootcamp est volontairement dense sur une journée : l'objectif n'est pas l'exhaustivité, mais
la première autonomie. Les manifests utilisés viennent directement du dossier `03-manifests/` du
lab — ce ne sont pas des exemples jetables, ils sont réutilisables pour la suite.

---
Projet Augmenté® — [Eddy Azebaze](https://github.com/Eddyazebaze)
