# 🏗️ Infrastructure as Code

> Terraform, Ansible, modules, providers, playbooks

**50 questions**

---

### 1. À quoi sert `terraform.tfstate` ?
`🟢 Débutant` · Sujet : **Terraform**

**Réponse :** Stocke l'état actuel de l'infrastructure gérée par Terraform, permettant de calculer les différences lors des futurs plan/apply.

### 2. Qu'est-ce qu'un playbook Ansible ?
`🟢 Débutant` · Sujet : **Ansible**

**Réponse :** Fichier YAML décrivant des tâches à exécuter sur des hôtes distants, définissant l'état désiré du système, de façon idempotente.

### 3. À quoi servent les modules Terraform ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Regroupent et réutilisent un ensemble de ressources sous forme de composant paramétrable, favorisant modularité et cohérence.

### 4. Qu'est-ce qu'un rôle Ansible ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Structure organisée de répertoires regroupant une logique de configuration réutilisable entre playbooks.

### 5. Différence `plan` / `apply` ?
`🟢 Débutant` · Sujet : **Terraform**

**Réponse :** `plan` = simulation des changements. `apply` = exécution réelle des changements.

### 6. Qu'est-ce que l'idempotence ?
`🟢 Débutant` · Sujet : **Ansible**

**Réponse :** Exécuter plusieurs fois le même playbook produit le même résultat final sans effet indésirable.

### 7. Qu'est-ce qu'un provider ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Plugin permettant à Terraform d'interagir avec une plateforme spécifique (AWS, Azure, K8s).

### 8. Qu'est-ce qu'un handler ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Tâche déclenchée uniquement lorsqu'elle est notifiée par une autre tâche ayant produit un changement.

### 9. À quoi sert `terraform init` ?
`🟢 Débutant` · Sujet : **Terraform**

**Réponse :** Initialise le répertoire (téléchargement providers, config backend).

### 10. Qu'est-ce qu'un inventaire ?
`🟢 Débutant` · Sujet : **Ansible**

**Réponse :** Fichier listant les hôtes cibles organisés en groupes, avec variables associées.

### 11. Qu'est-ce qu'un data source ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Lit des informations sur une ressource existante sans la gérer directement.

### 12. Qu'est-ce qu'`ansible-vault` ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Chiffre des données sensibles pour les versionner en toute sécurité dans Git.

### 13. Qu'est-ce qu'un backend distant et pourquoi verrouiller le state ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Le backend (S3 + DynamoDB pour le verrou, ou S3 avec `use_lockfile` depuis Terraform 1.10, GCS, Terraform Cloud, Azure Blob) stocke le state hors du poste local pour le partager. Le verrouillage empêche deux `apply` simultanés de corrompre le state. Le state contenant des secrets, il doit être chiffré et à accès restreint.

### 14. Comment structurer un projet Terraform pour plusieurs environnements ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Options : un dossier par environnement appelant des modules communs avec des variables (`envs/dev`, `envs/prod`), des workspaces (même code, states séparés, mais risque d'erreur d'environnement), ou Terragrunt pour factoriser. La séparation par dossiers avec state distinct par environnement et par domaine (réseau, données, applications) limite le blast radius.

### 15. Différence entre `variable`, `locals` et `output` ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `variable` : entrée paramétrable d'un module (type, défaut, validation, `sensitive`). `locals` : valeurs calculées internes pour éviter la répétition. `output` : valeurs exposées par un module ou un root (ex : ARN d'un LB), consommables par d'autres states via `terraform_remote_state` ou des data sources.

### 16. À quoi servent `count` et `for_each`, et pourquoi préférer `for_each` ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Les deux créent plusieurs instances d'une ressource. `count` indexe par nombre : supprimer un élément au milieu décale les index et recrée les ressources suivantes. `for_each` indexe par clé de map/set : stable, chaque instance est identifiée par sa clé, et permet d'itérer sur des objets complexes.

### 17. Que fait le bloc `lifecycle` (`create_before_destroy`, `prevent_destroy`, `ignore_changes`) ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `create_before_destroy` crée la nouvelle ressource avant de supprimer l'ancienne (zéro interruption). `prevent_destroy` fait échouer tout plan qui la détruirait (base de données). `ignore_changes` ignore les dérives sur certains attributs modifiés hors Terraform (tags posés par l'autoscaling, `desired_count` géré par un HPA).

### 18. Comment importer une ressource existante dans Terraform ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `terraform import aws_s3_bucket.x nom-bucket` lie une ressource réelle à une adresse du state, puis on écrit la configuration correspondante jusqu'à ce que `plan` soit vide. Depuis Terraform 1.5, le bloc `import { to = ..., id = ... }` déclaratif avec `plan -generate-config-out` génère la configuration automatiquement.

### 19. Comment renommer ou déplacer une ressource sans la détruire ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Le bloc `moved { from = aws_instance.old to = aws_instance.new }` (Terraform 1.1+) indique que l'adresse a changé, évitant un destroy/create. `terraform state mv` fait de même impérativement. Ces opérations sont indispensables lors du refactoring en modules.

### 20. Qu'est-ce que le drift et comment le détecter ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Une différence entre l'infrastructure réelle et le state (modification manuelle en console). `terraform plan -refresh-only` montre le drift sans proposer de changements de configuration ; un `plan` planifié en CI (ou driftctl) le détecte en continu. La résolution consiste soit à réappliquer, soit à mettre à jour le code.

### 21. Comment gérer les secrets dans Terraform ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Marquer les variables `sensitive = true` (masquées dans les logs mais présentes dans le state), lire les secrets depuis Vault/AWS Secrets Manager via data sources plutôt que dans des `.tfvars` commités, chiffrer le backend, et ne jamais commiter `terraform.tfstate` ni `*.tfvars` sensibles. Les `ephemeral` values (1.10+) évitent de les écrire dans le state.

### 22. Comment tester du code Terraform ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `terraform validate` et `fmt -check`, linters (tflint), scans de sécurité (tfsec/Trivy, Checkov), policy as code (OPA/Sentinel) sur le plan, tests natifs `terraform test` (1.6+, fichiers `.tftest.hcl` avec `run` blocks et assertions), Terratest (Go) pour déployer réellement et vérifier, et `plan` en CI sur chaque merge request.

### 23. Qu'est-ce qu'un module de registry et comment versionner ses modules ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Le Terraform Registry (public ou privé) héberge des modules réutilisables (`terraform-aws-modules/vpc/aws`). Ses propres modules se publient dans un dépôt Git tagué en SemVer, référencés via `source = "git::...?ref=v1.2.0"`. Toujours fixer la version d'un module et des providers (`required_providers` avec `~>`).

### 24. Quelle est la différence entre `terraform taint`/`-replace` et `destroy` ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `terraform apply -replace=aws_instance.x` (remplace `taint`) force la recréation d'une ressource lors du prochain apply, sans toucher aux autres. `terraform destroy` supprime toute l'infrastructure du state (ou `-target` pour une cible, à utiliser avec prudence).

### 25. Qu'est-ce que la dépendance implicite et explicite (`depends_on`) ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Terraform déduit l'ordre à partir des références entre ressources (`subnet_id = aws_subnet.a.id`). `depends_on` déclare une dépendance non visible dans les attributs (une policy IAM devant exister avant qu'un rôle soit utilisé par une Lambda). L'abuser réduit le parallélisme et masque une mauvaise structuration.

### 26. Qu'est-ce que le provider `null`/`terraform_data` et les provisioners, et pourquoi les éviter ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Les provisioners (`local-exec`, `remote-exec`) exécutent des scripts au cycle de vie ; ils sont un dernier recours car non idempotents et invisibles dans le plan. `terraform_data` (remplace `null_resource`) sert à déclencher des actions sur changement d'une valeur. Préférer cloud-init, Ansible, ou des ressources natives.

### 27. Qu'est-ce qu'OpenTofu ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Un fork open source de Terraform créé après le passage de HashiCorp à la licence BSL (2023), maintenu par la Linux Foundation. Il reste compatible avec le langage et les providers, et ajoute des fonctionnalités propres (chiffrement du state, `for_each` sur les providers). Les entreprises choisissent selon la politique de licence.

### 28. Comment utiliser Terraform pour Kubernetes et Helm ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Les providers `kubernetes` et `helm` permettent de déclarer namespaces, RBAC, releases Helm depuis Terraform, pratique pour le bootstrap d'un cluster (ingress, ArgoCD). Au-delà, il vaut mieux laisser GitOps (ArgoCD/Flux) gérer les applications : Terraform crée le cluster et installe l'operator GitOps, qui prend le relais.

### 29. Qu'est-ce que le `-target` et pourquoi son usage doit rester exceptionnel ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `terraform apply -target=module.x` n'applique que la ressource ciblée et ses dépendances. Utile pour débloquer une situation, mais il contourne le plan global et peut laisser le state incohérent. Un besoin fréquent de `-target` signale un state trop gros à découper.

### 30. Comment gérer un `plan` en CI et l'approbation avant `apply` ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Pipeline : `init` → `validate` → `plan -out=tfplan` posté en commentaire de la merge request (Atlantis, GitLab/GitHub Actions) → revue humaine → `apply tfplan` sur la branche principale avec verrou et environnement protégé. Le plan sauvegardé garantit qu'on applique exactement ce qui a été revu.

### 31. Quelles fonctions et expressions HCL sont indispensables ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Conditionnelles `cond ? a : b`, `for` expressions (`{ for k, v in var.map : k => upper(v) }`), splat `aws_instance.x[*].id`, `try()`/`coalesce()` pour les valeurs optionnelles, `lookup`, `merge`, `flatten`, `templatefile()` pour les fichiers de configuration, `jsonencode`/`yamlencode`, et les blocs `dynamic` pour générer des blocs imbriqués.

### 32. Différence entre Ansible et Terraform, et comment les combiner ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Terraform provisionne l'infrastructure (déclaratif, avec state) ; Ansible configure les systèmes (agentless via SSH, procédural mais idempotent par module). Combinaison classique : Terraform crée les VM et génère un inventaire dynamique, Ansible installe et configure les logiciels. Dans un monde conteneurisé, Ansible sert surtout aux hôtes et au legacy.

### 33. Qu'est-ce qu'un inventaire dynamique ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Un plugin ou script qui interroge une source (AWS EC2 tags, Kubernetes, Terraform state, CMDB) pour construire l'inventaire à la volée, plutôt qu'un fichier statique. Il évite les listes d'hôtes périmées et permet de cibler par tags (`group_by`).

### 34. Quelle est la précédence des variables Ansible ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Du moins prioritaire au plus prioritaire (simplifié) : defaults de rôle, variables d'inventaire (group_vars puis host_vars), facts, variables de play, vars de rôle, `set_fact`/registered, variables d'`include`, et enfin `--extra-vars` en ligne de commande qui écrase tout. Connaître cet ordre évite les surprises.

### 35. Qu'est-ce qu'un fact et à quoi sert `gather_facts` ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Les facts sont des informations collectées sur l'hôte cible au début du play (OS, IP, mémoire, interfaces), disponibles via `ansible_facts`. On les utilise pour conditionner les tâches (`when: ansible_os_family == "Debian"`). Désactiver `gather_facts` accélère les plays qui n'en ont pas besoin ; `setup` les collecte à la demande.

### 36. Comment gérer les templates avec Jinja2 ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Le module `template` rend un fichier `.j2` avec les variables (`{{ var }}`, boucles `{% for %}`, filtres `| default('x')`, `| to_yaml`), puis le copie sur la cible. Combiné à `notify` et un handler, un changement de configuration redémarre le service uniquement si le fichier a changé.

### 37. Qu'est-ce qu'une collection Ansible et Ansible Galaxy ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Une collection regroupe rôles, modules, plugins et playbooks distribuables (`community.general`, `amazon.aws`, `kubernetes.core`). Galaxy est le hub public ; `ansible-galaxy collection install` les installe depuis un `requirements.yml`. Ansible Automation Hub est l'équivalent privé/certifié de Red Hat.

### 38. Comment tester des rôles Ansible ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** `ansible-lint` pour les bonnes pratiques, `ansible-playbook --check --diff` pour un dry-run, Molecule pour tester un rôle dans des conteneurs/VM éphémères (converge, idempotence, verify avec des tests Testinfra ou Ansible), et l'exécution en CI sur chaque changement.

### 39. Différence entre `become`, `delegate_to` et `run_once` ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** `become` élève les privilèges (sudo). `delegate_to` exécute la tâche sur un autre hôte que la cible (par ex. `localhost` pour appeler une API, ou le load balancer pour retirer un nœud). `run_once` exécute la tâche une seule fois pour tout le groupe (migration de base), à combiner avec `delegate_to`.

### 40. Comment faire un déploiement rolling avec Ansible ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** `serial: 2` (ou un pourcentage) traite les hôtes par lots, `max_fail_percentage` arrête le play en cas d'échecs trop nombreux, et des `pre_tasks`/`post_tasks` retirent/réintègrent chaque hôte du load balancer (via `delegate_to`). On ajoute des `wait_for`/`uri` pour vérifier le health check avant de passer au lot suivant.

### 41. Qu'est-ce que les tags et `--limit` ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Les tags (`tags: [config]`) permettent d'exécuter un sous-ensemble de tâches (`--tags config`, `--skip-tags`). `--limit web01` restreint les hôtes ciblés parmi l'inventaire. Les deux accélèrent les itérations et les interventions ciblées.

### 42. Comment gérer les erreurs et les tâches non idempotentes (`changed_when`, `failed_when`, `block/rescue`) ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** `changed_when`/`failed_when` redéfinissent l'interprétation du résultat d'une commande (ex : `command` renvoyant toujours « changed »). `ignore_errors` continue malgré l'échec. `block`/`rescue`/`always` structurent un try/catch/finally pour des séquences avec rollback.

### 43. Qu'est-ce qu'AWX / Ansible Automation Platform ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Une interface web et API au-dessus d'Ansible : inventaires centralisés, credentials chiffrés, planification, RBAC, journal des exécutions, workflows chaînant des job templates, webhooks. AWX est la version open source ; Automation Platform la version supportée par Red Hat.

### 44. Qu'est-ce que Terraform Cloud/Enterprise et ses alternatives (Spacelift, env0, Atlantis) ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Des plateformes qui exécutent Terraform de façon centralisée : state managé, runs déclenchés par Git, approbations, policy as code, gestion des variables et des secrets, historique et coûts. Atlantis est l'option open source minimaliste pilotée par les merge requests.

### 45. Comment gérer les mises à jour de providers et de version de Terraform ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Fixer `required_version` et `required_providers` avec des contraintes `~>`, commiter `.terraform.lock.hcl` pour figer les versions et checksums, mettre à jour via `terraform init -upgrade` dans une merge request dédiée (Renovate automatise), et lire les notes de version pour les changements cassants, parfois accompagnés de migrations de state.

### 46. Qu'est-ce que la modularisation excessive et les bonnes pratiques de conception de modules ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Un module doit encapsuler une abstraction cohérente (un « service applicatif » avec son ALB, ses rôles, ses alarmes), avoir peu de variables obligatoires avec de bons défauts, des outputs utiles, une documentation (terraform-docs), et des exemples. Des modules d'une ressource (« wrapper ») ou trop configurables (dizaines de variables booléennes) nuisent à la lisibilité.

### 47. Qu'est-ce que le `data` block `aws_caller_identity` et les data sources courantes ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** `aws_caller_identity` récupère l'ID de compte courant, `aws_region` la région, `aws_availability_zones` les AZ, `aws_ami` la dernière image, `aws_iam_policy_document` construit une policy en HCL typé. Ils évitent de coder en dur des valeurs dépendantes du contexte.

### 48. Comment sécuriser l'exécution d'Ansible (clés SSH, vault, connexions) ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Authentification par clé SSH avec agent (jamais de mot de passe en clair), `ansible-vault` pour les fichiers sensibles avec le mot de passe fourni via `--vault-id` ou un script, `no_log: true` sur les tâches manipulant des secrets, vérification des host keys, et exécution depuis un runner CI isolé avec credentials injectés.

### 49. Qu'est-ce qu'un module custom et un plugin de filtre ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Un module est un script Python (ou autre) exécuté sur la cible, retournant du JSON (`changed`, `msg`), à écrire dans `library/` ou une collection quand aucun module existant ne convient. Un filtre Jinja2 personnalisé (`filter_plugins/`) transforme des données dans les templates et les expressions.

### 50. Qu'est-ce que la gestion d'infrastructure « immutable » vs « mutable » ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Mutable : on modifie les serveurs en place (Ansible, patchs), avec risque de dérive. Immutable : on ne modifie jamais une instance, on construit une nouvelle image (Packer) et on remplace (`create_before_destroy`, ASG rolling). Les conteneurs incarnent ce modèle ; il apporte reproductibilité et rollback simple.
