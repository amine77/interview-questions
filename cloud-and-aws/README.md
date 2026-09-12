# ☁️ Cloud & AWS

> EC2, Lambda, S3, IAM, VPC, FinOps, serverless, cloud-native patterns

**18 questions**

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
