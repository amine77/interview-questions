# ☁️ Cloud & AWS

> EC2, Lambda, S3, IAM, VPC, FinOps, serverless, cloud-native patterns

**150 questions**

---

### 1. Différence entre S3 et EBS ?
`🟢 Débutant` · Sujet : **AWS**

**Réponse :** S3 = stockage objet via API HTTP, adapté aux fichiers statiques à grande échelle. EBS = stockage bloc attaché à une instance EC2, comme un disque dur virtuel.

### 2. Différence Security Group / NACL ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Security Group = niveau instance, stateful. NACL = niveau sous-réseau, stateless, supporte règles de refus.

### 3. Différence EC2 / Lambda ?
`🟢 Débutant` · Sujet : **AWS**

**Réponse :** EC2 = VM persistante gérée. Lambda = serverless à la demande, facturé à l'exécution.

### 4. IAM et rôles IAM ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** IAM gère identités/permissions. Un rôle = permissions temporaires assignables à un service sans clés statiques.

### 5. Qu'est-ce qu'une VPC ?
`🟢 Débutant` · Sujet : **AWS**

**Réponse :** Réseau virtuel isolé avec sa propre plage IP, sous-réseaux, tables de routage.

### 6. Qu'est-ce qu'un Auto Scaling Group ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Ajuste automatiquement le nombre d'instances EC2 selon la charge.

### 7. Qu'est-ce qu'un "graceful shutdown" et pourquoi est-il important pour une application déployée sur Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready Java**

**Réponse :** Capacité d'une application à terminer proprement les requêtes en cours et libérer ses ressources avant l'arrêt. Sur Kubernetes, cela évite de couper des requêtes en cours lors d'un scaling down ou d'un déploiement, en écoutant le signal SIGTERM avant le SIGKILL.

### 8. Circuit Breaker pattern en environnement cloud-native (Resilience4j) ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Surveille les appels vers un service distant et ouvre le circuit après un taux d'échec, évitant de surcharger un service défaillant, avec half-open state pour tester la disponibilité.

### 9. Sidecar pattern en architecture cloud-native ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Conteneur auxiliaire déployé dans le même Pod fournissant des fonctionnalités transverses (proxy, logs) sans modifier le code principal.

### 10. Statelessness et scaling horizontal ?
`🟢 Débutant` · Sujet : **Cloud-ready**

**Réponse :** Application sans état de session en mémoire locale, stockant l'état externe (Redis). Permet de router vers n'importe quelle instance sans sticky session.

### 11. Connection pooling en environnement conteneurisé scalable ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Réutilise un ensemble limité de connexions DB, évitant la saturation lorsque de nombreuses instances scalent horizontalement.

### 12. Bulkhead pattern en résilience applicative ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Isole les ressources allouées à différents appels/dépendances, empêchant qu'une défaillance ne se propage à tout le système.

### 13. Health check superficiel vs profond ?
`🟢 Débutant` · Sujet : **Cloud-ready**

**Réponse :** Superficiel vérifie que le processus répond (liveness). Profond vérifie aussi les dépendances critiques (readiness).

### 14. Service mesh et problème résolu au-delà de Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Couche gérant la communication via sidecars (Istio, Linkerd), ajoutant mTLS, routage avancé, observabilité fine, résilience.

### 15. Quelle est la différence entre SQS et SNS ?
`🟢 Débutant` · Sujet : **AWS avancé**

**Réponse :** SQS (Simple Queue Service) est une file d'attente point-à-point : un message est consommé par un seul récepteur. SNS (Simple Notification Service) est un système pub/sub diffusant un message à plusieurs abonnés simultanément (souvent combiné avec SQS en fan-out).

### 16. Quels sont les principaux inconvénients d'une architecture serverless malgré ses avantages ?
`🟢 Débutant` · Sujet : **Serverless**

**Réponse :** Le cold start, la difficulté de débogage et de test local, le vendor lock-in potentiel, et des limites d'exécution (durée, mémoire).

### 17. Qu'est-ce que le FinOps et pourquoi est-il devenu important avec le cloud ?
`🟢 Débutant` · Sujet : **FinOps**

**Réponse :** Une pratique collaborative visant à optimiser et responsabiliser les coûts cloud en temps réel, via dashboards, alertes budgétaires et identification de ressources sous-utilisées.

### 18. Différence entre "showback" et "chargeback" ?
`🟠 Intermédiaire` · Sujet : **FinOps**

**Réponse :** Showback affiche les coûts à titre informatif. Chargeback refacture réellement ces coûts au budget de l'équipe.

### 19. Différence entre région, zone de disponibilité (AZ) et edge location ?
`🟢 Débutant` · Sujet : **AWS**

**Réponse :** Une région est une zone géographique isolée (eu-west-3 Paris). Elle contient plusieurs AZ, des datacenters distincts reliés à faible latence, sur lesquelles on répartit les ressources pour la haute disponibilité. Les edge locations sont les points de présence CloudFront/Route 53 pour le cache et le DNS au plus près des utilisateurs.

### 20. Différence entre RDS, Aurora et DynamoDB ?
`🟢 Débutant` · Sujet : **AWS**

**Réponse :** RDS : bases relationnelles managées (PostgreSQL, MySQL…) avec sauvegardes et multi-AZ. Aurora : moteur AWS compatible PostgreSQL/MySQL, stockage distribué sur 3 AZ, réplicas rapides, option Serverless v2. DynamoDB : base NoSQL clé-valeur/document entièrement managée, latence ms constante, scalabilité automatique, modèle de données à concevoir autour des accès.

### 21. Différence entre ALB, NLB et API Gateway ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** ALB : couche 7 (HTTP), routage par chemin/hôte, WebSocket, intégration WAF, cible ECS/EKS/Lambda. NLB : couche 4 (TCP/UDP), très haut débit, IP statique, latence minimale. API Gateway : gestion d'API managée (auth, throttling, clés d'API, transformation), pay-per-request, idéale devant Lambda ; plus chère à fort volume qu'un ALB.

### 22. Différence entre ECS, EKS et Fargate ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** ECS : orchestrateur de conteneurs propriétaire AWS, simple, intégré IAM. EKS : Kubernetes managé, portable, écosystème riche mais plus complexe. Fargate : mode « serverless » d'exécution de conteneurs pour ECS ou EKS, sans gérer d'instances EC2, facturé à la vCPU/mémoire consommée.

### 23. Qu'est-ce que CloudFront et comment l'utiliser avec S3 pour une SPA Angular ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** CloudFront est le CDN d'AWS. On héberge les fichiers statiques dans un bucket S3 privé, accessible uniquement via Origin Access Control, et on configure CloudFront avec un certificat ACM, la compression, et une règle de réponse d'erreur 403/404 → `index.html` (200) pour le routage côté client. L'invalidation du cache s'effectue au déploiement.

### 24. Qu'est-ce que Route 53 et quelles politiques de routage propose-t-il ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Le DNS managé d'AWS. Politiques : simple, pondérée (canary DNS), latence (région la plus proche), failover (avec health checks), géolocalisation, géoproximité, multi-valeur. Il gère aussi les domaines et les enregistrements alias vers ALB/CloudFront/S3.

### 25. Différence entre les classes de stockage S3 et le lifecycle ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Standard (accès fréquent), Intelligent-Tiering (bascule automatique), Standard-IA / One Zone-IA (accès rare, coût de récupération), Glacier Instant/Flexible/Deep Archive (archivage, récupération de minutes à heures). Une règle de lifecycle transite automatiquement les objets vers des classes moins chères puis les supprime.

### 26. Comment sécuriser un bucket S3 ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Bloquer l'accès public au niveau compte (`Block Public Access`), politiques de bucket au moindre privilège, chiffrement par défaut (SSE-S3 ou SSE-KMS), versioning et Object Lock pour l'immuabilité, journalisation des accès, et VPC endpoints pour éviter le transit par Internet. Servir le contenu public via CloudFront plutôt qu'un bucket public.

### 27. Qu'est-ce qu'une policy IAM et la différence entre identity-based et resource-based ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Un document JSON définissant `Effect`, `Action`, `Resource`, `Condition`. Une identity-based policy s'attache à un utilisateur/groupe/rôle ; une resource-based (bucket policy, KMS key policy) s'attache à la ressource et peut autoriser des principaux d'autres comptes. Un `Deny` explicite l'emporte toujours ; l'accès cross-compte exige les deux côtés.

### 28. Qu'est-ce que IRSA / Pod Identity sur EKS et pourquoi éviter les clés d'accès ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** IAM Roles for Service Accounts (ou EKS Pod Identity) associent un rôle IAM à un ServiceAccount Kubernetes via OIDC : le Pod obtient des credentials temporaires automatiquement rotatifs. On évite ainsi les access keys statiques dans des Secrets, avec un moindre privilège par workload.

### 29. Qu'est-ce qu'AWS Secrets Manager vs Parameter Store ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Parameter Store (SSM) stocke paramètres et secrets simples (SecureString via KMS), gratuit en standard. Secrets Manager ajoute la rotation automatique (RDS intégré), la réplication multi-région et une facturation par secret. Les deux s'intègrent avec Spring Cloud AWS pour injecter la configuration.

### 30. Différence entre CloudWatch Logs, Metrics et Alarms, et qu'est-ce que X-Ray ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** CloudWatch collecte les logs (groupes/flux, Logs Insights pour requêter), les métriques (natives et custom) et déclenche des alarmes (SNS, autoscaling). X-Ray est le service de tracing distribué. OpenTelemetry via l'ADOT collector permet de rester agnostique.

### 31. Qu'est-ce que CloudFormation / CDK et comment se comparent-ils à Terraform ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** CloudFormation est l'IaC native AWS (YAML/JSON, stacks, drift detection). CDK génère du CloudFormation depuis TypeScript/Java/Python avec des constructs de haut niveau. Terraform est multi-cloud, avec un state externe et un écosystème de providers plus vaste. Choisir selon le multi-cloud et les compétences de l'équipe.

### 32. Qu'est-ce qu'un VPC endpoint et pourquoi l'utiliser ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** Un point d'accès privé aux services AWS (S3, DynamoDB via gateway endpoint ; autres via interface endpoint/PrivateLink) sans passer par Internet ni NAT Gateway. Avantages : sécurité (trafic interne), réduction des coûts de NAT, latence. Les endpoints peuvent porter une policy restreignant les accès.

### 33. Différence entre NAT Gateway et Internet Gateway ?
`🟠 Intermédiaire` · Sujet : **AWS**

**Réponse :** L'Internet Gateway donne un accès bidirectionnel à Internet aux subnets publics (IP publique requise). La NAT Gateway permet aux instances de subnets privés de sortir vers Internet (mises à jour, APIs) sans être joignables de l'extérieur ; elle est facturée à l'heure et au Go, d'où l'intérêt des VPC endpoints.

### 34. Qu'est-ce que AWS Organizations, les SCP et une landing zone ?
`🟠 Intermédiaire` · Sujet : **AWS avancé**

**Réponse :** Organizations regroupe plusieurs comptes AWS avec facturation consolidée. Les Service Control Policies posent des garde-fous au niveau OU (interdire des régions, des services). Une landing zone (Control Tower) est un environnement multi-comptes préconfiguré : comptes de log/audit, réseau partagé, comptes par environnement.

### 35. Comment concevoir une architecture multi-AZ et multi-région, et quelles stratégies de DR ?
`🔴 Avancé` · Sujet : **AWS avancé**

**Réponse :** Multi-AZ : ALB + ASG sur plusieurs AZ, RDS multi-AZ, EKS avec nœuds répartis. Multi-région pour la DR selon RPO/RTO : backup & restore (heures), pilot light (base répliquée, compute minimal), warm standby (stack réduite active), active-active (Route 53 + Aurora Global/DynamoDB Global Tables). Coût croissant avec l'ambition.

### 36. Qu'est-ce qu'EventBridge et en quoi diffère-t-il de SNS/SQS ?
`🟠 Intermédiaire` · Sujet : **AWS avancé**

**Réponse :** EventBridge est un bus d'événements avec règles de filtrage sur le contenu, schémas, transformation et intégrations SaaS/AWS natives, adapté aux architectures event-driven inter-services. SNS est un pub/sub simple (fan-out), SQS une file point-à-point avec rétention. Un pattern courant : EventBridge/SNS → SQS → consommateur.

### 37. Qu'est-ce que Step Functions ?
`🟠 Intermédiaire` · Sujet : **AWS avancé**

**Réponse :** Un orchestrateur de workflows serverless défini en Amazon States Language (JSON) : enchaînement d'étapes Lambda/ECS/services AWS, branches, boucles, retries, timeouts, parallélisme et attente d'événements humains. Idéal pour les sagas et les processus longs, avec visualisation de chaque exécution.

### 38. Qu'est-ce que le cold start Lambda et comment le réduire pour Java ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** Le temps d'initialisation d'un nouvel environnement d'exécution (JVM, chargement des classes, initialisation Spring) avant de traiter la requête. Réductions : SnapStart (snapshot Firecracker après init), GraalVM native image, frameworks légers (Quarkus, Micronaut, Spring Cloud Function), moins de dépendances, Provisioned Concurrency, mémoire plus élevée (CPU proportionnel).

### 39. Quelles sont les limites Lambda à connaître ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** Durée max 15 minutes, mémoire 128 Mo à 10 Go, payload synchrone 6 Mo, `/tmp` 10 Go, package 250 Mo (ou image conteneur 10 Go), concurrence par compte (1 000 par défaut, ajustable), pas d'état entre invocations garanti. Ces limites orientent vers Step Functions ou ECS pour les traitements longs.

### 40. Comment gérer les erreurs et les retries avec Lambda et SQS ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** Une invocation SQS échouée renvoie le message dans la file après le visibility timeout, jusqu'à `maxReceiveCount` puis vers une Dead Letter Queue. Configurer le batch avec `ReportBatchItemFailures` pour ne rejouer que les messages en échec, rendre le handler idempotent, et surveiller la DLQ avec une alarme.

### 41. Qu'est-ce que le pattern « externalized configuration » et comment l'appliquer en cloud ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Séparer strictement le code (artefact unique) de la configuration qui varie par environnement : variables d'environnement, ConfigMap/Secrets, Parameter Store, Spring Cloud Config. L'application lit sa configuration au démarrage (ou à chaud via refresh), ce qui permet le « build once, deploy anywhere » du 12-factor.

### 42. Comment rendre une application Java résiliente aux redémarrages fréquents en cloud ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Démarrage rapide (lazy init, CDS/AppCDS, native), stateless (sessions dans Redis, fichiers dans S3), probes readiness/liveness distinctes, graceful shutdown avec `server.shutdown=graceful`, pas de tâches planifiées uniques sans verrou distribué (ShedLock), et reconnexion automatique aux dépendances.

### 43. Quelles options JVM configurer dans un conteneur ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready Java**

**Réponse :** `-XX:MaxRAMPercentage=75` plutôt que `-Xmx` fixe, `-XX:+UseContainerSupport` (défaut depuis JDK 10), choix du GC selon la charge (G1 par défaut, ZGC pour la faible latence, Serial pour les très petits conteneurs), `-XX:+ExitOnOutOfMemoryError` pour laisser Kubernetes redémarrer, et `-Djava.security.egd=file:/dev/./urandom`.

### 44. Qu'est-ce que le Class Data Sharing (CDS/AppCDS) et Project Leyden ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready Java**

**Réponse :** CDS pré-parse les classes dans une archive partagée mappée en mémoire au démarrage, réduisant le temps de boot de 20 à 40 % ; Spring Boot 3.3 le génère automatiquement (`-XX:AutoCreateSharedArchive`). Project Leyden (JDK 24+, AOT cache) va plus loin en conservant le profilage et le code compilé entre exécutions.

### 45. Qu'est-ce que le pattern Retry avec backoff exponentiel et jitter ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** En cas d'erreur transitoire, réessayer avec un délai croissant (100 ms, 200 ms, 400 ms…) plafonné, en ajoutant un aléa (jitter) pour éviter que tous les clients ne réessaient au même instant (thundering herd). Limiter le nombre de tentatives et ne retenter que les erreurs idempotentes (5xx, timeouts, pas 400).

### 46. Quelles pratiques concrètes pour réduire la facture cloud ?
`🟠 Intermédiaire` · Sujet : **FinOps**

**Réponse :** Rightsizing des instances et requests Kubernetes, arrêt des environnements hors heures ouvrées, Savings Plans/Reserved Instances pour la charge stable, Spot pour les charges tolérantes, lifecycle S3, suppression des volumes/IP orphelins, réduction des transferts inter-AZ et NAT, tagging obligatoire pour l'allocation des coûts, alertes de budget.

### 47. Différence entre instances On-Demand, Reserved, Savings Plans et Spot ?
`🟠 Intermédiaire` · Sujet : **FinOps**

**Réponse :** On-Demand : flexible, plein tarif. Reserved Instances : engagement 1 ou 3 ans sur un type précis, jusqu'à -72 %. Savings Plans : engagement sur un montant horaire, plus flexible (famille, région, Fargate/Lambda). Spot : capacité inutilisée jusqu'à -90 % mais interruptible avec 2 minutes de préavis, idéal pour le batch et les workers stateless.

### 48. Qu'est-ce que l'allocation des coûts par tags et pourquoi est-elle indispensable ?
`🟠 Intermédiaire` · Sujet : **FinOps**

**Réponse :** Les tags (`team`, `env`, `app`, `cost-center`) activés comme cost allocation tags permettent de ventiler la facture par équipe/produit dans Cost Explorer ou des outils comme Kubecost. Sans eux, impossible de responsabiliser les équipes ni d'identifier les gaspillages ; les imposer via des policies (SCP, OPA) évite les ressources non taguées.

### 49. Qu'est-ce que le pattern « strangler » appliqué à une migration vers le cloud ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Migrer progressivement : placer un routeur (ALB, API Gateway) devant le monolithe on-premise, extraire fonctionnalité par fonctionnalité vers des services cloud, basculer le trafic route par route, jusqu'à éteindre l'ancien système. Il limite le risque du « big bang » et permet de valider chaque étape en production.

### 50. Quelles sont les 6 R de la migration cloud ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready**

**Réponse :** Rehost (lift & shift), Replatform (petites optimisations, ex : passer à RDS), Repurchase (SaaS), Refactor/Re-architect (cloud-native, microservices), Retire (décommissionner), Retain (garder on-premise). Chaque application est classée selon sa valeur métier, sa criticité et son coût de migration.

### 51. Comment fonctionne l'évaluation d'une policy IAM (deny explicite, allow, SCP, resource policy, permission boundary) ?
`🟢 Débutant` · Sujet : **IAM**

**Réponse :** Par défaut tout est refusé ; un `Deny` explicite l'emporte toujours ; un `Allow` doit exister dans les identity policies ou la resource policy (pour un accès cross-account, les deux sont nécessaires) ; les SCP de l'organisation et les permission boundaries plafonnent ce qu'une identité peut obtenir ; les session policies restreignent encore lors d'un `AssumeRole`. Le Policy Simulator et IAM Access Analyzer aident à comprendre un refus.

### 52. Différence entre utilisateur IAM, rôle IAM, groupe et IAM Identity Center ?
`🟢 Débutant` · Sujet : **IAM**

**Réponse :** Utilisateur : identité permanente avec clés (à éviter pour les humains et les workloads). Groupe : ensemble d'utilisateurs partageant des policies. Rôle : identité temporaire assumée par un service, un utilisateur ou un compte externe via STS (credentials courts, pas de secret stocké). IAM Identity Center (ex SSO) fédère les humains depuis un IdP (Entra ID, Okta) vers des permission sets par compte : la pratique recommandée.

### 53. Qu'est-ce que STS `AssumeRole`, la trust policy et le confused deputy ?
`🟢 Débutant` · Sujet : **IAM**

**Réponse :** `AssumeRole` renvoie des credentials temporaires pour un rôle si la trust policy du rôle autorise le principal appelant et que ce principal a `sts:AssumeRole`. Pour un rôle assumé par un service tiers, ajouter un `ExternalId` dans la condition évite le « confused deputy » (un tiers utilisant son accès pour un autre client). `AssumeRoleWithWebIdentity` permet la fédération OIDC (GitHub Actions, Kubernetes) sans clés.

### 54. Comment donner à une application Java des credentials AWS sans clés en dur ?
`🟢 Débutant` · Sujet : **IAM**

**Réponse :** La chaîne de credentials du SDK v2 cherche successivement : variables d'environnement, profil, Web Identity token (IRSA/Pod Identity sur EKS), rôle de tâche ECS, profil d'instance EC2 (IMDSv2). En production, l'application reçoit toujours un rôle attaché à son compute ; les clés d'accès longues sont réservées aux cas sans alternative et tournées.

### 55. Quels types d'instances EC2 choisir et à quoi servent les familles (T, M, C, R, G) ?
`🟢 Débutant` · Sujet : **Compute**

**Réponse :** T (burstable, crédits CPU, dev/test et faibles charges), M (équilibré), C (calcul intensif), R (mémoire, bases et caches), G/P (GPU), I (stockage NVMe local). Suffixes : `g` pour Graviton (ARM, moins cher, très adapté à Java), `a` pour AMD, `n` pour réseau amélioré. Utiliser Compute Optimizer pour recommander la taille.

### 56. Comment fonctionne le cycle de vie d'un Auto Scaling Group (politiques, warm-up, lifecycle hooks, instance refresh) ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Politiques : target tracking (CPU 50 %, requêtes par cible ALB), step scaling, scheduled, predictive. `HealthCheckType: ELB` remplace les instances en échec applicatif ; le warm-up évite de compter les instances en démarrage ; les lifecycle hooks exécutent des actions à l'ajout/retrait (drain, backup de logs) ; l'instance refresh déploie une nouvelle AMI/launch template progressivement.

### 57. Différence entre ECS sur EC2, ECS sur Fargate et EKS : comment choisir ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** ECS : orchestrateur AWS simple (task definitions, services), intégré IAM/ALB, sans cluster à gérer avec Fargate (facturation par vCPU/mémoire de tâche). EKS : Kubernetes standard, portabilité et écosystème (Helm, operators), plus complexe et coûteux (control plane + nœuds ou Fargate). Choisir ECS/Fargate pour des équipes AWS-centrées cherchant la simplicité, EKS pour la portabilité, le multi-cloud ou des besoins Kubernetes spécifiques.

### 58. Comment déployer une application Spring Boot sur ECS Fargate (task definition, service, réseau) ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Image dans ECR, task definition (CPU/mémoire, conteneur, variables et secrets depuis Secrets Manager/Parameter Store, logs vers CloudWatch via awslogs, health check), rôle de tâche (accès S3/SQS) distinct du rôle d'exécution (tirer l'image, lire les secrets), service dans des sous-réseaux privés derrière un ALB (target group avec health check `/actuator/health`), déploiement rolling ou blue/green via CodeDeploy, autoscaling sur CPU ou requêtes par cible.

### 59. Quelles sont les spécificités d'EKS (add-ons, nœuds, réseau, mise à jour) ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Control plane managé, nœuds en managed node groups, Karpenter ou Fargate ; VPC CNI (une IP de VPC par Pod : planifier les plages, prefix delegation), add-ons gérés (CoreDNS, kube-proxy, EBS/EFS CSI), IRSA ou Pod Identity pour IAM, AWS Load Balancer Controller pour ALB/NLB, `aws-auth`/access entries pour l'authentification, et mises à jour de version tous les ~14 mois (support étendu payant).

### 60. Comment fonctionne Lambda en détail (modèle d'exécution, concurrence, versions, alias) ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Chaque invocation s'exécute dans un micro-VM (Firecracker) réutilisé tant qu'il est chaud ; la concurrence = nombre d'environnements simultanés (limite par compte, reserved/provisioned concurrency). Versions immuables et alias (`prod`) permettent le déploiement progressif (pondération, CodeDeploy canary). Configurer mémoire (proportionnelle au CPU), timeout, variables d'environnement chiffrées, et couches (layers) pour les dépendances.

### 61. Comment optimiser une Lambda Java (cold start, SnapStart, GraalVM, mémoire) ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Lambda SnapStart (Java 11+) restaure un snapshot de la JVM initialisée (cold start de secondes → centaines de ms) ; sinon GraalVM Native Image via runtime custom, réduire les dépendances (pas de Spring Boot complet, ou Spring Cloud Function/Micronaut/Quarkus), initialiser les clients SDK en dehors du handler, choisir 1-2 Go de mémoire (plus de CPU), Graviton (`arm64`), et provisioned concurrency pour les endpoints sensibles à la latence.

### 62. Différence entre invocation synchrone, asynchrone et par event source mapping pour Lambda ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Synchrone (API Gateway, ALB, appel direct) : l'appelant attend la réponse et gère les erreurs. Asynchrone (S3, SNS, EventBridge) : Lambda met en file, réessaie deux fois, puis destination d'échec/DLQ. Event source mapping (SQS, Kinesis, DynamoDB Streams, Kafka) : Lambda interroge la source par lots, avec batch size, fenêtre, `ReportBatchItemFailures` pour les échecs partiels, et concurrence maximale par file.

### 63. Qu'est-ce qu'AWS App Runner, Elastic Beanstalk et Lightsail, et quand les utiliser ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** App Runner : déployer un conteneur ou du code source avec autoscaling, HTTPS et déploiement automatique, sans gérer VPC/ALB : idéal pour des services web simples. Elastic Beanstalk : PaaS historique orchestrant EC2/ALB/ASG à partir d'un jar/war ; vieillissant. Lightsail : VPS simplifié pour de petits projets. Au-delà de la simplicité initiale, ECS/EKS offrent plus de contrôle.

### 64. Comment concevoir un VPC de production (sous-réseaux, tables de routage, multi-AZ, CIDR) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Un CIDR /16 non chevauchant avec les autres VPC/on-premise, sous-réseaux publics (ALB, NAT) et privés (compute) et isolés (bases) dans au moins deux ou trois AZ, tables de routage par type (public → IGW, privé → NAT par AZ pour éviter les coûts inter-AZ et les pannes), VPC endpoints pour S3/DynamoDB/ECR/Secrets Manager, flow logs activés, et IPAM pour gérer les plages à l'échelle de l'organisation.

### 65. Différence entre VPC peering, Transit Gateway et PrivateLink ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Peering : liaison 1-1 entre VPC (pas de transitivité, gestion en n²). Transit Gateway : hub central connectant des dizaines de VPC, VPN et Direct Connect avec tables de routage et segmentation (coût par attachement et Go). PrivateLink : exposer un service (NLB) à d'autres VPC/comptes via des endpoints privés sans routage réseau (modèle fournisseur/consommateur, idéal pour les APIs internes et SaaS).

### 66. Comment connecter un datacenter on-premise à AWS (VPN, Direct Connect) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Site-to-Site VPN : tunnels IPsec sur Internet, rapide à mettre en place, débit limité (~1,25 Gb/s par tunnel), latence variable. Direct Connect : liaison dédiée (1-100 Gb/s), latence stable, coût fixe, délai de mise en service de semaines ; combiner avec un VPN de secours. Client VPN pour l'accès des utilisateurs. Route via Transit Gateway pour desservir plusieurs VPC.

### 67. Comment fonctionne l'ALB en détail (listeners, règles, target groups, sticky sessions, WebSocket) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Listeners HTTP/HTTPS (certificats ACM, SNI multiples) avec règles ordonnées (host, path, header, query, IP source) vers des target groups (instances, IPs, Lambda, ECS tasks) ayant leur health check ; pondération pour le canary ; sticky sessions par cookie (à éviter avec un état externalisé) ; support HTTP/2, gRPC, WebSocket ; timeouts d'inactivité à aligner avec l'application ; logs d'accès vers S3 ; intégration WAF et Cognito/OIDC pour l'authentification au niveau du load balancer.

### 68. Qu'est-ce que Global Accelerator et quand le préférer à CloudFront ou Route 53 ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Deux IPs anycast statiques qui routent le trafic TCP/UDP via le réseau AWS vers l'endpoint régional le plus sain et le plus proche, avec failover en secondes : adapté aux APIs non cacheables, jeux, VoIP, ou quand des IPs fixes sont exigées (allow-lists). CloudFront cache et accélère le HTTP ; Route 53 fait du routage DNS (soumis aux TTL).

### 69. Comment fonctionnent les VPC Flow Logs, Reachability Analyzer et le diagnostic réseau AWS ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Flow Logs (VPC, sous-réseau, ENI) enregistrent les métadonnées des flux (accepté/rejeté) vers CloudWatch/S3 : premier outil pour un « timeout » (règle de security group ou NACL manquante). Reachability Analyzer simule un chemin entre deux ressources et indique le composant bloquant. Compléter avec `nc`/`curl` depuis une instance/Pod, les logs ALB et les métriques des NAT Gateway (port allocation errors).

### 70. Comment fonctionne S3 en détail (cohérence, versioning, lifecycle, multipart, performance) ?
`🟠 Intermédiaire` · Sujet : **Stockage**

**Réponse :** Cohérence forte lecture après écriture depuis 2020 ; versioning pour se protéger des suppressions (avec MFA delete) ; lifecycle pour transitions de classes et expiration (incluant les multipart incomplets) ; multipart upload obligatoire au-delà de 5 Go et recommandé dès 100 Mo (parallélisme, reprise) ; débit par préfixe très élevé (3 500 PUT / 5 500 GET par seconde par préfixe, scalable), S3 Transfer Acceleration et byte-range GET pour les gros objets.

### 71. Comment gérer les accès S3 : bucket policies, ACLs, Block Public Access, URLs présignées, Access Points ?
`🟠 Intermédiaire` · Sujet : **Stockage**

**Réponse :** Block Public Access activé par défaut au niveau compte ; les ACLs sont désactivées (`BucketOwnerEnforced`) ; les bucket policies gèrent les accès cross-account et les conditions (VPC endpoint, TLS obligatoire, chiffrement) ; URLs présignées pour un accès temporaire (upload/download depuis le navigateur) ; Access Points pour des politiques par application ; Object Lambda pour transformer à la volée. Auditer avec Access Analyzer et Macie pour les données sensibles.

### 72. Différence entre EBS gp3, io2, st1 et comment choisir pour une base de données ?
`🟠 Intermédiaire` · Sujet : **Stockage**

**Réponse :** gp3 : SSD à IOPS/débit configurables indépendamment de la taille (3 000 IOPS de base, jusqu'à 16 000), le défaut économique. io2 Block Express : IOPS élevées et durabilité 99,999 % pour les bases critiques. st1/sc1 : HDD pour le débit séquentiel (logs, big data). Un volume est mono-AZ : snapshots réguliers (incrémentaux, vers S3) et, pour la haute disponibilité, réplication applicative ou services managés.

### 73. Qu'est-ce qu'EFS et FSx, et quand les utiliser plutôt que S3 ou EBS ?
`🟠 Intermédiaire` · Sujet : **Stockage**

**Réponse :** EFS : NFS managé, multi-AZ, accessible par plusieurs instances/conteneurs simultanément (partage de fichiers, contenu CMS, PVC `ReadWriteMany` sur EKS), performance élastique mais latence supérieure à EBS. FSx : systèmes de fichiers spécialisés (Windows SMB, Lustre pour le HPC, NetApp ONTAP, OpenZFS). S3 pour les objets, EBS pour un disque de bloc mono-instance.

### 74. Comment concevoir RDS/Aurora pour la production (Multi-AZ, réplicas, paramètres, maintenance) ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** Multi-AZ (standby synchrone avec failover automatique en 1-2 min ; Aurora en quelques secondes avec réplicas dans plusieurs AZ), read replicas pour la lecture (asynchrone), parameter groups versionnés (équivalent de `postgresql.conf`), fenêtre de maintenance et mises à jour mineures automatiques, sauvegardes automatiques avec PITR (rétention jusqu'à 35 jours) et snapshots manuels, Performance Insights et Enhanced Monitoring activés, chiffrement KMS et IAM database authentication.

### 75. Quelles sont les spécificités d'Aurora (stockage distribué, Serverless v2, Global Database, cluster endpoints) ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** Stockage partagé répliqué six fois sur trois AZ, auto-extensible ; jusqu'à 15 réplicas avec lag de ms ; endpoints writer/reader (répartition automatique) et custom ; Serverless v2 (scaling fin en ACU, adapté aux charges variables) ; Global Database (réplication inter-régions < 1 s, failover managé) ; Aurora Limitless pour le sharding managé ; RDS Proxy pour mutualiser les connexions (Lambda). Coût plus élevé que RDS mais performance et disponibilité supérieures.

### 76. Comment modéliser des données dans DynamoDB (single-table design, clés, index) ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** Concevoir à partir des patterns d'accès : partition key (distribution uniforme, éviter les hot partitions) et sort key (requêtes par plage, hiérarchies `ORDER#2025#...`), GSI pour les requêtes alternatives (coût d'écriture supplémentaire, cohérence éventuelle), LSI créés à la création de la table. Le single-table design regroupe plusieurs entités avec des clés génériques (`PK`, `SK`) pour éviter les jointures. Pas de requêtes ad hoc : prévoir les accès ou exporter vers un entrepôt.

### 77. Comment fonctionnent la capacité, les transactions, TTL, Streams et DAX dans DynamoDB ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** Capacité on-demand (facturation par requête, pics absorbés) ou provisionnée avec autoscaling (moins chère à charge stable). Transactions ACID sur jusqu'à 100 items (`TransactWriteItems`). TTL supprime automatiquement les items expirés (gratuit). DynamoDB Streams + Lambda pour réagir aux changements (CDC, agrégats). DAX : cache en mémoire compatible API pour les lectures à latence microseconde. Global tables pour le multi-région actif-actif.

### 78. Qu'est-ce qu'ElastiCache (Redis/Valkey, Memcached) et MemoryDB, et comment les configurer ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** ElastiCache Redis/Valkey : cache et structures de données, mode cluster (sharding) ou réplication avec failover multi-AZ, sans persistance garantie ; serverless disponible. Memcached : cache simple multi-thread sans réplication. MemoryDB : Redis-compatible durable (journal multi-AZ) utilisable comme base primaire. Prévoir TLS, AUTH/IAM auth, taille des nœuds selon la mémoire, et les métriques d'éviction et de CPU.

### 79. Quelles autres bases managées AWS connaître (DocumentDB, Neptune, Timestream, Keyspaces, OpenSearch) ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** DocumentDB : compatible MongoDB API (pas MongoDB). Neptune : graphe (Gremlin, SPARQL, openCypher). Timestream : séries temporelles. Keyspaces : compatible Cassandra serverless. OpenSearch Service : recherche et analytics (fork d'Elasticsearch), avec option serverless. Redshift : entrepôt colonnaire. Choisir selon le modèle de données et vérifier le niveau de compatibilité réel avec les bibliothèques clientes.

### 80. Comment configurer SQS correctement (visibility timeout, DLQ, long polling, FIFO, dédoublonnage) ?
`🟠 Intermédiaire` · Sujet : **Messagerie**

**Réponse :** Visibility timeout ≥ temps de traitement max (sinon redélivrance en double), DLQ avec `maxReceiveCount` et alarme, long polling (`WaitTimeSeconds=20`) pour réduire les appels vides, batch de 10 messages, FIFO pour l'ordre par `MessageGroupId` et dédoublonnage par `MessageDeduplicationId` (fenêtre de 5 min, débit limité mais high throughput mode), chiffrement SSE-KMS, et consommateurs idempotents. Redrive de la DLQ vers la source après correction.

### 81. Comment fonctionnent SNS (fan-out, filtres, FIFO) et le pattern SNS → SQS ?
`🟠 Intermédiaire` · Sujet : **Messagerie**

**Réponse :** SNS publie vers plusieurs abonnés (SQS, Lambda, HTTP, e-mail, SMS, Kinesis Firehose) ; les filter policies par attribut ou corps évitent que chaque abonné filtre lui-même ; SNS FIFO → SQS FIFO conserve l'ordre. Le pattern SNS → SQS par consommateur découple les producteurs, permet des retries et DLQ par consommateur, et l'ajout d'abonnés sans modifier le producteur. Penser aux resource policies des files pour autoriser SNS.

### 82. Comment concevoir une architecture événementielle avec EventBridge (bus, règles, schémas, archive, Pipes, Scheduler) ?
`🟠 Intermédiaire` · Sujet : **Messagerie**

**Réponse :** Bus par domaine (ou le bus par défaut pour les événements AWS), règles avec patterns de contenu vers des cibles (Lambda, Step Functions, SQS, API destinations avec authentification), Schema Registry pour découvrir et générer les types, archive + replay pour rejouer des événements, Pipes pour connecter source → enrichissement → cible sans code, Scheduler pour des invocations planifiées à grande échelle. Latence de ~0,5 s et limites de débit à vérifier.

### 83. Différence entre Kinesis Data Streams, Kinesis Firehose et Amazon MSK ?
`🟠 Intermédiaire` · Sujet : **Messagerie**

**Réponse :** Data Streams : streaming ordonné par shard, rétention jusqu'à un an, consommateurs multiples (KCL, Lambda, Flink), mode on-demand ou provisionné par shards. Firehose : ingestion sans gestion vers S3/Redshift/OpenSearch avec transformation et buffering (pas de consommateurs personnalisés). MSK : Kafka managé (ou MSK Serverless), écosystème Kafka complet (Connect, Streams), plus de contrôle et de coût opérationnel. Choisir Kinesis pour l'intégration AWS native, MSK pour la compatibilité Kafka.

### 84. Comment consommer SQS et publier SNS depuis Spring Boot (Spring Cloud AWS) ?
`🟠 Intermédiaire` · Sujet : **Messagerie**

**Réponse :** `spring-cloud-aws-starter-sqs` : `@SqsListener("queue")` avec conversion JSON, acquittement configurable (`ON_SUCCESS`), concurrence, `SqsTemplate` pour envoyer ; `spring-cloud-aws-starter-sns` : `SnsTemplate`. Credentials via la chaîne du SDK (rôle de tâche/IRSA), endpoints LocalStack en local et Testcontainers en test. Gérer l'idempotence et les DLQ comme avec Kafka.

### 85. Comment concevoir une API serverless (API Gateway + Lambda) et quelles différences entre REST API et HTTP API ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** HTTP API : moins cher, plus rapide, JWT authorizer natif, CORS, suffisant pour la plupart des cas. REST API : fonctionnalités avancées (API keys et usage plans, validation de requêtes, transformation de mapping, WAF, caching, endpoints privés). Ajouter : authorizers Lambda ou Cognito, throttling, stages avec variables, logs d'accès, et intégrations directes vers SQS/DynamoDB/Step Functions sans Lambda quand possible.

### 86. Comment orchestrer des workflows avec Step Functions (Standard vs Express, patterns, erreurs) ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** Standard : longue durée (1 an), exactly-once, historique complet, facturé par transition. Express : court (5 min), haut débit, at-least-once, facturé par durée. Patterns : chaînage de Lambdas, `Map` pour le parallélisme (Distributed Map sur des millions d'items S3), `Parallel`, `Wait`, callbacks avec task token (attente d'une action humaine), retries/catch par état, intégrations SDK directes (plus de 200 services) sans Lambda. Idéal pour les sagas et les traitements longs.

### 87. Comment fonctionne Cognito (User Pools, Identity Pools, hosted UI) et ses limites ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** User Pools : annuaire d'utilisateurs avec authentification OIDC/OAuth2 (hosted UI, MFA, fédération sociale/SAML, triggers Lambda pour personnaliser), émettant des JWT validables par API Gateway/ALB/Spring. Identity Pools : échangent une identité (Cognito, Google, SAML) contre des credentials IAM temporaires pour accéder directement à S3/DynamoDB. Limites : personnalisation de l'UI, fonctionnalités entreprise (SCIM, passkeys arrivées tardivement), quotas ; alternatives : Keycloak, Auth0.

### 88. Qu'est-ce qu'AWS SAM, Serverless Framework et comment développer/tester en local (LocalStack) ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** SAM : extension CloudFormation pour Lambda/API/DynamoDB avec `sam build`, `sam local invoke/start-api`, `sam deploy` (pipeline, canary via CodeDeploy). Serverless Framework et CDK sont des alternatives. LocalStack émule les services AWS localement (S3, SQS, DynamoDB, Lambda) pour les tests d'intégration (Testcontainers LocalStack) ; garder aussi un environnement AWS de développement car l'émulation n'est pas parfaite (IAM, quotas).

### 89. Comment fonctionne KMS (CMK, clés gérées, enveloppe, rotation, grants, multi-région) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** KMS génère et protège des clés ; le chiffrement d'enveloppe utilise une data key chiffrée par la CMK (S3, EBS, RDS, Secrets Manager l'utilisent). Clés gérées par AWS (`aws/s3`) vs clés client (key policy contrôlant l'accès, rotation annuelle automatique, alias, grants pour des accès temporaires, clés multi-régions pour la DR). Le coût par requête et les quotas KMS peuvent surprendre sur des workloads massifs (utiliser le cache de data key du SDK).

### 90. Comment gérer les secrets en production (Secrets Manager, rotation, accès depuis ECS/EKS/Lambda) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Secrets Manager stocke, chiffre (KMS) et tourne automatiquement (Lambda de rotation ou rotation managée RDS), versionne et journalise l'accès ; les workloads y accèdent via leur rôle (injection dans ECS task definition `secrets`, External Secrets Operator sur EKS, extension Lambda avec cache). Parameter Store (SecureString) est gratuit pour les cas simples sans rotation. Ne jamais mettre de secrets dans les variables d'environnement en clair ni dans les images.

### 91. Quels services de détection et de conformité activer (GuardDuty, Security Hub, Config, Inspector, CloudTrail, Detective) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** CloudTrail (journal des appels API, multi-région, vers S3 avec intégrité), GuardDuty (détection de menaces sur CloudTrail/VPC Flow/DNS/EKS/S3), Security Hub (agrégation et standards CIS/FSBP), AWS Config (inventaire et règles de conformité, remédiation automatique), Inspector (vulnérabilités EC2/ECR/Lambda), Detective (investigation), Macie (données sensibles S3). Les activer au niveau organisation avec un compte délégué de sécurité.

### 92. Comment protéger une application web sur AWS (WAF, Shield, ACM, security groups)?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** WAF sur ALB/CloudFront/API Gateway avec managed rules (OWASP core, bad inputs, bots), règles de rate limiting et géo, mode count avant block ; Shield Standard (DDoS L3/L4 inclus) et Advanced pour les grands comptes ; certificats ACM gratuits renouvelés automatiquement ; security groups en allow-list stricte (ALB → app → base), pas d'IP publiques sur le compute, IMDSv2 obligatoire, et CloudFront devant l'ALB pour absorber et cacher.

### 93. Qu'est-ce qu'une landing zone (Control Tower), la structure multi-comptes et les SCP recommandées ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Control Tower déploie une organisation avec OUs (Security, Infrastructure, Workloads, Sandbox), comptes de log archive et d'audit, guardrails préventifs (SCP) et détectifs (Config), Account Factory pour créer des comptes standardisés. SCP typiques : interdire de quitter l'organisation, de désactiver CloudTrail/GuardDuty, de créer des ressources hors régions autorisées, d'utiliser le root. Un compte par application et par environnement isole le blast radius et les coûts.

### 94. Comment sécuriser les accès humains (SSO, MFA, break-glass, accès temporaires) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** IAM Identity Center avec IdP externe et MFA obligatoire, permission sets par rôle métier (lecture seule par défaut, administration élevée sur demande), pas d'utilisateurs IAM humains, root verrouillé avec MFA matériel et alertes sur son usage, procédure break-glass documentée et testée, accès aux instances via SSM Session Manager (pas de SSH/bastion ouvert), et revue périodique des accès (Access Analyzer unused access).

### 95. Comment utiliser CloudWatch efficacement (Logs Insights, metric filters, embedded metrics, dashboards, Contributor Insights) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Logs Insights pour requêter les logs (`fields`, `filter`, `stats`, `parse`) avec rétention définie par groupe (coût), metric filters ou Embedded Metric Format pour créer des métriques depuis les logs JSON, alarmes composites et détection d'anomalies, dashboards partagés, Contributor Insights pour les top-N (clients bruyants), et Synthetics (canaries) pour la surveillance externe. Exporter vers S3 pour l'archivage long terme.

### 96. Qu'est-ce que X-Ray, l'ADOT et comment tracer une application Java sur AWS ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** X-Ray fournit le tracing distribué et la carte des services ; l'AWS Distro for OpenTelemetry (ADOT) collecte traces et métriques via OTel (agent Java auto-instrumentation ou Micrometer Tracing) et les exporte vers X-Ray, CloudWatch ou Prometheus managé. Propagation via le header `X-Amzn-Trace-Id` (ALB, API Gateway, Lambda) et W3C. CloudWatch Application Signals automatise les SLO et les métriques dorées.

### 97. Comment mettre en place Prometheus et Grafana managés sur AWS ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Amazon Managed Service for Prometheus (AMP) stocke les métriques scrapées par un collecteur (ADOT, Prometheus agent sur EKS, ou le scraper managé) avec alert manager intégré ; Amazon Managed Grafana (AMG) s'authentifie via Identity Center et interroge AMP, CloudWatch, X-Ray, OpenSearch. Coût par échantillon ingéré et par utilisateur actif ; alternative auto-hébergée (kube-prometheus-stack) sur EKS.

### 98. Comment concevoir les alertes et l'astreinte sur AWS (SNS, Incident Manager, intégrations) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Alarmes CloudWatch basées sur des SLO (taux d'erreur, latence p99, saturation) et sur les signaux de santé AWS (Health Dashboard, événements EventBridge), notifiées via SNS vers PagerDuty/Opsgenie/Slack (Chatbot), Incident Manager pour les plans de réponse et runbooks (SSM Automation), et alertes de coût (Budgets, anomaly detection). Éviter les alarmes sur CPU seul ; alerter sur ce qui impacte l'utilisateur.

### 99. Comment structurer un projet CDK (stacks, constructs, environnements, tests) et quelles bonnes pratiques ?
`🟠 Intermédiaire` · Sujet : **IaC**

**Réponse :** Constructs L2/L3 réutilisables, stacks par cycle de vie (réseau, données, application), `Stage` par environnement avec des props typées, `cdk-nag` pour les règles de sécurité, tests unitaires (`Template.fromStack` assertions) et snapshots, `cdk diff` en PR, pipelines CDK (self-mutating) ou GitHub Actions avec OIDC, bootstrap par compte/région, et éviter les changements de logical ID qui recréent des ressources (`overrideLogicalId`, `RemovalPolicy.RETAIN` sur les données).

### 100. Terraform ou CDK/CloudFormation sur AWS : comment choisir et comment gérer l'état et la dérive ?
`🟠 Intermédiaire` · Sujet : **IaC**

**Réponse :** CloudFormation/CDK : natif, sans état à gérer, rollback automatique, mais propre à AWS et parfois en retard sur les nouveaux services. Terraform/OpenTofu : multi-cloud, écosystème de providers et modules, état à sécuriser (S3 + verrouillage DynamoDB ou état natif), plan explicite. Dérive : CloudFormation drift detection, `terraform plan` en CI, AWS Config. Une organisation choisit généralement un outil principal et interdit les modifications manuelles (SCP, alertes CloudTrail).

### 101. Quels services AWS pour le CI/CD (CodePipeline, CodeBuild, CodeDeploy, ECR) et comment les articuler avec GitHub Actions ?
`🟠 Intermédiaire` · Sujet : **CI/CD**

**Réponse :** CodeBuild exécute les builds (conteneurs, cache, rapports), CodeDeploy déploie sur EC2/ECS/Lambda (rolling, blue/green, canary avec rollback sur alarmes), CodePipeline orchestre (CodeCommit est déprécié pour les nouveaux clients). ECR stocke les images avec scan et lifecycle policies. Beaucoup d'équipes gardent GitHub Actions/GitLab CI pour le build et utilisent OIDC pour assumer un rôle AWS sans clés, puis déploient via CDK/Terraform ou CodeDeploy.

### 102. Comment sécuriser et optimiser ECR (scan, immutabilité, lifecycle, cache, réplication) ?
`🟠 Intermédiaire` · Sujet : **CI/CD**

**Réponse :** Tags immuables (interdire l'écrasement), scan à la poussée (basic ou enhanced via Inspector) avec blocage des CVE critiques en pipeline, lifecycle policies pour supprimer les images anciennes ou non taguées (coût), réplication cross-région/compte pour la DR, pull-through cache pour Docker Hub/ECR Public (limites de débit), et endpoints VPC pour tirer sans passer par le NAT (coût et sécurité).

### 103. Comment implémenter un déploiement blue/green ou canary sur ECS et Lambda ?
`🟠 Intermédiaire` · Sujet : **CI/CD**

**Réponse :** ECS : CodeDeploy avec deux target groups et un listener de test, bascule progressive (`Linear10PercentEvery1Minute`, `Canary10Percent5Minutes`), alarmes CloudWatch déclenchant le rollback, hooks Lambda pour les tests ; ou ECS native blue/green (2025). Lambda : alias avec pondération de versions et CodeDeploy, ou déploiement progressif SAM. Dans les deux cas, les métriques par version sont indispensables.

### 104. Comment concevoir une architecture 3-tiers hautement disponible sur AWS ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** CloudFront + WAF devant un ALB multi-AZ, compute en ASG/ECS dans des sous-réseaux privés répartis sur 3 AZ, RDS/Aurora Multi-AZ avec réplicas en lecture, ElastiCache pour les sessions et le cache, S3 pour les fichiers, SQS pour les traitements asynchrones, Route 53 avec health checks, secrets dans Secrets Manager, observabilité CloudWatch/X-Ray, et infrastructure en IaC. Chaque couche est stateless et redondante.

### 105. Comment concevoir une architecture serverless événementielle complète ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** API Gateway (ou ALB) → Lambda pour le synchrone, DynamoDB pour l'état, EventBridge/SNS/SQS pour découpler les traitements, Step Functions pour les workflows, S3 + événements pour les fichiers, Cognito pour l'identité, CloudFront pour le front statique, et X-Ray/CloudWatch pour l'observabilité. Points d'attention : idempotence partout, DLQ sur chaque consommateur, limites de concurrence, coût à haut débit constant (un conteneur peut être moins cher), tests d'intégration réels.

### 106. Comment appliquer le Well-Architected Framework (piliers, revues) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Six piliers : excellence opérationnelle, sécurité, fiabilité, performance, optimisation des coûts, durabilité. Le Well-Architected Tool guide une revue par questions, produit des risques élevés/moyens et un plan d'amélioration ; des lenses (serverless, SaaS, conteneurs) ajoutent des questions spécifiques. Utile avant une mise en production ou une migration, et périodiquement.

### 107. Comment concevoir le multi-tenant SaaS sur AWS (silo, pool, bridge) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Silo : infrastructure dédiée par tenant (isolation forte, coût élevé, via comptes ou stacks séparés). Pool : ressources partagées avec isolation logique (tenant_id, IAM avec session tags/ABAC, RLS, DynamoDB avec préfixe de clé), coût optimisé. Bridge : mélange selon les tiers de service. Points clés : onboarding automatisé, métriques et coûts par tenant, throttling par tenant, et isolation vérifiée par tests.

### 108. Comment concevoir la reprise après sinistre sur AWS (backup/restore, pilot light, warm standby, multi-site) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Par RTO/RPO croissants en exigence et coût : backup & restore (AWS Backup cross-région, IaC pour reconstruire, heures), pilot light (données répliquées, compute éteint, dizaines de minutes), warm standby (réplique réduite active, minutes), multi-site actif-actif (Route 53/Global Accelerator, Aurora Global, DynamoDB global tables, secondes). Tester les bascules régulièrement (game days) ; la plupart des workloads se contentent de multi-AZ + backups cross-région.

### 109. Qu'est-ce qu'AWS Backup et comment gérer les sauvegardes centralisées ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Un service centralisant les plans de sauvegarde (fréquence, rétention, copie cross-région/compte, vault lock immuable contre le ransomware) pour EBS, RDS, DynamoDB, EFS, S3, EC2, avec sélection par tags, rapports de conformité et restauration testée. Compléter par les snapshots automatiques natifs et documenter les procédures de restauration avec leur RTO.

### 110. Comment gérer les quotas de service et les limites API (throttling) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Chaque service a des quotas par compte/région (Lambda concurrency, EC2 vCPU, API rates) visibles dans Service Quotas, certains ajustables sur demande ; surveiller avec les métriques `ThrottledRequests` et Trusted Advisor ; implémenter le backoff exponentiel avec jitter dans les SDK (par défaut) et des files pour lisser ; répartir sur plusieurs comptes pour les workloads très larges. Demander les augmentations avant les événements de charge.

### 111. Comment analyser et prévoir les coûts (Cost Explorer, CUR, budgets, anomalies, tags) ?
`🟠 Intermédiaire` · Sujet : **Coûts**

**Réponse :** Cost Explorer pour l'analyse par service/compte/tag et les prévisions, le Cost and Usage Report (CUR) exporté vers S3/Athena pour l'analyse fine, Budgets avec alertes et actions, Cost Anomaly Detection, tags d'allocation obligatoires (équipe, application, environnement) appliqués par SCP/Config, et une revue mensuelle FinOps. Les coûts cachés fréquents : transfert de données, NAT Gateway, logs CloudWatch, snapshots oubliés, KMS.

### 112. Comment réduire les coûts de transfert de données et de NAT Gateway ?
`🟠 Intermédiaire` · Sujet : **Coûts**

**Réponse :** VPC endpoints (gateway pour S3/DynamoDB gratuits, interface pour les autres) pour éviter le NAT, compute et données dans la même AZ quand possible (trafic inter-AZ facturé), CloudFront devant S3/ALB (sortie moins chère et cache), compression, Direct Connect pour les gros volumes hybrides, ECR pull-through et cache d'images, et suivi par flow logs des plus gros émetteurs.

### 113. Quand utiliser Spot, Graviton et les Savings Plans, et comment les combiner ?
`🟠 Intermédiaire` · Sujet : **Coûts**

**Réponse :** Spot (jusqu'à 90 % moins cher, interruption avec préavis de 2 min) pour les workloads tolérants (batch, CI, workers Kubernetes avec Karpenter et PDB). Graviton (ARM) pour 20-40 % de gain sur la plupart des workloads Java/conteneurs. Savings Plans (Compute, flexibles) pour la base de charge stable, achetés après stabilisation. Combinaison typique : base en Savings Plans + pics en On-Demand/Spot, le tout en Graviton.

### 114. Comment construire un data lake sur S3 (Glue, Athena, Lake Formation, formats) ?
`🟠 Intermédiaire` · Sujet : **Données**

**Réponse :** S3 organisé par zones (raw, curated) en formats colonnaires (Parquet, Iceberg pour les tables transactionnelles), catalogue Glue Data Catalog (crawlers ou définitions), transformations Glue ETL/EMR/Spark ou Lambda, requêtes SQL Athena (paiement par données scannées : partitionner et compresser), Lake Formation pour les permissions fines (colonnes, lignes), et Redshift Spectrum/QuickSight pour l'analyse. Alimenter par Kinesis Firehose ou DMS/CDC.

### 115. Qu'est-ce qu'AWS DMS et comment migrer une base vers AWS avec un minimum d'interruption ?
`🟠 Intermédiaire` · Sujet : **Données**

**Réponse :** Database Migration Service copie les données (full load) puis applique le CDC en continu entre source et cible (homogène ou hétérogène avec le Schema Conversion Tool), permettant de basculer l'application avec quelques secondes d'arrêt une fois le lag nul. Prévoir : validation des données, index/contraintes recréés après le chargement, tests de performance sur la cible, et plan de rollback (réplication inverse).

### 116. Comment exposer des fichiers S3 aux utilisateurs de façon sécurisée et performante ?
`🟠 Intermédiaire` · Sujet : **Données**

**Réponse :** Jamais de bucket public : CloudFront avec Origin Access Control vers le bucket privé, signed URLs/cookies CloudFront pour le contenu restreint (ou URLs présignées S3 pour des accès ponctuels), cache et compression, TLS via ACM, WAF, et logs. Pour les uploads : URL présignée `PUT` ou POST policy générée par le backend avec contraintes (taille, type), puis événement S3 → traitement.

### 117. Comment traiter des fichiers volumineux ou de nombreux fichiers à l'arrivée sur S3 ?
`🟠 Intermédiaire` · Sujet : **Données**

**Réponse :** Événements S3 → SQS (buffer, retries, DLQ) → workers (Lambda pour < 15 min et petits fichiers, sinon ECS/Batch) ; pour des millions d'objets, S3 Batch Operations ou Step Functions Distributed Map ; lecture par range pour les gros fichiers ; S3 Inventory pour lister sans coûteux `ListObjects` ; idempotence par clé d'objet et version ; et S3 Event Notifications vers EventBridge pour des règles riches.

### 118. Comment migrer une application Java monolithique vers AWS étape par étape ?
`🟠 Intermédiaire` · Sujet : **Migration**

**Réponse :** Rehost d'abord (EC2 ou conteneur ECS avec la base sur RDS via DMS) pour réduire le risque, puis replatform (secrets, logs, ALB, autoscaling, S3 pour les fichiers, sessions dans ElastiCache), mesurer et optimiser les coûts, puis refactor progressif (strangler : extraire des services vers ECS/Lambda avec SQS/EventBridge) selon la valeur métier. Chaque étape est réversible et observée.

### 119. Qu'est-ce qu'AWS Migration Hub, Application Migration Service et le Migration Evaluator ?
`🟠 Intermédiaire` · Sujet : **Migration**

**Réponse :** Migration Evaluator estime les coûts à partir de l'inventaire existant ; Migration Hub centralise le suivi et la découverte (Application Discovery Service) ; Application Migration Service (MGN) réplique des serveurs entiers (lift-and-shift automatisé avec test et bascule) ; DMS pour les bases ; DataSync/Snow family pour le transfert de données volumineuses. Le programme MAP peut financer une partie de la migration.

### 120. Comment utiliser Systems Manager (Session Manager, Parameter Store, Run Command, Patch Manager, Automation) ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** Session Manager : shell sur les instances sans SSH ni IP publique, journalisé (remplace les bastions). Parameter Store : configuration hiérarchique. Run Command et State Manager : exécuter et maintenir des configurations à l'échelle. Patch Manager : fenêtres de patch automatisées. Automation : runbooks (documents) pour les opérations répétables (redémarrages, remédiations, création d'AMI). Nécessite l'agent SSM et un rôle d'instance.

### 121. Comment construire et maintenir des AMI (Image Builder, golden images, durcissement) ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** EC2 Image Builder pipeline : image de base (Amazon Linux 2023), composants (durcissement CIS, agents SSM/CloudWatch, JDK), tests, distribution multi-régions/comptes, et planification (reconstruction mensuelle pour les patchs). Les instances redéployées par instance refresh de l'ASG. Pour les conteneurs, le même principe s'applique aux images de base ECR.

### 122. Comment fonctionne le Health Dashboard, les événements planifiés et la gestion des pannes régionales ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** AWS Health signale les incidents et les maintenances planifiées (retrait d'instance, mise à jour RDS) par compte, avec événements EventBridge pour automatiser (drain avant retrait). En cas de panne régionale, seules les architectures multi-régions préparées basculent ; la plupart des services régionaux dépendent aussi d'us-east-1 pour certains plans de contrôle (IAM, CloudFront) : conserver des credentials et des procédures qui n'exigent pas d'appels de contrôle pendant l'incident.

### 123. Comment gérer les mises à jour majeures RDS/Aurora (PostgreSQL 14 → 16) sans risque ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** Tester sur un snapshot restauré ou un clone Aurora, vérifier les extensions et paramètres, utiliser la blue/green deployment RDS (réplique logique verte mise à jour puis bascule en moins d'une minute), planifier hors pic avec fenêtre de maintenance, valider les performances (plans modifiés) et prévoir le rollback (snapshot pré-migration). Les mises à jour mineures automatiques restent activées.

### 124. Comment diagnostiquer une application lente sur AWS méthodiquement ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** Partir de l'expérience utilisateur (CloudWatch RUM/Synthetics, latence ALB `TargetResponseTime` vs `ResponseTime`), puis descendre : X-Ray pour localiser le service/dépendance lent, métriques de saturation (CPU/mémoire ECS, throttling Lambda, connexions RDS et Performance Insights top SQL, latence DynamoDB et throttles, ElastiCache CPU/évictions), réseau (NAT saturé, cross-AZ), puis profiling applicatif. Comparer avec un déploiement récent (CloudTrail, CodeDeploy).

### 125. Comment fonctionne ABAC avec les tags IAM et les session tags ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Les policies conditionnent l'accès par tags (`aws:ResourceTag/team` égal à `aws:PrincipalTag/team`), permettant une seule policy pour de nombreuses équipes et ressources ; les session tags transmis à l'`AssumeRole` (depuis l'IdP SAML/OIDC ou explicitement) portent le contexte (tenant, projet). Prérequis : gouvernance des tags (obligatoires, non modifiables par les utilisateurs via `aws:TagKeys` conditions).

### 126. Comment fonctionne IAM Access Analyzer et comment atteindre le moindre privilège ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Access Analyzer détecte les ressources accessibles depuis l'extérieur de la zone de confiance (S3, rôles, KMS, SQS), valide les policies (erreurs, bonnes pratiques) et génère une policy à partir de l'activité CloudTrail d'un rôle. Démarche : commencer restrictif, itérer avec les logs de refus (`AccessDenied` dans CloudTrail), revoir les permissions inutilisées (unused access findings), et automatiser ces contrôles en CI (cfn-nag, Checkov, cdk-nag).

### 127. Comment sécuriser les workloads conteneurisés sur AWS (ECS/EKS) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Images minimales scannées et signées (Signer), rôles IAM par tâche/Pod distincts, réseau privé avec security groups par tâche (awsvpc) ou NetworkPolicies, secrets injectés depuis Secrets Manager, read-only root filesystem et non-root, GuardDuty Runtime Monitoring, logs centralisés, limites de ressources, et sur EKS : Pod Security Standards, RBAC minimal, mise à jour régulière des versions et add-ons, endpoints d'API privés.

### 128. Qu'est-ce que Verified Access, Verified Permissions et Cedar ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Verified Access : accès zero-trust aux applications internes sans VPN, basé sur l'identité (IdP) et la posture de l'appareil, avec politiques Cedar. Verified Permissions : service d'autorisation fine (policies Cedar évaluées par API, schémas, intégration Cognito) pour externaliser les règles applicatives. Cedar est un langage de politiques open source, analysable et rapide, alternative à OPA/Rego dans l'écosystème AWS.

### 129. Comment fonctionne Route 53 en détail (zones privées, health checks, failover, ARC, Resolver) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Zones publiques et privées (associées à des VPC), enregistrements alias vers ALB/CloudFront/S3 (gratuits, sans TTL), politiques (simple, pondérée, latence, géo, geoproximity, failover, multivalue), health checks (endpoint, alarme, calculés) pilotant le failover, Application Recovery Controller pour des bascules contrôlées entre régions, Resolver endpoints (inbound/outbound) pour le DNS hybride, et DNS Firewall.

### 130. Comment fonctionne CloudFront en détail (behaviors, caching, origin failover, Functions, Lambda@Edge, OAC) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Distributions avec origines (S3 via OAC, ALB, API Gateway, custom) et behaviors par path (politiques de cache et de requête d'origine, TTL, compression, HTTP/3), origin groups pour le failover, invalidations, CloudFront Functions (JS léger, réécritures d'URL, headers) et Lambda@Edge (logique plus riche : A/B, authentification), signed URLs/cookies, géo-restriction, logs temps réel, et WAF/Shield intégrés. Idéal aussi pour les SPA Angular/React avec fallback vers `index.html`.

### 131. Comment exposer une API privée uniquement à l'intérieur du réseau d'entreprise ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** API Gateway REST privé avec resource policy limitant à un VPC endpoint `execute-api`, ou ALB interne dans les sous-réseaux privés joignable via VPN/Direct Connect/Transit Gateway, ou PrivateLink pour partager avec d'autres comptes. Route 53 zone privée pour les noms, certificats ACM privés (Private CA) si TLS interne, et security groups restreignant les sources.

### 132. Comment gérer IPv6 et l'épuisement d'IPv4 sur AWS (coût des IPv4 publiques) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Depuis 2024, chaque IPv4 publique est facturée : réduire (pas d'IP publique sur le compute, ALB/NAT partagés), passer les VPC en dual-stack, activer IPv6 sur ALB/CloudFront/EKS (mode IPv6 pour éviter l'épuisement d'IPs de Pods), et Public IP Insights pour l'inventaire. Les ressources internes n'ont pas besoin d'IPv4 publique.

### 133. Comment fonctionne AWS Batch et quand l'utiliser par rapport à ECS/Lambda ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Batch planifie des jobs conteneurisés (files, priorités, dépendances, array jobs) sur des environnements de calcul EC2/Spot/Fargate dimensionnés automatiquement : traitements longs, calcul scientifique, rendus, ETL lourds. Lambda pour < 15 min et petits volumes, ECS services pour les workloads permanents, Batch pour les jobs ponctuels ou massifs à optimiser en coût (Spot).

### 134. Comment déployer une application Spring Boot sur Lambda via Spring Cloud Function ou l'adaptateur serverless-java-container ?
`🟠 Intermédiaire` · Sujet : **Compute**

**Réponse :** Spring Cloud Function expose des `Function` beans invoquées par le handler AWS (`FunctionInvoker`), avec un contexte Spring minimal ; l'adaptateur serverless-java-container fait tourner une application Spring MVC complète derrière API Gateway (portabilité maximale, cold start plus long). Dans les deux cas : SnapStart, `spring.main.lazy-initialization`, exclusion des starters inutiles, et une fonction par responsabilité si la taille le permet.

### 135. Comment dimensionner et optimiser les connexions à RDS depuis Lambda et des conteneurs autoscalés ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** Les fonctions Lambda ou centaines de tâches ouvrent trop de connexions : RDS Proxy (pooling, multiplexage, failover plus rapide, IAM auth), ou PgBouncer auto-hébergé ; côté application, HikariCP petit et `max_connections` calculé ; surveiller `DatabaseConnections` ; et privilégier des accès groupés (SQS → worker avec pool stable) plutôt que des Lambdas concurrentes vers la base.

### 136. Comment implémenter le cache et les sessions d'une application Java sur AWS ?
`🟠 Intermédiaire` · Sujet : **Bases**

**Réponse :** Sessions : Spring Session avec ElastiCache Redis/Valkey (cluster mode selon la taille) ou jetons stateless ; cache applicatif : Caffeine local + ElastiCache distribué, ou DAX pour DynamoDB ; cache HTTP : CloudFront/API Gateway caching. Chiffrement in-transit, AUTH/IAM, alarmes sur les évictions et la mémoire, et tolérance à la panne du cache (dégradation).

### 137. Comment fonctionne Kinesis Data Streams avec Java (KCL, agrégation, checkpoints, resharding) ?
`🟠 Intermédiaire` · Sujet : **Données**

**Réponse :** Le Kinesis Client Library (KCL 3) répartit les shards entre workers avec un lease table DynamoDB, gère les checkpoints, le resharding et le failover ; le KPL agrège les petits enregistrements. Enhanced fan-out pour plusieurs consommateurs à faible latence. Dimensionner en shards (1 Mo/s écriture, 2 Mo/s lecture) ou en mode on-demand ; idempotence obligatoire (at-least-once).

### 138. Comment fonctionne Amazon MSK (provisionné, Serverless, Connect, IAM auth) et ses différences avec Kafka auto-hébergé ?
`🟠 Intermédiaire` · Sujet : **Données**

**Réponse :** MSK gère brokers, patchs et métriques (Prometheus/CloudWatch), avec stockage EBS ou tiered, authentification IAM (`aws-msk-iam-auth`) ou SASL/SCRAM/mTLS, MSK Connect pour Kafka Connect managé, MSK Serverless pour les charges variables (limites de partitions et de débit), et Schema Registry via Glue. On reste responsable des topics, ACLs, dimensionnement des partitions et de la configuration client.

### 139. Comment tester et déboguer des Lambdas et intégrations serverless ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** Tests unitaires du code métier hors handler, tests d'intégration contre de vraies ressources dans un compte de test (SAM `deploy` éphémère, CDK avec stacks par branche) ou LocalStack pour les services simples, logs structurés avec `requestId`, X-Ray, Lambda Powertools (Java : logging, tracing, métriques, idempotence, validation), `sam logs`/CloudWatch Live Tail, et tests de charge sur les quotas de concurrence.

### 140. Qu'est-ce que Lambda Powertools et le pattern d'idempotence serverless ?
`🟠 Intermédiaire` · Sujet : **Serverless**

**Réponse :** Une bibliothèque officielle (Java, Python, TS, .NET) fournissant logging structuré, tracing X-Ray, métriques EMF, validation de payload, gestion des paramètres, et l'utilitaire `@Idempotent` : la clé (hash du payload) est stockée dans DynamoDB avec l'état et le résultat, garantissant qu'une invocation dupliquée (retries SQS/EventBridge) renvoie le même résultat sans réexécuter les effets de bord.

### 141. Comment implémenter une saga et l'outbox avec les services AWS ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Orchestration : Step Functions avec états de compensation (`Catch` → rollback) et intégrations directes (DynamoDB, SQS, Lambda). Chorégraphie : EventBridge entre services, chaque service publiant ses événements. Outbox : DynamoDB Streams ou Aurora + DMS/Debezium vers EventBridge/Kinesis pour publier fiablement après commit. Idempotence via Powertools ou table de déduplication.

### 142. Comment concevoir un système de traitement de fichiers/ETL serverless à grande échelle ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** S3 (arrivée) → EventBridge → Step Functions Distributed Map (parallélisme sur des milliers d'objets, tolérance d'échec) → Lambda/ECS/Glue selon la durée, résultats en S3 Parquet + Glue Catalog, Athena pour la vérification, notifications SNS, et suivi dans DynamoDB. Contrôler la concurrence pour ne pas saturer les dépendances (bases, APIs), et prévoir le retraitement partiel.

### 143. Comment choisir entre API Gateway, ALB et un ingress EKS pour exposer des APIs ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** API Gateway : gestion d'API (clés, quotas, authorizers, WAF, caching, throttling, documentation), coût par requête élevé à fort volume, intégrations serverless. ALB : simple, économique à volume élevé, routage L7, authentification OIDC intégrée, pour ECS/EKS/EC2. Ingress/Gateway API sur EKS avec AWS Load Balancer Controller : contrôle Kubernetes-native, plus complexe. Souvent : ALB/EKS pour le trafic principal, API Gateway pour les APIs partenaires.

### 144. Comment estimer le coût d'une architecture avant de la construire ?
`🟠 Intermédiaire` · Sujet : **Coûts**

**Réponse :** AWS Pricing Calculator avec les hypothèses de trafic, stockage et transfert ; comparer les alternatives (Lambda vs Fargate au débit attendu, Aurora vs RDS, on-demand vs provisionné DynamoDB) ; inclure les postes cachés (NAT, logs, KMS, sorties, snapshots, support plan) ; ajouter 20-30 % de marge ; valider ensuite sur un prototype avec tags et Cost Explorer, et instaurer des budgets par environnement.

### 145. Quels sont les gaspillages les plus fréquents et comment les détecter automatiquement ?
`🟠 Intermédiaire` · Sujet : **Coûts**

**Réponse :** Instances sous-utilisées ou oubliées (Compute Optimizer, Trusted Advisor), volumes EBS non attachés et snapshots anciens, load balancers sans cibles, IPs élastiques non associées, NAT dans chaque AZ non nécessaire, logs CloudWatch sans rétention, environnements de dev actifs la nuit (Instance Scheduler), RDS surdimensionné (Performance Insights), DynamoDB provisionné sans autoscaling, et données S3 sans lifecycle. Automatiser via Config rules et rapports hebdomadaires.

### 146. Comment structurer les comptes et environnements pour une équipe produit (dev, staging, prod) ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** Un compte par environnement (isolation IAM et quotas, coûts visibles), infrastructure identique via IaC paramétré par environnement, données de prod jamais copiées sans anonymisation, accès prod restreints et audités, déploiements uniquement par pipeline (pas de console), sandboxes individuels avec budgets et nettoyage automatique (aws-nuke), et partage des ressources communes (ECR, réseau, DNS) via un compte infra et RAM.

### 147. Qu'est-ce que AWS RAM, les Service Catalog et les Landing Zone Accelerator ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** Resource Access Manager partage des ressources (sous-réseaux, Transit Gateway, Route 53 Resolver rules, licences, préfixes IPAM) entre comptes d'une organisation. Service Catalog publie des produits IaC approuvés (portfolio) que les équipes déploient en self-service avec contraintes. Landing Zone Accelerator (LZA) déploie une landing zone conforme (réglementaire) en IaC au-delà de Control Tower.

### 148. Comment obtenir de l'aide et suivre les bonnes pratiques (support plans, Trusted Advisor, re:Post, docs) ?
`🟠 Intermédiaire` · Sujet : **Exploitation**

**Réponse :** Support Developer/Business/Enterprise selon les SLA de réponse et l'accès aux TAM ; Trusted Advisor (Business+) pour les vérifications de coût, sécurité, limites et tolérance aux pannes ; AWS Health pour les incidents ; re:Post et la documentation (prescriptive guidance, whitepapers, Architecture Center) ; Well-Architected reviews avec un partenaire ; et suivre les annonces (What's New, re:Invent) pour les nouveaux services qui simplifient des architectures existantes.

### 149. Comment intégrer l'IA générative dans une application sur AWS (Bedrock, Knowledge Bases, Guardrails) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Amazon Bedrock donne accès à des modèles (Anthropic Claude, Amazon Nova, Llama, Mistral) via une API unifiée avec IAM, sans gérer d'infrastructure ; Knowledge Bases implémente le RAG managé (ingestion S3, embeddings, OpenSearch Serverless/pgvector), Agents pour l'appel d'outils, Guardrails pour filtrer contenus et données sensibles, et l'intégration Spring AI (`spring-ai-bedrock`). Points d'attention : coût par token, régions disponibles, quotas, et journalisation des invocations.

### 150. Quelles bonnes pratiques pour un projet AWS greenfield (checklist de démarrage) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Organisation multi-comptes avec Control Tower et SSO, IaC dès le premier jour avec pipeline et OIDC, tags obligatoires et budgets, réseau privé par défaut avec endpoints, secrets dans Secrets Manager, CloudTrail/GuardDuty/Config activés, chiffrement KMS partout, observabilité (logs structurés, métriques, traces, alarmes SLO), sauvegardes automatisées et testées, Well-Architected review avant la mise en production, et documentation d'architecture (diagrammes, ADR, runbooks).
