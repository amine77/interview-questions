# 🛠️ DevOps Practices & Tooling

> CI/CD, SonarQube, Trivy, Renovate, Prometheus, Grafana, Backstage

**50 questions**

---

### 1. Qu'est-ce que le principe d'Infrastructure as Code (IaC) ?
`🟢 Débutant` · Sujet : **DevOps**

**Réponse :** Définir et gérer l'infrastructure via des fichiers de configuration versionnés plutôt que des actions manuelles, garantissant reproductibilité, traçabilité et automatisation (Terraform, Ansible, CloudFormation).

### 2. Qu'est-ce que le "Blue-Green Deployment" et en quoi diffère-t-il du "Canary Release" ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Le Blue-Green bascule instantanément tout le trafic d'un environnement stable vers une nouvelle version validée. Le Canary Release déploie la nouvelle version à un petit sous-ensemble d'utilisateurs progressivement.

### 3. Qu'est-ce que SonarQube et à quoi sert-il dans une pipeline CI/CD ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Outil d'analyse statique de code détectant bugs, vulnérabilités, code smells et mesurant la couverture de tests, intégré en CI/CD pour bloquer les déploiements ne respectant pas les quality gates.

### 4. Qu'est-ce que Prometheus et comment fonctionne-t-il avec Grafana ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Prometheus collecte et stocke des métriques via un modèle "pull" (scrape des endpoints /metrics). Grafana se connecte à Prometheus pour visualiser ces métriques sous forme de dashboards et configurer des alertes.

### 5. Qu'est-ce que le "shift-left testing" dans une pipeline CI/CD ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Pratique consistant à exécuter les tests le plus tôt possible dans le cycle de développement plutôt qu'en fin de pipeline, permettant de détecter et corriger les problèmes plus rapidement.

### 6. Qu'est-ce que Vault (HashiCorp) et pourquoi l'utiliser plutôt que des variables d'environnement pour les secrets ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Outil de gestion centralisée des secrets offrant chiffrement, rotation automatique, contrôle d'accès fin et audit, contrairement aux variables d'environnement statiques et sans traçabilité.

### 7. GitHub Actions / GitLab CI et le concept de runner ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Plateformes CI définissant des pipelines déclenchés par événements Git. Un runner est la machine exécutant les jobs.

### 8. Qu'est-ce qu'Argo Rollouts ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Contrôleur K8s ajoutant des stratégies avancées (Canary, Blue-Green) avec analyse automatique des métriques et rollback automatique.

### 9. Qu'est-ce que Trivy ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Scanner de vulnérabilités open-source analysant images Docker et dépôts pour détecter des CVE, intégrable en CI/CD.

### 10. Kustomize vs Helm ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Kustomize personnalise des manifestes YAML via patches déclaratifs sans templating, intégré à kubectl. Helm utilise des templates et des packages versionnés.

### 11. Renovate ou Dependabot ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Outils scannant les dépendances et créant automatiquement des PR de mise à jour, réduisant la dette technique.

### 12. Nexus ou Artifactory ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Gestionnaires de dépôts d'artefacts binaires permettant d'héberger des versions internes, mettre en cache des dépendances externes.

### 13. OpenTelemetry et problème résolu ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Standard unifiant la collecte de traces/métriques/logs, vendor-neutral, évitant le verrouillage propriétaire.

### 14. Backstage (Spotify) ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Plateforme de developer portal centralisant découverte des services, documentation, templates, facilitant l'onboarding en microservices.

### 15. Terragrunt et problème résolu vs Terraform seul ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Wrapper facilitant configurations multi-environnements, évitant duplication via héritage, gestion centralisée des backends d'état.

### 16. Semgrep vs linter classique ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Analyse statique basée sur des règles sémantiques (AST), détectant vulnérabilités spécifiques, contrairement à un linter de style/syntaxe.

### 17. Packer (HashiCorp) ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Automatise la création d'images machine identiques (AMI, Docker, VM), garantissant cohérence et infrastructure immuable.

### 18. Policy as code avec OPA ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Définir des règles de gouvernance en code déclaratif (Rego), appliquées automatiquement (admission controller K8s) plutôt que manuellement.

### 19. GitOps drift detection avec ArgoCD ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Compare en continu l'état Git et l'état réel du cluster, signalant les divergences, avec correction automatique possible.

### 20. k9s et son intérêt quotidien ?
`🟢 Débutant` · Sujet : **Outils DevOps**

**Réponse :** Client terminal interactif (TUI) pour Kubernetes, navigation rapide, logs temps réel, actions courantes sans longues commandes kubectl.

### 21. Différence entre intégration continue, livraison continue et déploiement continu ?
`🟢 Débutant` · Sujet : **DevOps**

**Réponse :** CI : chaque commit est construit et testé automatiquement. Continuous Delivery : chaque build validé est déployable, la mise en production reste une décision humaine. Continuous Deployment : tout build validé part automatiquement en production. La maturité des tests conditionne le passage d'un niveau à l'autre.

### 22. Quelles sont les métriques DORA et à quoi servent-elles ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Quatre indicateurs de performance de livraison : fréquence de déploiement, lead time des changements, taux d'échec des changements, temps de rétablissement (MTTR). Elles mesurent à la fois vitesse et stabilité et servent à comparer objectivement l'amélioration d'une équipe plutôt que sa vélocité en points.

### 23. Qu'est-ce qu'un pipeline « as code » et quelles bonnes pratiques ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Le pipeline est versionné avec le code (`.gitlab-ci.yml`, workflow GitHub Actions, `Jenkinsfile`). Bonnes pratiques : étapes rapides en premier (lint, tests unitaires), cache des dépendances, jobs parallèles, images fixes par digest, secrets injectés par le runner, artefacts signés, templates réutilisables (includes, actions composites).

### 24. Qu'est-ce qu'un build reproductible et pourquoi est-il souhaitable ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Un build qui produit exactement le même artefact (même hash) à partir du même code, quelle que soit la machine ou l'heure. Il permet de vérifier qu'un binaire correspond bien à son code source (supply chain) et de cacher les builds. Requiert des versions figées, pas de timestamps, un ordre déterministe.

### 25. Différence entre un artefact « snapshot » et « release » (Maven/npm) ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Un snapshot (`1.2.0-SNAPSHOT`) est une version en cours, écrasable, résolue à la dernière publication. Une release est immuable : une fois publiée, on ne peut plus la remplacer. Les builds de production ne doivent dépendre que de releases pour être reproductibles.

### 26. Qu'est-ce que le versionnement sémantique (SemVer) ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** `MAJOR.MINOR.PATCH` : MAJOR pour les changements incompatibles, MINOR pour les ajouts compatibles, PATCH pour les corrections. Les plages `^1.2.0` (npm) ou `[1.2,2.0)` (Maven) s'appuient dessus. Les Conventional Commits (`feat:`, `fix:`, `BREAKING CHANGE`) permettent d'automatiser le calcul de version et le changelog (semantic-release).

### 27. Qu'est-ce qu'ArgoCD et comment se compare-t-il à Flux ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Les deux sont des opérateurs GitOps qui synchronisent l'état d'un cluster avec un dépôt Git. ArgoCD offre une UI riche, le multi-cluster, les ApplicationSets et le pattern App of Apps. Flux est plus modulaire (controllers Kustomize, Helm, notification), CLI-first et natif Kubernetes (CRDs). Le choix dépend surtout des préférences d'équipe.

### 28. Qu'est-ce que Jenkins et pourquoi migre-t-on souvent vers GitLab CI / GitHub Actions ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Jenkins est un serveur CI extensible par plugins avec pipelines Groovy. Ses points faibles : maintenance du serveur et des plugins, sécurité, configuration parfois hors Git. Les CI hébergées apportent le pipeline as code natif, des runners éphémères, une intégration plus étroite avec le dépôt et les merge requests.

### 29. Qu'est-ce qu'un runner éphémère et pourquoi est-ce important ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Un runner (agent CI) créé pour un job puis détruit (conteneur, Pod Kubernetes via l'executor Kubernetes de GitLab ou ARC pour GitHub). Il garantit un environnement propre, évite les fuites de secrets entre jobs et permet l'autoscaling. Le cache doit alors être externalisé (S3, registry).

### 30. Comment gérer le cache de dépendances dans une pipeline CI ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Clé de cache basée sur le hash du lockfile (`package-lock.json`, `pom.xml`), stockage distribué (S3/GCS), restauration en début de job. Distinguer cache (accélération, tolérant à la perte) et artefacts (résultats passés entre jobs). Pour Docker, utiliser BuildKit avec `--cache-from`/`--cache-to` vers la registry.

### 31. Qu'est-ce que Testcontainers et pourquoi l'utiliser en CI ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Une librairie qui démarre des conteneurs Docker (PostgreSQL, Kafka, Redis…) pendant les tests d'intégration et les détruit ensuite. On teste contre la vraie technologie plutôt que H2 ou des mocks, avec la même configuration en local et en CI (nécessite Docker-in-Docker ou un socket Docker sur le runner).

### 32. Qu'est-ce que Helmfile / ApplicationSet et le problème du déploiement multi-environnements ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Déployer la même application sur dev/staging/prod avec des variantes. Helmfile déclare un ensemble de releases Helm avec des values par environnement. ApplicationSet (ArgoCD) génère des Applications à partir de générateurs (liste de clusters, dossiers Git, pull requests), évitant la duplication de manifestes.

### 33. Qu'est-ce qu'un scan de secrets et quels outils utiliser ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Détection de credentials commités par erreur via des patterns et de l'entropie : gitleaks, trufflehog, GitHub Secret Scanning, GitLab Secret Detection. À exécuter en pre-commit et en CI, et associer à un processus de rotation immédiate car un secret commité est considéré compromis même après suppression de l'historique.

### 34. Qu'est-ce qu'un pre-commit hook et quelles vérifications y placer ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Un script exécuté avant chaque commit (framework `pre-commit`, husky/lint-staged en JS). On y place les vérifications rapides : formatage (Prettier, Spotless), lint, scan de secrets, validation de messages de commit (commitlint). Les vérifications lentes restent en CI pour ne pas ralentir les développeurs.

### 35. Qu'est-ce que Docker BuildKit et Buildx ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** BuildKit est le moteur de build moderne de Docker : exécution parallèle des stages, cache mount (`RUN --mount=type=cache`), secrets mount sans couche persistée, builds multi-architecture. Buildx est la CLI qui l'expose, notamment pour construire des images `linux/amd64` et `linux/arm64` en une commande.

### 36. Quelle stratégie pour des images Docker plus sûres et plus petites ?
`🔴 Avancé` · Sujet : **Outils DevOps**

**Réponse :** Images de base minimales (distroless, Alpine, Chainguard, Ubuntu chiseled), multi-stage, utilisateur non-root, pas de shell si inutile, dépendances figées, scan Trivy/Grype en CI, signature cosign, épinglage par digest et rebuild régulier pour intégrer les correctifs de sécurité de la base.

### 37. Qu'est-ce que Crossplane ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Un framework Kubernetes qui expose des ressources cloud (buckets, bases managées, VPC) comme des CRDs. Il permet de gérer l'infrastructure via kubectl/GitOps avec réconciliation continue, et de définir des abstractions (Compositions) pour offrir aux équipes une plateforme en self-service.

### 38. Qu'est-ce que Pulumi et en quoi diffère-t-il de Terraform ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Pulumi permet d'écrire l'infrastructure dans des langages généralistes (TypeScript, Python, Go, Java) avec boucles, tests unitaires et packages classiques, là où Terraform utilise le HCL déclaratif. Les deux gèrent un state et des providers ; Terraform a un écosystème plus large, Pulumi convient aux équipes de développeurs.

### 39. Qu'est-ce que le Platform Engineering et un Internal Developer Platform ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Une discipline consistant à construire une plateforme interne (golden paths, templates, self-service, portail comme Backstage) pour que les équipes produit déploient sans expertise infra profonde. Elle traite la charge cognitive du « you build it, you run it » en industrialisant les bonnes pratiques.

### 40. Qu'est-ce que le SRE et l'error budget ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Site Reliability Engineering applique l'ingénierie logicielle à l'exploitation. L'error budget est la marge d'indisponibilité tolérée par le SLO (99,9 % = ~43 min/mois) : tant qu'il reste du budget, on peut livrer rapidement ; s'il est consommé, la priorité passe à la fiabilité. Cela objective l'arbitrage entre vitesse et stabilité.

### 41. Qu'est-ce qu'un post-mortem « blameless » ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Une analyse d'incident centrée sur les causes systémiques et non sur les individus : chronologie, impact, causes racines (5 pourquoi), ce qui a bien fonctionné, actions correctives suivies. Sans culpabilisation, les équipes partagent honnêtement les faits, ce qui améliore réellement le système.

### 42. Qu'est-ce que le chaos engineering ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Injecter volontairement des pannes contrôlées (kill de Pods, latence réseau, saturation CPU) en production ou pré-production pour vérifier la résilience et découvrir les faiblesses avant qu'elles ne surviennent. Outils : Chaos Monkey, Litmus, Chaos Mesh, AWS Fault Injection Service. On part d'une hypothèse et d'un blast radius limité.

### 43. Qu'est-ce qu'un runbook et un playbook d'astreinte ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Un runbook décrit pas à pas comment diagnostiquer et résoudre une situation connue (redémarrer un consumer Kafka bloqué, purger un cache). Lié à chaque alerte, il réduit le MTTR et permet l'automatisation progressive (runbook automation). Le playbook couvre l'organisation de la réponse (rôles, communication, escalade).

### 44. Quelles stratégies de déploiement existent au-delà du blue-green et canary ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Rolling update (remplacement progressif, défaut Kubernetes), recreate (arrêt puis démarrage, simple mais interruption), shadow/dark launch (trafic dupliqué vers la nouvelle version sans impact utilisateur), A/B testing (routage par segment), et feature flags pour découpler déploiement et activation.

### 45. Comment gérer les migrations de base de données dans une pipeline de déploiement continu ?
`🔴 Avancé` · Sujet : **DevOps**

**Réponse :** Migrations versionnées (Flyway/Liquibase) exécutées avant ou au démarrage de la nouvelle version, toujours compatibles avec la version précédente (expand/contract) pour permettre rolling update et rollback. Éviter les migrations longues bloquantes ; les lancer comme job séparé (Kubernetes Job, hook Helm pre-upgrade) avec verrou pour éviter l'exécution concurrente.

### 46. Qu'est-ce que la « configuration drift » entre environnements et comment la limiter ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Des différences non maîtrisées entre dev, staging et prod (versions, variables, ressources) qui font qu'un bug n'apparaît qu'en production. Limiter : même artefact promu d'un environnement à l'autre, configuration externalisée et versionnée, IaC pour tout, environnements éphémères par branche, et vérification de parité automatisée.

### 47. Qu'est-ce qu'un environnement éphémère (preview environment) ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Un environnement complet créé automatiquement pour chaque merge request (namespace Kubernetes, sous-domaine dédié) et détruit à sa fermeture. Il permet aux reviewers, QA et product de tester la fonctionnalité isolément. Outils : ArgoCD ApplicationSet pull request generator, GitLab Review Apps, Okteto.

### 48. Qu'est-ce que Make / Taskfile / just dans un projet et pourquoi standardiser les commandes ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** Un fichier de tâches (`make test`, `task build`) offre une interface unique pour les commandes courantes, identique en local et en CI. Cela réduit la documentation, évite les scripts divergents entre développeurs et rend l'onboarding plus rapide.

### 49. Qu'est-ce que le tag d'image « latest » et pourquoi l'éviter en production ?
`🟠 Intermédiaire` · Sujet : **Outils DevOps**

**Réponse :** `latest` est un tag mobile : il désigne l'image la plus récemment poussée sans ce tag explicite, donc non reproductible et trompeur. En production, utiliser des tags immuables (version SemVer, SHA du commit) et idéalement le digest `@sha256:...` ; configurer `imagePullPolicy` en conséquence.

### 50. Quels indicateurs suivre pour la santé d'une pipeline CI/CD elle-même ?
`🟠 Intermédiaire` · Sujet : **DevOps**

**Réponse :** Durée moyenne et p95 des pipelines, taux de réussite, taux de tests flaky, temps d'attente des runners, fréquence des reruns, coût par build. Une pipeline lente ou instable dégrade directement le lead time et la confiance des développeurs, donc elle mérite le même suivi qu'un service.
