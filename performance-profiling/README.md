# ⚡ Performance & Profiling Backend

> JMH, JFR, async-profiler, HikariCP, caching multi-niveaux

**50 questions**

---

### 1. Quelle démarche suivre face à un problème de performance ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** Mesurer avant d'optimiser : définir l'objectif (latence p99, débit, coût), reproduire avec une charge réaliste, observer avec les métriques et un profileur pour localiser le goulot (base, réseau, CPU, GC, verrous), corriger une chose à la fois, mesurer à nouveau. L'intuition se trompe souvent ; le profileur, rarement.

### 2. Pourquoi regarder les percentiles (p95, p99) plutôt que la moyenne ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** La moyenne masque les valeurs extrêmes : un service à 50 ms en moyenne peut avoir un p99 à 2 s ressenti par 1 % des requêtes, souvent les plus importantes (gros clients). Avec plusieurs appels par page, la probabilité de toucher une latence p99 devient élevée. Les SLO s'expriment en percentiles ; les histogrammes Micrometer/Prometheus les calculent.

### 3. Quelles sont les causes les plus fréquentes de lenteur d'un backend Java ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** Par ordre de fréquence : requêtes SQL (N+1, index manquants, pagination absente), appels réseau séquentiels ou sans timeout, pools de connexions/threads sous-dimensionnés, sérialisation JSON excessive, GC mal configuré ou heap trop petit, verrous contendus, logs synchrones verbeux, et cache absent sur les données chaudes.

### 4. Qu'est-ce que la loi d'Amdahl et la loi de Little, et leur utilité ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Amdahl : le gain du parallélisme est borné par la part séquentielle (à 10 % séquentiel, max ×10 quel que soit le nombre de cœurs). Little : concurrence moyenne = débit × temps de réponse ; elle permet de dimensionner les threads et pools (100 rps × 0,2 s = 20 requêtes en cours) et de comprendre qu'augmenter la latence sature les pools.

### 5. Comment écrire un benchmark JMH correct ?
`🟠 Intermédiaire` · Sujet : **JMH**

**Réponse :** Classe avec `@State(Scope.Thread)`, méthodes `@Benchmark`, `@BenchmarkMode(Mode.AverageTime)`, `@OutputTimeUnit`, `@Warmup`/`@Measurement` (itérations), `@Fork(2+)`. Retourner le résultat ou l'injecter dans un `Blackhole` pour empêcher l'élimination de code mort ; passer les données par `@Param` ou champs non constants pour éviter le constant folding. Lancer via le plugin Maven/Gradle, jamais depuis l'IDE.

### 6. Quels sont les pièges classiques des microbenchmarks ?
`🟠 Intermédiaire` · Sujet : **JMH**

**Réponse :** Mesurer sans warm-up (interpréteur vs JIT), code mort éliminé, constantes repliées, données non représentatives (petites tailles tenant en cache CPU), boucle mesurée qui domine, effet d'ordre des tests, GC survenant pendant la mesure, et surtout extrapoler un micro-gain à une application dominée par les I/O. JMH corrige les premiers ; le jugement corrige le dernier.

### 7. Comment mesurer les allocations avec JMH ?
`🟠 Intermédiaire` · Sujet : **JMH**

**Réponse :** Le profileur `-prof gc` de JMH rapporte le taux d'allocation par opération (`gc.alloc.rate.norm` en octets/op) et le nombre de collections. Il révèle les allocations cachées (boxing, lambdas capturantes, itérateurs, `String.format`). Un code qui alloue zéro octet par opération dans une boucle chaude est une cible réaliste pour les chemins critiques.

### 8. Comment démarrer et exploiter un enregistrement JFR ?
`🟠 Intermédiaire` · Sujet : **JFR**

**Réponse :** Au lancement : `-XX:StartFlightRecording=duration=60s,filename=rec.jfr,settings=profile` ; à chaud : `jcmd <pid> JFR.start duration=60s filename=rec.jfr` ; en continu avec un buffer circulaire et `JFR.dump` à la demande. Analyser dans JDK Mission Control : vue « Method Profiling » (hot methods), « Garbage Collections », « Lock Instances », « Allocations », « Exceptions », « File/Socket I/O ». La ligne de commande `jfr print --events` extrait des événements.

### 9. Quels événements JFR sont les plus utiles en diagnostic ?
`🟠 Intermédiaire` · Sujet : **JFR**

**Réponse :** `jdk.ExecutionSample` (CPU par pile), `jdk.ObjectAllocationSample` (qui alloue), `jdk.JavaMonitorEnter`/`ThreadPark` (contention et attentes), `jdk.GarbageCollection`/`GCHeapSummary`, `jdk.SocketRead`/`FileRead` (I/O lents), `jdk.ExceptionThrow` (exceptions cachées), `jdk.ThreadStart`, `jdk.VirtualThreadPinned`. Les événements personnalisés (`jdk.jfr.Event`) ajoutent le contexte métier.

### 10. Comment créer un événement JFR personnalisé ?
`🟠 Intermédiaire` · Sujet : **JFR**

**Réponse :** Étendre `jdk.jfr.Event` avec des champs annotés (`@Label`, `@Name`), instancier, `begin()`, remplir, `commit()`. L'événement apparaît dans JMC avec durée et pile, sans coût si désactivé. Utile pour tracer des opérations métier (traitement d'une commande) et les corréler avec GC, verrous et I/O sur la même ligne de temps.

### 11. Qu'est-ce qu'async-profiler et pourquoi est-il plus précis que les profileurs classiques ?
`🟠 Intermédiaire` · Sujet : **async-profiler**

**Réponse :** Un profileur par échantillonnage utilisant `AsyncGetCallTrace` et `perf_events` : il n'attend pas les safepoints (le biais qui fait attribuer le temps aux mauvaises lignes), voit le code natif et le noyau, et a un surcoût très faible. Modes : `cpu`, `wall` (temps d'horloge, inclut les attentes), `alloc`, `lock`, `itimer`. Sortie en flame graph HTML ou format collapsed.

### 12. Comment lire un flame graph ?
`🟠 Intermédiaire` · Sujet : **async-profiler**

**Réponse :** Chaque rectangle est une frame ; la largeur représente la part d'échantillons (temps), la hauteur la profondeur de pile ; l'axe horizontal n'est pas le temps. Chercher les « plateaux » larges au sommet (fonctions où le temps est réellement passé) et remonter pour comprendre qui les appelle. Comparer deux profils avec un flame graph différentiel. Le mode `wall` révèle les attentes I/O invisibles en mode CPU.

### 13. Comment profiler dans un conteneur Kubernetes ?
`🟠 Intermédiaire` · Sujet : **async-profiler**

**Réponse :** Copier async-profiler dans l'image ou un conteneur éphémère partageant le namespace de processus (`kubectl debug --share-processes`), autoriser `perf_events` (`kernel.perf_event_paranoid`, capabilité `SYS_PTRACE`/`SYSLOG`), lancer `./asprof -d 30 -e cpu -f /tmp/p.html <pid>` puis récupérer le fichier. Alternative sans privilèges : JFR, ou le profilage continu (Pyroscope, Datadog, Elastic Universal Profiling).

### 14. Qu'est-ce que le profilage continu (continuous profiling) ?
`🟠 Intermédiaire` · Sujet : **async-profiler**

**Réponse :** Collecter en permanence des profils à faible surcoût sur toutes les instances de production (Pyroscope/Grafana, Parca, Datadog Profiler) et les stocker avec des labels (service, version, Pod). On peut ainsi comparer avant/après un déploiement, trouver la régression exacte, et lier un pic de latence à une pile d'appels sans reproduire le problème.

### 15. Comment dimensionner le pool de connexions HikariCP ?
`🟠 Intermédiaire` · Sujet : **HikariCP**

**Réponse :** Contrairement à l'intuition, un pool petit est souvent plus rapide : formule de départ `cœurs_db × 2 + disques effectifs` (une dizaine pour la plupart des services), puis ajuster selon les métriques (`hikaricp.connections.pending`, temps d'attente). Un pool surdimensionné crée de la contention côté base. Avec les virtual threads, le pool devient la limite de concurrence effective : dimensionner et instrumenter en conséquence.

### 16. Quels paramètres HikariCP faut-il connaître ?
`🟠 Intermédiaire` · Sujet : **HikariCP**

**Réponse :** `maximumPoolSize`, `minimumIdle` (préférer égal au max pour un pool fixe), `connectionTimeout` (attente d'une connexion, 30 s par défaut, souvent trop long : 1-5 s pour échouer vite), `idleTimeout`, `maxLifetime` (inférieur au timeout du serveur/du load balancer, ~30 min), `keepaliveTime`, `leakDetectionThreshold` (alerte si une connexion n'est pas rendue), `validationTimeout`.

### 17. Comment diagnostiquer « Connection is not available, request timed out » ?
`🟠 Intermédiaire` · Sujet : **HikariCP**

**Réponse :** Le pool est vide : soit la charge dépasse la capacité (temps d'attente `pending` élevé, requêtes lentes qui gardent les connexions : optimiser les requêtes ou augmenter prudemment), soit des fuites (connexions jamais fermées : activer `leakDetectionThreshold`, vérifier les try-with-resources et les transactions longues), soit la base est saturée. Les métriques Micrometer `hikaricp.*` et les logs de la base tranchent.

### 18. Pourquoi les transactions longues sont-elles néfastes pour le pool et la base ?
`🟠 Intermédiaire` · Sujet : **HikariCP**

**Réponse :** Une transaction ouverte garde une connexion du pool et des verrous en base pendant toute sa durée, y compris pendant des appels HTTP ou des traitements CPU si `@Transactional` englobe trop. Cela réduit la concurrence disponible et provoque timeouts et deadlocks. Réduire la portée transactionnelle au strict accès aux données ; `spring.jpa.open-in-view=false` évite de garder la session pendant le rendu.

### 19. Comment identifier les requêtes lentes ?
`🟠 Intermédiaire` · Sujet : **Base de données**

**Réponse :** Logs de requêtes lentes de la base (`log_min_duration_statement` PostgreSQL, `slow_query_log` MySQL), `pg_stat_statements` (temps total par requête normalisée, le meilleur point de départ), APM avec spans SQL (temps par requête et nombre par transaction, détectant le N+1), et `EXPLAIN (ANALYZE, BUFFERS)` sur les candidates pour voir le plan réel : scans séquentiels, estimations fausses, tris sur disque.

### 20. Comment lire un plan d'exécution `EXPLAIN ANALYZE` ?
`🟠 Intermédiaire` · Sujet : **Base de données**

**Réponse :** Comparer lignes estimées et réelles (écart → statistiques obsolètes, `ANALYZE`), repérer les `Seq Scan` sur grandes tables (index manquant ou non utilisable), les `Nested Loop` sur gros volumes, les tris et hash sur disque (`work_mem`), et le temps par nœud. L'ordre des colonnes d'un index composite et les fonctions appliquées aux colonnes (`lower(email)`) déterminent son utilisation.

### 21. Quelles optimisations JPA/Hibernate ont le plus d'impact ?
`🟠 Intermédiaire` · Sujet : **Base de données**

**Réponse :** Éliminer le N+1 (`JOIN FETCH`, `@EntityGraph`, `@BatchSize`), projections DTO pour les lectures, pagination avec `Slice` quand le count est inutile, `hibernate.jdbc.batch_size` + `order_inserts/updates` pour les écritures en masse, `@Transactional(readOnly=true)`, éviter `FetchType.EAGER`, `StatelessSession` pour les imports, cache de second niveau uniquement sur les données de référence, et logs `hibernate.generate_statistics` pour compter les requêtes par transaction.

### 22. Qu'est-ce que le caching multi-niveaux et pourquoi l'adopter ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** Superposer plusieurs caches à latence croissante : cache local en mémoire (Caffeine, nanosecondes, par instance), cache distribué (Redis, ~1 ms, partagé), puis la base. Le local absorbe les données ultra-chaudes et protège Redis ; le distribué évite le recalcul par chaque instance. Compromis : cohérence entre instances (invalidation par message pub/sub ou TTL court sur le local).

### 23. Comment implémenter un cache à deux niveaux avec Spring ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** Un `CacheManager` composite : Caffeine en premier niveau (TTL court, taille bornée), Redis en second ; à la lecture, chercher L1 puis L2 puis la source, en remplissant vers le haut ; à l'écriture, invalider L2 et publier un message (Redis pub/sub, Kafka) pour que chaque instance invalide son L1. Des bibliothèques (JetCache, Redisson near cache, Hazelcast near cache) fournissent ce pattern.

### 24. Comment configurer Caffeine efficacement ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** `maximumSize` ou `maximumWeight` (jamais illimité), `expireAfterWrite` (données à fraîcheur bornée) ou `expireAfterAccess` (données chaudes), `refreshAfterWrite` avec un `CacheLoader` pour rafraîchir en arrière-plan sans bloquer (early refresh), `recordStats()` exposé via Micrometer (taux de hit, évictions). L'algorithme W-TinyLFU offre un meilleur taux de hit que LRU.

### 25. Qu'est-ce que le cache stampede (dogpile) et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** À l'expiration d'une entrée très demandée, des centaines de requêtes recalculent simultanément la même valeur et saturent la base. Solutions : verrou ou single-flight (une seule requête recalcule, les autres attendent ou servent l'ancienne valeur), `refreshAfterWrite` (rafraîchissement anticipé), TTL avec jitter pour désynchroniser les expirations, et pré-chargement des clés critiques.

### 26. Quelles stratégies d'invalidation de cache ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** TTL (simple, tolère une obsolescence bornée), invalidation explicite à l'écriture (`@CacheEvict`, précise mais couplée), invalidation par événements (CDC/Debezium ou événements métier vers les caches), versionnement des clés (`user:v2:{id}`), et write-through. Combiner TTL de sécurité et invalidation explicite : le TTL rattrape les invalidations manquées.

### 27. Comment mesurer l'efficacité d'un cache ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** Taux de hit (objectif souvent > 90 % pour les données de référence), latence des hits vs misses, taille et évictions (évictions élevées = cache trop petit), fraîcheur, et surtout l'impact sur la cible (baisse des requêtes vers la base). Un cache avec un faible taux de hit ajoute de la latence et de la complexité pour rien.

### 28. Quels pièges avec Redis en cache distribué ?
`🟠 Intermédiaire` · Sujet : **Cache**

**Réponse :** Grosses valeurs (sérialisation coûteuse, bande passante), clés sans TTL (mémoire qui gonfle), commandes O(N) bloquantes (`KEYS`, `SMEMBERS` sur de gros sets : Redis est mono-thread), hot keys saturant un nœud du cluster, absence de timeout côté client (Lettuce/Jedis), et panne de Redis qui doit dégrader (cache-aside avec fallback) et non faire tomber l'application.

### 29. Comment choisir et régler le GC pour la latence ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Objectif de pauses faibles : G1 avec `-XX:MaxGCPauseMillis` réaliste, ou ZGC générationnel (`-XX:+UseZGC -XX:+ZGenerational`, par défaut générationnel en Java 23+) pour les heaps de plusieurs Go et des pauses < 1 ms, au prix de CPU supplémentaire. Donner assez de heap (les GC concurrents ont besoin de marge), surveiller le temps GC et les pauses via JFR et les métriques `jvm.gc.*`.

### 30. Comment régler le GC pour le débit (batch) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Parallel GC (`-XX:+UseParallelGC`) maximise le débit avec des pauses longues acceptables, un heap large (`-Xms` = `-Xmx` pour éviter les redimensionnements), et éventuellement un jeune espace plus grand (`-Xmn`) si les objets meurent jeunes. Vérifier que le temps total en GC reste faible (< 5 %) et que les full GC sont rares.

### 31. Quels indicateurs JVM surveiller en production ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Temps et fréquence GC, taille des générations après collecte (tendance = fuite), heap utilisé vs max, metaspace, threads actifs et bloqués, pools (HikariCP, executors), taux d'allocation, code cache, latences des endpoints en percentiles, CPU du processus, et OOM/redémarrages. Micrometer expose `jvm.*`, `process.*`, `hikaricp.*`, `executor.*` vers Prometheus/Grafana.

### 32. Comment diagnostiquer une latence intermittente (spikes) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Corréler les spikes avec les pauses GC (logs `-Xlog:gc*` avec timestamps), les compilations JIT au démarrage, les déoptimisations, les safepoints longs (`-Xlog:safepoint`), la contention de verrous (JFR), les timeouts réseau ou base, les CPU throttling en conteneur (limites CPU basses : métriques `container_cpu_cfs_throttled_seconds`), et les voisins bruyants. Un profil `wall` sur la fenêtre du spike est décisif.

### 33. Quel impact des limites CPU Kubernetes sur une JVM ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Une limite CPU (`limits.cpu`) déclenche du throttling CFS dès que le quota par période (100 ms) est consommé, même si la moyenne est basse, allongeant les latences et les pauses GC ; la JVM dimensionne aussi ses threads GC/JIT sur ce nombre de cœurs. Bonnes pratiques : `requests` réalistes, limites CPU généreuses ou absentes, `-XX:ActiveProcessorCount` si besoin, et surveiller le throttling.

### 34. Comment optimiser la sérialisation JSON ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Réutiliser un `ObjectMapper` unique (coûteux à créer), éviter `@JsonView`/introspection excessive, désactiver `FAIL_ON_UNKNOWN_PROPERTIES` si pertinent, utiliser des DTO plats plutôt que des graphes d'entités, `@JsonInclude(NON_NULL)`, streaming (`JsonParser`) pour les gros documents, et considérer Jackson Blackbird/afterburner ou des formats binaires (Protobuf) entre services quand le JSON domine le profil CPU.

### 35. Comment réduire la latence des appels réseau sortants ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Timeouts courts et explicites (connexion, lecture), pools de connexions HTTP réutilisés (keep-alive), HTTP/2 quand possible, parallélisation des appels indépendants (`CompletableFuture.allOf`, virtual threads), agrégation d'appels (batch endpoints), cache des réponses stables, compression, et proximité réseau (même zone). Instrumenter chaque dépendance pour connaître sa contribution à la latence.

### 36. Comment optimiser le logging ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Les logs synchrones sur disque ou console sont un goulot fréquent : niveau INFO en production, éviter la construction de messages coûteux (paramétrage `{}` ou `isDebugEnabled`), appender asynchrone (Logback `AsyncAppender`, Log4j2 async avec disruptor), format JSON produit une seule fois, et échantillonnage des logs très fréquents. Mesurer : le logging peut représenter 10-20 % du CPU d'un service verbeux.

### 37. Comment gérer les traitements lourds sans dégrader les requêtes utilisateur ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Les sortir du chemin de requête : file de messages et workers dédiés, pools de threads séparés (bulkhead) pour isoler les ressources, priorisation, et retour immédiat (202 + suivi). Pour les calculs CPU intensifs dans le même processus, limiter le parallélisme (`ForkJoinPool` dédié) pour laisser des cœurs aux requêtes interactives.

### 38. Quand utiliser la programmation réactive (WebFlux) pour la performance ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Quand la charge est dominée par des I/O concurrentes très nombreuses avec peu de CPU par requête (gateways, streaming, agrégation d'appels). Elle réduit les threads mais complexifie le code et le débogage, et une seule opération bloquante ruine les gains. Depuis Java 21, les virtual threads offrent une scalabilité comparable avec du code impératif : c'est souvent le meilleur rapport gain/complexité.

### 39. Comment optimiser le temps de démarrage d'une application Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Mesurer avec `spring.main.lazy-initialization` (à utiliser prudemment), le `BufferingApplicationStartup` et Actuator `/startup` pour voir les étapes lentes ; réduire le scan de composants et l'auto-configuration inutile (`spring.autoconfigure.exclude`), CDS/AppCDS, Spring AOT (`spring-boot:process-aot`) qui précalcule la configuration, et GraalVM Native Image pour un démarrage en dizaines de millisecondes (serverless).

### 40. Comment concevoir un test de charge réaliste ?
`🟠 Intermédiaire` · Sujet : **Tests de charge**

**Réponse :** Définir des scénarios représentatifs (mix de requêtes, données variées, pas une seule clé chaude), monter la charge progressivement (ramp-up) jusqu'à l'objectif puis au-delà pour trouver le point de rupture, durée suffisante pour voir GC et fuites (soak test), environnement proche de la production, et observer côté serveur (CPU, pools, GC, base) pas seulement les temps côté client. Outils : Gatling, k6, JMeter, Locust.

### 41. Qu'est-ce que le coordinated omission et pourquoi fausse-t-il les mesures ?
`🟠 Intermédiaire` · Sujet : **Tests de charge**

**Réponse :** Quand l'outil de charge attend la réponse avant d'envoyer la suivante (boucle fermée), les périodes lentes génèrent moins de requêtes et sont sous-représentées dans les percentiles : les latences réelles vues par des utilisateurs arrivant à rythme constant sont bien pires. Utiliser un modèle en boucle ouverte (taux d'arrivée fixe : Gatling `constantUsersPerSec`, k6 `constant-arrival-rate`, wrk2) ou un outil corrigeant le biais.

### 42. Comment interpréter les résultats d'un test de charge ?
`🟠 Intermédiaire` · Sujet : **Tests de charge**

**Réponse :** Tracer débit, latence percentiles et erreurs en fonction de la charge : le « genou » où la latence explose indique la capacité ; identifier la ressource saturée à ce point (CPU, pool, base) ; comparer avec les SLO et la charge de pointe attendue avec marge (×2). Un débit qui plafonne avec CPU bas signale un goulot d'attente (verrou, pool, dépendance).

### 43. Comment détecter et corriger la contention de verrous ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Symptômes : CPU bas avec débit plafonné, threads `BLOCKED` dans les thread dumps sur le même moniteur, événements JFR `JavaMonitorEnter` longs. Corrections : réduire la section critique, remplacer par des structures concurrentes ou des atomiques, partitionner l'état (striping), verrous lecture/écriture, ou repenser pour éviter l'état partagé. `synchronized` sur des méthodes entières est le suspect habituel.

### 44. Comment optimiser une boucle chaude en Java ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Après l'avoir identifiée au profileur : éviter allocations et boxing, préférer tableaux et primitives aux collections génériques, sortir les invariants de la boucle, éviter les appels virtuels mégamorphiques (le JIT inline les sites monomorphiques), utiliser `StringBuilder`, et laisser le JIT faire (le code simple s'optimise mieux). Vérifier le gain avec JMH ; ne pas sacrifier la lisibilité ailleurs.

### 45. Qu'est-ce que le profil mémoire et comment traquer une fuite ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Observer la tendance de l'ancienne génération après chaque GC : si elle monte sans redescendre, fuite. Prendre un heap dump (`jcmd <pid> GC.heap_dump`, ou automatique sur OOM), l'analyser avec Eclipse MAT (« Leak Suspects », dominator tree, chemins vers les GC roots) : caches sans borne, `static` collections, listeners non désenregistrés, `ThreadLocal` avec pools, sessions, connexions non fermées. Comparer deux dumps espacés révèle ce qui croît.

### 46. Comment mesurer et améliorer l'efficacité CPU en cloud (coût) ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Le coût suit le CPU et la mémoire réservés : profiler pour supprimer le travail inutile (sérialisation, logs, requêtes redondantes), régler le GC pour moins de CPU, dimensionner requests/limits sur l'usage réel (VPA en recommandation), utiliser des instances ARM (Graviton) souvent moins chères pour Java, et l'autoscaling sur des métriques pertinentes. Suivre le coût par requête comme métrique de performance.

### 47. Comment optimiser les écritures en masse depuis Java ?
`🟠 Intermédiaire` · Sujet : **Base de données**

**Réponse :** JDBC batch (`addBatch`/`executeBatch`, `reWriteBatchedInserts=true` pour PostgreSQL), transactions par lots de quelques milliers de lignes, `COPY` PostgreSQL ou `LOAD DATA` MySQL pour les imports massifs, désactivation temporaire des index/contraintes si possible, Spring Batch avec `JdbcBatchItemWriter`, et éviter Hibernate pour les volumes très importants (ou utiliser `StatelessSession`).

### 48. Quel rôle jouent les timeouts dans la performance globale ?
`🟠 Intermédiaire` · Sujet : **Application**

**Réponse :** Sans timeout, une dépendance lente immobilise des threads et des connexions jusqu'à saturer le service, propageant la panne. Définir des timeouts par dépendance cohérents avec le budget de latence (le timeout total d'une requête doit rester inférieur au timeout de l'appelant), plus courts que le timeout du load balancer, et combinés avec retries limités et circuit breaker. Les timeouts sont une optimisation de disponibilité.

### 49. Comment documenter et présenter une optimisation ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Avant/après avec la même charge et les mêmes métriques (percentiles, débit, CPU, coût), le profil montrant le goulot identifié, le changement précis et son risque, et le résultat en production après déploiement (pas seulement en test). Une optimisation non mesurée en production n'est pas terminée ; conserver les benchmarks comme tests de non-régression de performance.

### 50. Quelles optimisations éviter (prématurées ou contre-productives) ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Micro-optimisations sur du code non critique au détriment de la lisibilité, caches partout sans mesure, pools surdimensionnés, `parallelStream` par réflexe, réactif par principe, réglages GC exotiques copiés d'un blog, désactivation de la validation ou des logs par « performance ». Règle : optimiser ce que le profileur montre, dans l'ordre d'impact, et prouver le gain.
