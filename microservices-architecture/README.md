# 🧩 Microservices & Architecture Patterns

> Circuit Breaker, Saga, CQRS, Event Sourcing, gRPC, GraphQL, WebSockets

**50 questions**

---

### 1. Pattern "Circuit Breaker" ?
`🟢 Débutant` · Sujet : **Microservices**

**Réponse :** Empêche un service défaillant d'être sollicité en continu en "ouvrant le circuit" après échecs répétés, évitant la propagation en cascade.

### 2. Pattern Saga ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Gère les transactions distribuées via étapes locales avec compensation en cas d'échec, évitant un verrou ACID global.

### 3. Pattern "Database per Service" ?
`🟢 Débutant` · Sujet : **Microservices**

**Réponse :** Chaque microservice a sa propre base, garantissant couplage faible mais complexifiant cohérence des données.

### 4. Pattern Strangler Fig ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Remplace progressivement les fonctionnalités d'un monolithe par des microservices.

### 5. Architecture event-driven ?
`🟢 Débutant` · Sujet : **Microservices**

**Réponse :** Communication asynchrone via événements publiés sur un broker, réduisant le couplage temporel.

### 6. Idempotence entre microservices ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Une opération produit le même résultat qu'elle soit exécutée une ou plusieurs fois, crucial pour les retries.

### 7. Quelle est la différence fondamentale entre GraphQL et REST ?
`🟢 Débutant` · Sujet : **GraphQL**

**Réponse :** REST expose plusieurs endpoints fixes retournant des structures de données prédéfinies (souvent en sur- ou sous-récupération). GraphQL expose un point d'entrée unique où le client spécifie précisément les champs souhaités dans sa requête, évitant l'over-fetching et l'under-fetching.

### 8. Qu'est-ce que l'Event Sourcing et en quoi diffère-t-il du stockage d'état classique ?
`🟠 Intermédiaire` · Sujet : **Event Sourcing**

**Réponse :** Au lieu de stocker uniquement l'état actuel d'une entité, on stocke la séquence complète des événements ayant conduit à cet état. L'état courant est reconstruit en rejouant ces événements, offrant un historique complet, de l'auditabilité et la possibilité de revenir à un état antérieur.

### 9. Quels sont les avantages de gRPC par rapport à une API REST/JSON classique ?
`🟠 Intermédiaire` · Sujet : **gRPC**

**Réponse :** Utilise Protocol Buffers (format binaire compact et typé) au lieu de JSON texte, supporte nativement le streaming bidirectionnel via HTTP/2, et génère automatiquement du code client/serveur fortement typé à partir d'un fichier .proto, réduisant la latence et les erreurs de contrat.

### 10. Qu'est-ce que le pattern CQRS (Command Query Responsibility Segregation) ?
`🟠 Intermédiaire` · Sujet : **CQRS**

**Réponse :** Une approche séparant les opérations d'écriture (commands) des opérations de lecture (queries), permettant d'optimiser et de scaler indépendamment chaque côté, souvent combinée avec l'Event Sourcing.

### 11. Quelle est la différence entre WebSockets et Server-Sent Events (SSE) ?
`🟢 Débutant` · Sujet : **WebSockets**

**Réponse :** WebSockets est bidirectionnel full-duplex. SSE est unidirectionnel (serveur vers client), plus simple, utilise HTTP standard, adapté aux notifications ou flux d'événements.

### 12. Qu'est-ce qu'un "snapshot" dans un système à Event Sourcing ?
`🔴 Avancé` · Sujet : **Event Sourcing**

**Réponse :** Instantané périodique de l'état, évitant de rejouer tout l'historique des événements à chaque lecture, améliorant les performances pour un historique long.

### 13. Quels sont les quatre types de communication supportés par gRPC ?
`🟠 Intermédiaire` · Sujet : **gRPC**

**Réponse :** Unaire, streaming serveur, streaming client, streaming bidirectionnel.

### 14. Quels sont les avantages et inconvénients des microservices par rapport à un monolithe ?
`🟢 Débutant` · Sujet : **Microservices**

**Réponse :** Avantages : déploiements indépendants, scalabilité ciblée, autonomie des équipes, isolation des pannes, hétérogénéité technologique. Inconvénients : complexité distribuée (réseau, latence, cohérence), observabilité et tests plus difficiles, coût d'infrastructure, besoin de maturité DevOps. Un monolithe modulaire est souvent le bon point de départ.

### 15. Qu'est-ce qu'un monolithe modulaire et pourquoi est-il redevenu populaire ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Un déploiement unique dont le code est organisé en modules aux frontières explicites (packages, Spring Modulith, Java modules) communiquant par interfaces ou événements internes. Il offre la clarté des domaines sans les coûts opérationnels des microservices, et prépare une extraction ultérieure si un module doit scaler séparément.

### 16. Comment découper un système en microservices (bounded contexts, DDD) ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Partir du domaine métier : identifier les bounded contexts (langage ubiquitaire distinct, règles propres) via event storming, aligner un service sur un contexte et une équipe, minimiser les données partagées, et vérifier que la plupart des changements métier touchent un seul service. Découper par entité technique (« service User ») est l'anti-pattern classique.

### 17. Qu'est-ce que la loi de Conway et son « inverse » ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Une organisation produit des systèmes qui reflètent sa structure de communication. L'inverse Conway maneuver consiste à organiser les équipes (stream-aligned, autonomes, alignées sur un domaine) pour obtenir l'architecture souhaitée. Des microservices avec des équipes en silos par couche technique échouent.

### 18. Différence entre communication synchrone et asynchrone entre services ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Synchrone (REST, gRPC) : simple, réponse immédiate, mais couplage temporel (l'appelé doit être disponible) et cascades de pannes. Asynchrone (messages/événements) : découplage, résilience, mais cohérence éventuelle, débogage plus complexe, gestion des doublons et de l'ordre. Mixer les deux selon les besoins de chaque interaction.

### 19. Qu'est-ce que le pattern API Gateway et le BFF (Backend For Frontend) ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** L'API Gateway est le point d'entrée unique : routage, authentification, rate limiting, agrégation. Le BFF est une gateway dédiée à un type de client (web, mobile) qui adapte et agrège les appels aux besoins de cette UI, évitant des APIs génériques over-fetch/under-fetch et permettant à l'équipe front de posséder cette couche.

### 20. Qu'est-ce que le pattern Outbox transactionnel ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Pour publier un événement de façon fiable après une écriture en base, on insère l'événement dans une table `outbox` dans la même transaction que la donnée, puis un relais (polling ou Debezium/CDC) le publie vers Kafka et le marque envoyé. Cela évite la double écriture non atomique (base OK mais Kafka KO, ou l'inverse).

### 21. Qu'est-ce que le Change Data Capture (Debezium) ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Le CDC lit le journal de transactions de la base (WAL, binlog) et émet chaque changement de ligne comme événement Kafka, sans modifier l'application. Cas d'usage : outbox, réplication vers un cache/Elasticsearch, migration strangler, alimentation de vues CQRS, audit.

### 22. Différence entre chorégraphie et orchestration dans une Saga ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Chorégraphie : chaque service réagit aux événements des autres et publie les siens ; pas de point central mais le flux global est difficile à suivre. Orchestration : un coordinateur (Camunda, Temporal, Step Functions) pilote les étapes et les compensations ; plus lisible et observable, au prix d'un composant central. Orchestrer dès que la saga dépasse 3-4 étapes.

### 23. Qu'est-ce qu'une transaction compensatoire ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Dans une saga, l'inverse métier d'une étape déjà commitée (annuler une réservation, rembourser un paiement) exécutée quand une étape ultérieure échoue. Elle ne restaure pas nécessairement l'état exact (un email envoyé ne se retire pas), d'où l'importance de concevoir les étapes irréversibles en dernier.

### 24. Comment gérer la cohérence des données sans transactions distribuées (2PC) ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Accepter la cohérence éventuelle : sagas avec compensations, outbox pour les événements fiables, idempotence des consommateurs, réconciliation périodique, et conception des invariants métier à l'intérieur d'un seul agrégat/service. Le 2PC (XA) est évité car bloquant et fragile aux pannes du coordinateur.

### 25. Qu'est-ce que le pattern « API Composition » et ses limites ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Un service ou la gateway interroge plusieurs services et joint les résultats en mémoire pour répondre à une requête. Simple, mais coûteux pour les jointures volumineuses et dépendant de la disponibilité de tous. Pour les requêtes complexes, CQRS avec une vue matérialisée alimentée par événements est préférable.

### 26. Comment versionner une API et gérer les changements cassants ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Ne casser que si nécessaire : ajouter des champs plutôt que renommer (tolerant reader), déprécier avec un délai. Si rupture : version dans l'URL (`/v2/`) ou dans un header/media type, faire coexister les versions, consumer-driven contracts pour connaître les usages réels, et supprimer l'ancienne version après migration des clients.

### 27. Qu'est-ce que la découverte de services et comment est-elle assurée dans Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Trouver dynamiquement l'adresse d'une instance de service. Hors Kubernetes : registre (Eureka, Consul) avec client-side load balancing. Dans Kubernetes, le DNS des Services et kube-proxy jouent ce rôle, rendant Eureka superflu ; un service mesh ajoute du routage fin.

### 28. Qu'est-ce qu'un service mesh (Istio, Linkerd) et que fournit-il ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Un proxy sidecar (Envoy) ou ambient devant chaque service, piloté par un plan de contrôle : mTLS automatique, retries/timeouts/circuit breaking déclaratifs, routage canary par poids, télémétrie uniforme (métriques, traces), politiques d'autorisation. Il sort ces préoccupations du code applicatif au prix d'une complexité et d'un surcoût de latence.

### 29. Comment propager le contexte (trace id, utilisateur, locale) entre services ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Via des headers standardisés : W3C `traceparent` pour le tracing (propagé automatiquement par Micrometer/OpenTelemetry), `Authorization` (token relayé ou échangé), headers custom pour tenant/locale. Pour Kafka, les headers de message jouent le même rôle. Éviter de propager des données sensibles ou volumineuses.

### 30. Qu'est-ce que le pattern « Anti-Corruption Layer » ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Une couche de traduction entre un service et un système externe ou legacy dont le modèle est différent ou de mauvaise qualité. Elle convertit les données et concepts vers le modèle du domaine, empêchant que le modèle externe ne « contamine » le code métier. Indispensable lors d'un strangler fig.

### 31. Comment gérer les timeouts en chaîne (timeout budget) ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Chaque appel doit avoir un timeout inférieur à celui de l'appelant, sinon l'appelant abandonne alors que l'appelé travaille encore. On propage un budget (deadline) via header/gRPC deadline, on additionne retries et timeouts, et on définit des timeouts par opération plutôt qu'un global. Sans cela, une lenteur en bout de chaîne sature tous les pools.

### 32. Qu'est-ce que le pattern « Backpressure » ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Un mécanisme par lequel un consommateur signale à un producteur de ralentir quand il ne suit plus, au lieu de laisser les files exploser. Présent dans Reactive Streams (`request(n)`), Kafka (pull-based, lag), gRPC flow control, et les systèmes réactifs Spring WebFlux. L'alternative est le shedding (rejeter les requêtes excédentaires).

### 33. Comment tester une architecture microservices ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Tests unitaires et d'intégration par service (Testcontainers), contract tests entre consommateurs et fournisseurs (Pact), tests de composant avec les dépendances simulées (WireMock), un petit nombre de tests E2E sur les parcours critiques, tests en production (canary, synthetic monitoring) et chaos engineering. Éviter l'environnement d'intégration partagé où tout doit tourner.

### 34. Qu'est-ce que l'observabilité spécifique aux microservices (traces, correlation) ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Sans tracing distribué, une requête traversant 10 services est impossible à déboguer. Il faut un trace id propagé partout, des logs structurés avec ce trace id, des métriques RED (Rate, Errors, Duration) par service et par endpoint, et une carte des dépendances (Jaeger/Tempo, Kiali). Les SLO se définissent au niveau du parcours utilisateur.

### 35. Qu'est-ce qu'un « distributed monolith » ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** L'anti-pattern où des microservices restent couplés : déploiements à synchroniser, base partagée, appels synchrones en chaîne, librairie de domaine partagée. On paie la complexité distribuée sans en avoir les bénéfices. Signes : un changement exige plusieurs PR coordonnées, une panne d'un service fait tomber les autres.

### 36. Comment synchroniser le modèle de lecture dans CQRS et gérer la cohérence éventuelle côté UI ?
`🟠 Intermédiaire` · Sujet : **CQRS**

**Réponse :** Le côté écriture publie des événements consommés par des projecteurs qui mettent à jour la vue de lecture (table dénormalisée, Elasticsearch, Redis). L'UI peut lire une donnée légèrement périmée : on l'atténue par mise à jour optimiste, attente de la version (`read-your-writes` via un numéro de version), ou affichage « en cours ».

### 37. CQRS implique-t-il nécessairement l'Event Sourcing ?
`🟠 Intermédiaire` · Sujet : **CQRS**

**Réponse :** Non. CQRS sépare simplement les modèles de commande et de requête ; ils peuvent partager une base relationnelle avec des DTO de lecture dédiés. L'Event Sourcing est un choix de persistance indépendant, souvent combiné à CQRS car le journal d'événements se prête mal aux requêtes directes.

### 38. Quels sont les inconvénients de l'Event Sourcing ?
`🟠 Intermédiaire` · Sujet : **Event Sourcing**

**Réponse :** Courbe d'apprentissage, requêtes impossibles sans projections, versionnement des événements (upcasting quand le schéma évolue), volume de stockage, complexité des corrections (on ne modifie pas le passé, on compense), difficulté de suppression pour le RGPD (crypto-shredding), et outillage encore spécialisé (Axon, EventStoreDB, Marten).

### 39. Comment gérer le RGPD et le droit à l'effacement avec un journal d'événements immuable ?
`🟠 Intermédiaire` · Sujet : **Event Sourcing**

**Réponse :** Crypto-shredding : les données personnelles de chaque événement sont chiffrées avec une clé propre à l'utilisateur ; supprimer la clé rend les données illisibles sans modifier le journal. Alternatives : stocker les données personnelles hors du journal (référence vers un store effaçable) ou anonymiser lors des projections.

### 40. Qu'est-ce que l'upcasting d'événements ?
`🟠 Intermédiaire` · Sujet : **Event Sourcing**

**Réponse :** Quand la structure d'un événement change, on ne réécrit pas l'historique : un upcaster transforme à la lecture les anciennes versions vers la nouvelle (ajout de champ par défaut, renommage). Les événements sont versionnés (`OrderCreatedV2`) et le code doit rester capable de lire toutes les versions passées.

### 41. Qu'est-ce que le problème N+1 en GraphQL et comment le résoudre avec DataLoader ?
`🟠 Intermédiaire` · Sujet : **GraphQL**

**Réponse :** Un resolver de champ appelé pour chaque élément d'une liste déclenche une requête par élément. DataLoader regroupe les identifiants demandés dans le même tick et exécute une seule requête batch (`WHERE id IN (...)`), avec cache par requête. Spring for GraphQL l'intègre via `@BatchMapping`.

### 42. Comment sécuriser une API GraphQL (profondeur, complexité, introspection) ?
`🟠 Intermédiaire` · Sujet : **GraphQL**

**Réponse :** Limiter la profondeur et la complexité des requêtes (coût par champ), timeout, désactiver l'introspection en production, persisted queries (liste blanche), rate limiting basé sur le coût, autorisation au niveau des resolvers et non seulement du endpoint, et masquer les erreurs internes.

### 43. Qu'est-ce qu'un schéma fédéré (Apollo Federation, GraphQL Federation) ?
`🟠 Intermédiaire` · Sujet : **GraphQL**

**Réponse :** Chaque microservice expose un sous-graphe GraphQL, et un routeur compose un supergraphe unifié : un type peut être étendu par plusieurs services (`@key`, entités). Le client interroge une seule API alors que la résolution est distribuée. C'est l'équivalent GraphQL de l'API Gateway avec composition.

### 44. Qu'est-ce qu'une subscription GraphQL ?
`🟠 Intermédiaire` · Sujet : **GraphQL**

**Réponse :** Une opération temps réel où le serveur pousse des événements au client (généralement via WebSocket, protocole graphql-ws). Elle complète query et mutation pour les notifications, chats, tableaux de bord. Côté serveur, elle s'appuie souvent sur un Publisher réactif (`Flux`) alimenté par un bus d'événements.

### 45. Qu'est-ce que Protocol Buffers et comment faire évoluer un schéma de façon compatible ?
`🟠 Intermédiaire` · Sujet : **gRPC**

**Réponse :** Un format binaire typé défini dans des fichiers `.proto` générant le code client/serveur. Règles d'évolution : ne jamais réutiliser ni changer un numéro de champ, ajouter des champs optionnels, réserver les numéros supprimés (`reserved`), ne pas changer les types. Les champs inconnus sont ignorés, ce qui assure la compatibilité ascendante et descendante.

### 46. Comment exposer un service gRPC aux navigateurs et gérer le load balancing ?
`🟠 Intermédiaire` · Sujet : **gRPC**

**Réponse :** Les navigateurs ne supportent pas HTTP/2 trailers : on utilise gRPC-Web via un proxy (Envoy) ou Connect. Le load balancing pose problème car HTTP/2 multiplexe sur une connexion persistante : un Service Kubernetes L4 envoie tout au même Pod ; il faut un LB L7 (Envoy, Linkerd) ou un client-side LB avec headless Service.

### 47. Comment gérer les erreurs, deadlines et retries en gRPC ?
`🟠 Intermédiaire` · Sujet : **gRPC**

**Réponse :** gRPC utilise des status codes standardisés (`NOT_FOUND`, `UNAVAILABLE`, `DEADLINE_EXCEEDED`) avec détails optionnels (`google.rpc.Status`). Le client fixe une deadline propagée aux appels aval ; les retries se configurent via service config (codes retriables, backoff). Les interceptors gèrent auth, logging et métriques.

### 48. Comment scaler des WebSockets sur plusieurs instances ?
`🟠 Intermédiaire` · Sujet : **WebSockets**

**Réponse :** Les connexions sont stateful : un message destiné à un utilisateur doit atteindre l'instance qui tient sa connexion. Solution : un broker pub/sub (Redis, Kafka, RabbitMQ/STOMP relay) auquel toutes les instances souscrivent, sticky sessions au load balancer pour le handshake, et gestion des reconnexions côté client avec reprise (identifiants de message).

### 49. Qu'est-ce que STOMP sur WebSocket avec Spring et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **WebSockets**

**Réponse :** STOMP est un protocole de messagerie texte (subscribe/send sur des destinations) qui structure les échanges WebSocket. Spring fournit `@MessageMapping`, un broker simple en mémoire ou un relais vers RabbitMQ/ActiveMQ, et `SimpMessagingTemplate` pour pousser. Utile pour les notifications et chats ; pour du simple push serveur→client, SSE suffit souvent.

### 50. Qu'est-ce qu'un « thundering herd » et le problème du retry storm ?
`🟠 Intermédiaire` · Sujet : **Microservices**

**Réponse :** Quand un service revient après une panne, tous les clients réessaient au même instant et le font retomber. Prévention : backoff exponentiel avec jitter, circuit breaker avec état half-open (laisser passer quelques requêtes), rate limiting côté client, et files avec lissage. Même logique pour l'expiration simultanée de caches.
