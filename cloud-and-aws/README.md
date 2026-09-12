# ☁️ Cloud & AWS

> EC2, Lambda, S3, IAM, VPC, FinOps, serverless, cloud-native patterns

**50 questions**

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
