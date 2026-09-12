# 🔀 Git & GitOps

> Branching, rebase/merge, ArgoCD, Flux, drift detection

**50 questions**

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

### 16. Quelles sont les trois zones de Git (working directory, index, repository) ?
`🟢 Débutant` · Sujet : **Git**

**Réponse :** Le working directory contient les fichiers modifiés, l'index (staging area) prépare le prochain commit (`git add`), et le repository stocke les commits (`git commit`). Cette séparation permet de committer une partie seulement des modifications (`git add -p`).

### 17. Que fait `git rebase -i` et à quoi sert-il ?
`🟢 Débutant` · Sujet : **Git**

**Réponse :** Le rebase interactif permet de réécrire une série de commits : réordonner, fusionner (`squash`/`fixup`), reformuler (`reword`), supprimer ou éditer. On l'utilise pour nettoyer l'historique d'une branche avant de la partager, jamais sur des commits déjà poussés et partagés.

### 18. Différence entre `git reset --soft`, `--mixed` et `--hard` ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** `--soft` déplace HEAD en gardant index et fichiers (recommit). `--mixed` (défaut) déplace HEAD et vide l'index, garde les fichiers. `--hard` déplace HEAD et écrase index et fichiers : les modifications non commitées sont perdues. `git reflog` permet de retrouver un commit après un reset malheureux.

### 19. Qu'est-ce que `git reflog` et comment récupérer un commit perdu ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Le reflog journalise tous les mouvements de HEAD et des branches localement (~90 jours). Après un `reset --hard`, un rebase raté ou une branche supprimée, `git reflog` montre le SHA précédent et `git checkout <sha>` ou `git branch recovery <sha>` le restaure.

### 20. Différence entre `git merge --squash`, `--no-ff` et fast-forward ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Fast-forward : la branche cible avance simplement sans commit de merge (historique linéaire). `--no-ff` force un commit de merge conservant la trace de la branche. `--squash` condense tous les commits de la branche en un seul sur la cible, sans lien avec la branche d'origine.

### 21. Comment résoudre un conflit de merge ou de rebase ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Git marque les zones `<<<<<<<`, `=======`, `>>>>>>>` dans les fichiers. On édite, puis `git add` et `git merge --continue` (ou `git rebase --continue`). `git mergetool`, `git diff --ours/--theirs` et `git checkout --ours/--theirs <file>` aident. En cas de doute, `git merge --abort` / `git rebase --abort`. `git rerere` mémorise les résolutions.

### 22. Qu'est-ce que `git bisect` ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Une recherche dichotomique du commit ayant introduit une régression : `git bisect start`, `git bisect bad`, `git bisect good <sha>`, puis Git propose des commits à tester jusqu'à identifier le coupable. `git bisect run <script>` automatise avec un test qui retourne 0/1.

### 23. Différence entre `git log --oneline --graph`, `git blame` et `git show` ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** `git log --graph` visualise les branches et merges. `git blame <file>` indique le dernier commit et auteur de chaque ligne (`-w` ignore les espaces, `-C` suit les déplacements). `git show <sha>` affiche le contenu d'un commit. `git log -S "texte"` cherche les commits ayant ajouté/supprimé une chaîne.

### 24. Qu'est-ce qu'un commit signé et pourquoi l'imposer ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Signer les commits avec GPG, SSH (Git 2.34+) ou Sigstore/gitsign prouve leur auteur, car le champ `author` est librement modifiable. Les plateformes affichent « Verified » et une règle de protection de branche peut exiger des commits signés, ce qui protège la chaîne d'approvisionnement.

### 25. Qu'est-ce que Conventional Commits ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Une convention de messages `type(scope): description` (`feat`, `fix`, `docs`, `refactor`, `chore`, `BREAKING CHANGE:` dans le corps). Elle rend l'historique lisible et permet de générer automatiquement changelog et numéro de version (semantic-release, release-please), et de valider les messages avec commitlint.

### 26. Différence entre sous-modules, subtree et monorepo ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Un submodule référence un commit précis d'un autre dépôt (complexité de synchronisation). Un subtree copie l'historique dans le dépôt parent. Un monorepo regroupe plusieurs projets dans un seul dépôt avec des outils (Nx, Turborepo, Bazel) pour ne construire que ce qui a changé. Le choix dépend du couplage entre projets.

### 27. Qu'est-ce que Git LFS ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Large File Storage remplace les gros fichiers binaires (images, modèles, archives) par des pointeurs dans Git et stocke le contenu sur un serveur dédié. Il évite de gonfler le dépôt tout en versionnant ces fichiers ; à configurer via `.gitattributes`.

### 28. Que sont les hooks Git côté client et côté serveur ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Scripts déclenchés à des événements : `pre-commit` (lint, format), `commit-msg` (validation du message), `pre-push` (tests rapides) côté client ; `pre-receive`/`update` côté serveur pour imposer des politiques. Les hooks client ne sont pas versionnés par défaut, d'où les outils `pre-commit`/husky.

### 29. Qu'est-ce qu'une branche protégée et quelles règles y appliquer ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Une configuration côté plateforme (GitHub/GitLab) sur `main`/`release/*` : interdire le push direct et le force-push, exiger une merge request avec N approbations, statut CI vert, résolution des commentaires, commits signés, historique linéaire, et CODEOWNERS pour les revues obligatoires par domaine.

### 30. Qu'est-ce que le fichier CODEOWNERS ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Un fichier qui associe des chemins à des équipes ou personnes (`/infra/ @platform-team`). La plateforme demande automatiquement leur revue sur toute merge request touchant ces fichiers et peut la rendre obligatoire. Il formalise la responsabilité par domaine dans un monorepo.

### 31. Comment réécrire l'historique pour supprimer un secret commité ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Considérer le secret compromis et le révoquer immédiatement. Ensuite `git filter-repo` (remplace `filter-branch`) ou BFG Repo-Cleaner pour purger le fichier de tout l'historique, puis force-push et demander à tous les collaborateurs de recloner. Les forks et caches de la plateforme peuvent conserver l'ancien contenu.

### 32. Différence entre `git worktree` et cloner plusieurs fois ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** `git worktree add ../hotfix hotfix-branch` crée un second répertoire de travail partageant le même dépôt `.git`, permettant de travailler sur deux branches simultanément sans stash ni clone dupliqué (économie de disque et un seul fetch).

### 33. Qu'est-ce que le shallow clone et à quoi sert-il en CI ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** `git clone --depth 1` ne récupère que le dernier commit, accélérant les checkouts CI sur de gros dépôts. Limites : pas d'historique pour `git describe`, `blame` ou le calcul de version ; utiliser `--depth 50` ou `fetch --unshallow` si nécessaire.

### 34. Quelles stratégies de branches existent (GitFlow, GitHub Flow, trunk-based) ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** GitFlow : branches `develop`, `release/*`, `hotfix/*` — adapté aux releases versionnées espacées. GitHub Flow : `main` + branches de fonctionnalité courtes mergées par PR, déploiement continu. Trunk-based : commits fréquents sur `main`, branches de quelques heures, feature flags. La tendance moderne va vers trunk-based pour maximiser l'intégration.

### 35. Qu'est-ce qu'une release branch et comment gérer un hotfix ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** Une branche `release/1.4` figée pour stabilisation et corrections. Un hotfix est corrigé sur la branche de release (ou de la version en prod), tagué, déployé, puis cherry-pické ou mergé vers `main` pour ne pas réintroduire le bug dans la version suivante.

### 36. Qu'est-ce que le `.gitattributes` et le problème des fins de ligne ?
`🟠 Intermédiaire` · Sujet : **Git**

**Réponse :** `.gitattributes` définit des comportements par chemin : normalisation des fins de ligne (`* text=auto`, évite les diffs CRLF/LF entre Windows et Linux), fichiers binaires, LFS, stratégies de merge (`merge=ours` pour un changelog), et `export-ignore` pour les archives.

### 37. Comment structurer les dépôts GitOps (mono vs multi-repo, dossier par environnement vs branche) ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Séparer le code applicatif du dépôt de configuration (manifests/Helm values). Dans ce dernier, préférer un dossier par environnement (`envs/dev`, `envs/prod`) avec Kustomize overlays plutôt qu'une branche par environnement (les branches divergent et compliquent la promotion). Un dépôt par équipe ou par plateforme selon la taille.

### 38. Comment promouvoir une version de dev à prod en GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** La CI construit et pousse l'image, puis ouvre une merge request (ou commit automatique) modifiant le tag d'image dans `envs/dev`. La promotion vers staging/prod est un nouveau commit/merge request sur le dossier correspondant, potentiellement automatisé (ArgoCD Image Updater, Kargo) avec approbations humaines pour la production.

### 39. Qu'est-ce que la synchronisation automatique, le self-heal et le prune dans ArgoCD ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** `automated sync` applique les changements Git sans action manuelle. `selfHeal` rétablit l'état Git si quelqu'un modifie le cluster à la main (`kubectl edit`). `prune` supprime les ressources retirées de Git. Ensemble, ils garantissent que Git est l'unique source de vérité ; en prod, certaines équipes gardent une validation manuelle.

### 40. Comment gérer les secrets en GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Ne jamais commiter de secrets en clair. Options : Sealed Secrets (chiffrés avec la clé publique du cluster), SOPS avec KMS/age (fichiers chiffrés dans Git, déchiffrés par ArgoCD/Flux via plugin), ou External Secrets Operator qui ne commite que des références vers Vault/AWS Secrets Manager.

### 41. Qu'est-ce que les sync waves et les hooks ArgoCD ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Les annotations `argocd.argoproj.io/sync-wave` ordonnent le déploiement des ressources (namespace et CRDs en vague -1, base en 0, application en 1). Les hooks `PreSync`/`Sync`/`PostSync`/`SyncFail` exécutent des Jobs (migration de base, tests smoke, notification) autour de la synchronisation.

### 42. Comment fonctionne le rollback en GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Un rollback est un `git revert` du commit fautif : le controller resynchronise l'état précédent, et l'historique conserve la trace de l'incident. ArgoCD propose aussi un rollback UI vers une révision antérieure, mais il désactive l'auto-sync tant que Git n'est pas aligné. Attention aux migrations de base non réversibles.

### 43. Qu'est-ce que la health assessment dans ArgoCD ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** ArgoCD évalue l'état des ressources (Healthy, Progressing, Degraded, Suspended, Missing) à partir de leur status (Deployment disponible, Ingress avec adresse, Job terminé). Des health checks Lua personnalisés couvrent les CRDs. Combiné au statut Synced/OutOfSync, cela donne une vue fiable de chaque application.

### 44. Qu'est-ce que Flux et ses controllers principaux ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Flux est une suite d'operators : source-controller (Git, Helm repos, OCI, buckets), kustomize-controller, helm-controller, notification-controller (alertes, webhooks), image-reflector/automation-controller (mise à jour automatique des tags d'image dans Git). Il est natif Kubernetes (CRDs) et s'accompagne d'une CLI `flux bootstrap`.

### 45. Comment gérer plusieurs clusters en GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** ArgoCD : une instance centrale gérant plusieurs clusters via des credentials enregistrés, et des ApplicationSets avec générateur `clusters` pour déployer sur tous. Flux : une instance par cluster pointant sur un dossier dédié du dépôt. Un « hub cluster » centralise, mais un ArgoCD par cluster limite le blast radius.

### 46. Qu'est-ce que la progressive delivery et comment l'intégrer en GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps**

**Réponse :** Livrer graduellement (canary, blue-green, A/B) avec analyse automatisée des métriques avant d'élargir. Argo Rollouts ou Flagger (Flux) remplacent le Deployment par une ressource `Rollout`/`Canary`, pilotent le service mesh/ingress pour le trafic, interrogent Prometheus et annulent automatiquement en cas de dégradation.

### 47. Comment gérer le déploiement de la base de données et des migrations en GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps/Deploy**

**Réponse :** Séparer le schéma (Job de migration en hook PreSync ou init container avec verrou) de l'application, garantir la compatibilité ascendante (expand/contract), et éviter les migrations destructrices automatiques. Pour les bases elles-mêmes, un operator (CloudNativePG) permet de les déclarer aussi en Git.

### 48. Comment gérer les variables d'environnement et la configuration par environnement dans les manifests ?
`🟠 Intermédiaire` · Sujet : **GitOps/Deploy**

**Réponse :** Kustomize overlays (patches par environnement, `configMapGenerator` avec hash pour redémarrer les Pods au changement) ou Helm values par environnement. Les valeurs non sensibles vivent dans Git ; les secrets via External Secrets. Éviter la logique conditionnelle complexe dans les templates : mieux vaut des overlays lisibles.

### 49. Qu'est-ce que la « drift » et comment ArgoCD/Flux la détectent-ils ?
`🟠 Intermédiaire` · Sujet : **GitOps/Deploy**

**Réponse :** Les controllers comparent en continu (polling ou webhook Git, et watch des ressources cluster) l'état désiré rendu depuis Git avec l'état réel. Toute différence marque l'application `OutOfSync` ; avec self-heal elle est corrigée, sinon notifiée. Certaines différences légitimes (champs mutés par des controllers) sont ignorées via `ignoreDifferences`.

### 50. Quels sont les inconvénients ou limites du GitOps ?
`🟠 Intermédiaire` · Sujet : **GitOps/Deploy**

**Réponse :** Latence de propagation, secrets à gérer spécifiquement, prolifération de dépôts/YAML, opérations impératives difficiles (redémarrage, scaling d'urgence à réconcilier), courbe d'apprentissage, et nécessité d'une discipline stricte (pas de `kubectl apply` manuel). Il faut aussi outiller la promotion entre environnements, non couverte nativement.
