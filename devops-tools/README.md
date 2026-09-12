# 🛠️ DevOps Practices & Tooling

> CI/CD, SonarQube, Trivy, Renovate, Prometheus, Grafana, Backstage

**20 questions**

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
