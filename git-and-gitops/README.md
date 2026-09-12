# 🔀 Git & GitOps

> Branching, rebase/merge, ArgoCD, Flux, drift detection

**15 questions**

---

### 1. Quelle est la différence entre `git merge` et `git rebase` ?
`🟢 Débutant` · Sujet : **Git**

**Réponse :** `merge` crée un commit de fusion combinant les historiques. `rebase` réapplique les commits par-dessus une autre branche, produisant un historique linéaire mais réécrivant les commits.

### 2. Principe fondamental de GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Le dépôt Git sert de source de vérité unique. Un agent (ArgoCD, Flux) synchronise en continu l'état réel avec l'état déclaré.

### 3. À quoi sert `git cherry-pick` ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Applique un commit spécifique d'une branche à une autre sans fusionner tout l'historique.

### 4. Avantage principal de GitOps vs déploiement manuel ?
`🟢 Débutant` · Sujet : **GitOps**

**Réponse :** Traçabilité complète, reproductibilité, rollback simplifié, réduction des erreurs humaines.

### 5. Que fait `git stash` ?
`🟢 Débutant` · Sujet : **Git**

**Réponse :** Met de côté temporairement les modifications non commitées, réapplicables via `git stash pop`.

### 6. Différence `git fetch` / `git pull` ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** `fetch` récupère sans fusionner. `pull` = fetch + merge (ou rebase) automatique.

### 7. Différence push / pull deployment ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Push = pipeline CI/CD externe applique les changements. Pull = agent interne (ArgoCD/Flux) surveille et applique lui-même.

### 8. Différence `git reset` / `git revert` ?
`🟢 Débutant` · Sujet : **Git**

**Réponse :** reset déplace le pointeur de branche (réécrit historique). revert crée un nouveau commit annulant un précédent.

### 9. Outils GitOps courants ?
`🟢 Débutant` · Sujet : **GitOps**

**Réponse :** ArgoCD et Flux.

### 10. Detached HEAD ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** HEAD pointe directement vers un commit plutôt qu'une branche ; risque de perte de commits.

### 11. Dérive de configuration (drift) ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Écart entre état réel et état déclaré ; GitOps réconcilie automatiquement.

### 12. Qu'est-ce qu'un `.gitignore` ?
`🟢 Débutant` · Sujet : **Git**

**Réponse :** Liste des fichiers/répertoires que Git doit ignorer.

### 13. Différence tag / branche ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Tag = référence immuable pointant vers un commit précis. Branche évolue avec de nouveaux commits.

### 14. Pattern App of Apps (ArgoCD) ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Une application parente déclare et gère plusieurs applications enfants.

### 15. Qu'est-ce qu'un "canary analysis" automatisé vs un canary release manuel ?
`🟠 Intermédiaire` · Sujet : **GitOps/Deploy**

**Réponse :** Le manuel nécessite une validation humaine. L'analyse automatisée (Argo Rollouts, Flagger) compare en continu les métriques et déclenche un rollback automatique si dégradation, sans intervention humaine.
