# 📊 Observability

> Logs, métriques, traces, SLI/SLO/SLA, golden signals, dashboards

**50 questions**

---

### 1. Quels sont les trois piliers de l'observabilité ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Les logs (événements horodatés détaillés), les métriques (mesures numériques agrégées, ex : latence, taux d'erreur) et les traces distribuées (suivi d'une requête à travers plusieurs services), souvent combinés via Prometheus, Grafana et Zipkin/Jaeger.

### 2. Quelle est la différence entre monitoring et observabilité ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Le monitoring surveille des métriques prédéfinies pour détecter des problèmes connus. L'observabilité permet de comprendre l'état interne d'un système à partir de ses sorties (logs, métriques, traces), y compris pour diagnostiquer des problèmes imprévus.

### 3. Qu'est-ce que le "distributed tracing" et quel identifiant relie les spans entre services ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Suivi d'une requête à travers plusieurs microservices. Chaque requête reçoit un trace ID unique propagé entre services, et chaque étape locale devient un span rattaché à ce trace ID.

### 4. Qu'est-ce qu'un SLI, un SLO et un SLA ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** SLI = métrique mesurée. SLO = objectif interne. SLA = engagement contractuel envers le client, souvent avec pénalités.

### 5. Cardinalité des métriques et enjeu dans Prometheus ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Nombre de combinaisons uniques de labels. Une cardinalité trop élevée explose l'utilisation mémoire de Prometheus.

### 6. Golden signals de Google SRE ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Latence, trafic, erreurs, saturation. Vue d'ensemble suffisante pour détecter la plupart des problèmes.

### 7. Corrélation logs/traces ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Injection du trace ID dans les logs applicatifs, permettant de retrouver tous les logs d'une requête à travers plusieurs services.

### 8. Dashboard as code avec Grafana ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Définir les dashboards en JSON/YAML versionnés dans Git, permettant reproductibilité, revue de code, déploiement automatisé.

### 9. Sampling dans le tracing distribué ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Collecte d'un sous-ensemble représentatif des traces, réduisant le volume de données tout en gardant une visibilité statistique.

### 10. Alert fatigue et comment la limiter ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Volume excessif d'alertes désensibilisant les équipes. Limité via seuils basés sur l'impact réel et regroupement des alertes.

### 11. Quels sont les types de métriques Prometheus (counter, gauge, histogram, summary) ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Counter : valeur cumulative croissante (requêtes totales), à lire avec `rate()`. Gauge : valeur instantanée montante/descendante (mémoire, connexions actives). Histogram : distribution en buckets côté serveur, agrégeable, permet `histogram_quantile`. Summary : quantiles calculés côté client, non agrégeables entre instances. Préférer histogram pour les latences.

### 12. Comment calculer un percentile de latence p95 avec PromQL ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** `histogram_quantile(0.95, sum(rate(http_server_requests_seconds_bucket[5m])) by (le, uri))`. Le `rate` sur les buckets, l'agrégation par `le` (obligatoire) et par dimension utile, puis la fonction estime le quantile par interpolation linéaire. La précision dépend des buckets définis ; les native histograms améliorent cela.

### 13. Que sont les métriques RED et USE ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** RED (services) : Rate (requêtes/s), Errors (taux d'erreur), Duration (latence). USE (ressources) : Utilization (% d'usage), Saturation (file d'attente, throttling), Errors. RED s'applique aux APIs, USE aux CPU, disques, pools de connexions ; ensemble ils couvrent les golden signals.

### 14. Comment exposer des métriques depuis Spring Boot avec Micrometer ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Micrometer est la façade (comme SLF4J pour les logs) ; `spring-boot-starter-actuator` + `micrometer-registry-prometheus` exposent `/actuator/prometheus`. Métriques automatiques : HTTP, JVM, pools, caches, Kafka. Métriques custom via `MeterRegistry` (`Counter`, `Timer`, `Gauge`) ou `@Timed`/`@Counted`. Les tags doivent rester à faible cardinalité.

### 15. Qu'est-ce qu'un ServiceMonitor / PodMonitor et la découverte de cibles Prometheus dans Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Prometheus découvre dynamiquement les cibles via l'API Kubernetes (annotations ou, avec Prometheus Operator, les CRDs `ServiceMonitor`/`PodMonitor` qui sélectionnent des Services/Pods par labels et indiquent le port et le chemin à scraper). Cela évite toute configuration manuelle à chaque nouveau déploiement.

### 16. Comment fonctionne l'alerting avec Prometheus et Alertmanager ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Les règles d'alerte (PromQL + `for` pour la durée) sont évaluées par Prometheus et envoyées à Alertmanager, qui déduplique, groupe, route (par label vers Slack/PagerDuty/email), inhibe (une alerte majeure masque les mineures) et gère les silences. Les alertes doivent être actionnables et liées à un runbook.

### 17. Qu'est-ce que le stockage longue durée de métriques (Thanos, Mimir, VictoriaMetrics) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Prometheus stocke localement quelques semaines. Thanos et Mimir ajoutent un stockage objet (S3), une vue globale multi-clusters, la déduplication des Prometheus en HA et le downsampling. VictoriaMetrics est une alternative plus économe. Ils exposent une API compatible PromQL pour Grafana.

### 18. Différence entre logs structurés et non structurés, et pourquoi préférer JSON ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Un log texte libre exige des regex fragiles pour en extraire des champs. Un log JSON (Logback avec `logstash-logback-encoder` ou le support natif de Spring Boot 3.4 `logging.structured.format`) porte des champs typés (`level`, `trace_id`, `user_id`, `duration_ms`) directement indexables et filtrables dans Loki/Elasticsearch.

### 19. Quelles bonnes pratiques pour des logs utiles et sûrs ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Niveaux cohérents (ERROR = action requise), messages avec contexte (identifiants métier, pas de « erreur »), pas de données sensibles (mots de passe, tokens, données personnelles), pas de logs dans les boucles chaudes, un événement par ligne, corrélation par trace id, et niveau de log modifiable à chaud (Actuator `/loggers`).

### 20. Différence entre Loki et Elasticsearch (ELK) pour les logs ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Elasticsearch indexe le contenu complet (recherche full-text puissante, coûteux en stockage et CPU). Loki n'indexe que les labels (namespace, app) et stocke les lignes compressées, ce qui est bien moins cher ; la recherche se fait par grep sur les chunks filtrés par labels (LogQL). Loki s'intègre naturellement à Grafana et Prometheus.

### 21. Qu'est-ce que le MDC (Mapped Diagnostic Context) en Java ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Une map par thread (SLF4J/Logback) où l'on place des valeurs contextuelles (trace id, tenant, user) automatiquement ajoutées à chaque ligne de log du thread. Micrometer Tracing y injecte `traceId`/`spanId`. Attention aux threads asynchrones et virtuels : le contexte doit être propagé explicitement (`ContextSnapshot`, `TaskDecorator`).

### 22. Comment collecter les logs de conteneurs dans Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Les applications écrivent sur stdout/stderr ; le runtime les stocke sur le nœud. Un agent en DaemonSet (Fluent Bit, Promtail/Alloy, Vector, Filebeat) lit ces fichiers, enrichit avec les métadonnées Kubernetes (namespace, pod, labels) et envoie vers Loki/Elasticsearch/OpenSearch. Pas de fichiers de log dans le conteneur.

### 23. Qu'est-ce qu'un span, ses attributs et les relations parent/enfant ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Un span représente une unité de travail (requête HTTP, requête SQL) avec nom, début/durée, statut, attributs (méthode, URL, `db.statement`), événements et liens. Les spans d'une trace forment un arbre via `parent_span_id` ; le span racine est l'entrée dans le système. La visualisation en cascade révèle où le temps est passé.

### 24. Comment fonctionne la propagation de contexte W3C Trace Context ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Le header `traceparent: 00-<trace-id>-<span-id>-<flags>` (et `tracestate`) est injecté dans chaque requête sortante et lu à l'entrée, reliant les spans entre services. OpenTelemetry et Micrometer Tracing le gèrent automatiquement pour HTTP, gRPC, Kafka (headers) et les clients JDBC instrumentés ; le format B3 de Zipkin est l'ancien standard.

### 25. Différence entre instrumentation automatique et manuelle avec OpenTelemetry ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** L'agent Java OpenTelemetry (`-javaagent`) instrumente sans code les frameworks courants (Spring, JDBC, Kafka, HTTP clients). L'instrumentation manuelle via l'API (`Tracer.spanBuilder`, `@WithSpan`) ajoute des spans métier et des attributs personnalisés. En pratique on combine : automatique pour la technique, manuelle pour le métier.

### 26. Qu'est-ce que l'OpenTelemetry Collector et pourquoi l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Un composant intermédiaire recevant les signaux (OTLP, Prometheus, Jaeger…), les traitant (batching, filtrage, sampling, enrichissement, suppression de données sensibles) et les exportant vers un ou plusieurs backends. Il découple les applications des outils, permet de changer de fournisseur sans redéployer et centralise la configuration.

### 27. Différence entre head-based et tail-based sampling ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Head-based : la décision est prise au début de la trace (probabilité fixe), simple mais peut ignorer des traces intéressantes. Tail-based : le collector garde en mémoire la trace complète et décide à la fin (conserver 100 % des erreurs et des traces lentes, 1 % du reste), plus pertinent mais nécessite que tous les spans passent par le même collector.

### 28. Qu'est-ce que Grafana Tempo et Jaeger ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Deux backends de traces. Jaeger (CNCF) est l'outil historique avec UI dédiée et stockage Elasticsearch/Cassandra. Tempo stocke les traces à bas coût dans un stockage objet, sans indexation lourde, s'intègre à Grafana (TraceQL) et permet de sauter depuis un log Loki ou une métrique (exemplars) vers la trace correspondante.

### 29. Qu'est-ce qu'un exemplar ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Une référence attachée à un point de métrique (bucket d'histogramme) vers un trace id concret. Dans Grafana, un point du graphe de latence p99 peut ainsi ouvrir directement une trace représentative, reliant métriques et traces sans recherche manuelle.

### 30. Comment définir un SLO et calculer un error budget en PromQL ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** SLI = proportion de bonnes requêtes : `sum(rate(http_requests_total{code!~"5.."}[30d])) / sum(rate(http_requests_total[30d]))`. Avec un SLO de 99,9 %, l'error budget est 0,1 % des requêtes sur la fenêtre. Les alertes « burn rate » (multi-fenêtres, ex. 14,4× sur 1 h et 6× sur 6 h) préviennent quand le budget se consomme trop vite.

### 31. Qu'est-ce que le monitoring synthétique et le RUM ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Synthétique : des sondes exécutent périodiquement des scénarios (ping HTTP, parcours de connexion avec Playwright, Blackbox exporter, Checkly) depuis plusieurs régions pour détecter les pannes avant les utilisateurs. RUM (Real User Monitoring) : un script dans le navigateur mesure l'expérience réelle (Core Web Vitals, erreurs JS) par device et géographie.

### 32. Qu'est-ce que le profiling continu (Pyroscope, Parca) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Un « quatrième pilier » : collecte à faible surcharge des profils CPU/mémoire/allocations en production, stockés en continu et interrogeables par période et labels. Il permet de répondre à « quelle fonction consomme le CPU depuis le déploiement de 14 h » sans reproduire le problème ; l'agent Java s'appuie sur async-profiler/JFR.

### 33. Comment monitorer une JVM en production et quelles métriques regarder ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Micrometer expose : heap utilisé/max par génération, pauses et fréquence GC (`jvm_gc_pause_seconds`), threads (états, virtuels), classes chargées, CPU process, descripteurs de fichiers, pools (HikariCP : actifs, en attente, timeouts). Alertes typiques : GC > 10 % du temps, heap post-GC en hausse continue (fuite), threads bloqués.

### 34. Comment monitorer Kafka (producteurs, consommateurs, lag) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Lag des consumer groups (Kafka Exporter, Burrow, `kafka_consumergroup_lag`), débit par topic, erreurs de production, temps de commit, rebalances fréquentes, ISR sous-répliqués, disque des brokers. Une alerte sur le lag croissant détecte un consommateur trop lent ou bloqué avant que les données ne soient perdues par rétention.

### 35. Comment monitorer une base de données (PostgreSQL) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** postgres_exporter ou pgwatch : connexions actives vs max, requêtes lentes (`pg_stat_statements`), verrous et attentes, taux de cache hit, bloat et vacuum, réplication lag, taille des tables/indexes, transactions longues. Corréler avec les métriques applicatives du pool de connexions.

### 36. Qu'est-ce que Grafana et ses concepts (datasource, panel, variable, annotation) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Grafana visualise des données de sources variées (Prometheus, Loki, Tempo, SQL, CloudWatch). Un dashboard contient des panels (graphes, stats, tables), des variables (sélecteur de namespace/service réutilisé dans les requêtes), des annotations (déploiements marqués sur les graphes) et peut définir des alertes unifiées.

### 37. Comment concevoir un bon dashboard ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Un objectif par dashboard (vue service, vue infra, vue SLO), les informations critiques en haut (SLO, erreurs, latence), hiérarchie du général au détail, unités et seuils explicites, mêmes couleurs pour les mêmes concepts, variables pour naviguer, liens vers logs/traces et runbooks. Éviter les « murs de graphes » illisibles.

### 38. Qu'est-ce que le monitoring boîte blanche vs boîte noire ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Boîte noire : observer le système de l'extérieur comme un utilisateur (sondes HTTP, tests synthétiques) — détecte les symptômes. Boîte blanche : métriques internes exposées par l'application (pools, files, GC) — explique les causes et permet la prédiction. Les alertes de pagination viennent surtout de la boîte noire et des SLO.

### 39. Comment gérer l'observabilité en environnement multi-tenant ou multi-équipes ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Labels standardisés (`team`, `service`, `env`) imposés par convention/policy, namespaces et permissions Grafana par équipe, tenants Loki/Mimir/Tempo pour l'isolation et les quotas, dashboards et alertes as code dans le dépôt de chaque équipe, et une plateforme commune opérée par l'équipe platform.

### 40. Que sont les Kubernetes events et kube-state-metrics ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** kube-state-metrics expose l'état des objets Kubernetes en métriques (Pods en CrashLoopBackOff, réplicas indisponibles, Jobs échoués, PVC pending), indispensable pour alerter sur la santé des déploiements. Les events (`kubectl get events`) sont éphémères ; un exporter (kubernetes-event-exporter) les envoie vers Loki pour les conserver.

### 41. Comment mesurer le coût d'une pile d'observabilité et le maîtriser ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Les logs verbeux et les métriques à haute cardinalité sont les premiers postes. Leviers : niveaux de log adaptés, échantillonnage des traces, réduction des labels inutiles (`relabel_configs`, `metric_relabel_configs`), rétention différenciée (chaud/froid), agrégation (recording rules), et suivi de la volumétrie par équipe.

### 42. Qu'est-ce qu'une recording rule Prometheus ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Une règle qui pré-calcule périodiquement une expression PromQL coûteuse et la stocke comme nouvelle série (`job:http_requests:rate5m`). Elle accélère les dashboards et les alertes, et normalise les calculs (SLI) entre équipes. Convention de nommage : `level:metric:operations`.

### 43. Comment corréler un déploiement à une régression de performance ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Annoter les déploiements sur les graphes (annotation Grafana via l'API depuis la CI/ArgoCD), ajouter le label `version` aux métriques (Micrometer commonTags) pour comparer les versions côte à côte pendant un canary, et lier traces/profils à la version. Les métriques DORA « change failure rate » s'en nourrissent.

### 44. Qu'est-ce que le health check Actuator et comment l'enrichir ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** `/actuator/health` agrège des `HealthIndicator` (base, disque, Kafka, Redis, custom). On sépare les groupes `liveness` et `readiness` (`management.endpoint.health.group.readiness.include=db,kafka`) pour que Kubernetes ne redémarre pas un Pod dont seule une dépendance est en panne. Les détails sont masqués aux non-authentifiés.

### 45. Différence entre alerte sur symptôme et alerte sur cause ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Alerter sur les symptômes visibles par l'utilisateur (SLO en danger, taux d'erreur, latence) réveille l'astreinte pour ce qui compte. Les alertes sur causes (CPU haut, disque à 80 %) servent de signaux d'avertissement non paginants ou de contexte pendant l'investigation. Paginer sur les causes génère du bruit et de la fatigue.

### 46. Comment gérer l'observabilité d'une application serverless (Lambda) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Logs structurés dans CloudWatch (Logs Insights), métriques natives (invocations, erreurs, durée, throttles, cold starts via `Init Duration`), X-Ray ou OpenTelemetry via ADOT layer, corrélation par request id, et alarmes sur les erreurs et la DLQ. Lambda Powertools (Java) simplifie logs, métriques et tracing.

### 47. Qu'est-ce que l'observabilité frontend (erreurs JS, Web Vitals) ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Collecter côté navigateur les erreurs non capturées, les rejets de promesses, les Core Web Vitals et les timings des appels API (Sentry, Grafana Faro, Datadog RUM), avec versions de release et source maps pour des stack traces lisibles. Propager le `traceparent` depuis le front vers le back permet des traces de bout en bout.

### 48. Comment mener une investigation d'incident avec les trois piliers ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Partir de l'alerte (métrique), identifier la période et le service via les dashboards, ouvrir les traces lentes/en erreur de cette période (exemplars, TraceQL), puis lire les logs corrélés par trace id pour la cause exacte. Noter la chronologie pour le post-mortem et ajouter une alerte/dashboard si un signal manquait.

### 49. Qu'est-ce que la « cardinality explosion » et comment y remédier ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Un label à valeurs illimitées (user id, URL avec identifiant, request id) crée des millions de séries et fait tomber Prometheus. Remèdes : normaliser les chemins (`/users/{id}`, ce que fait Micrometer avec les templates d'URI), déplacer ces valeurs dans les logs/traces, limiter par `metric_relabel_configs`, et surveiller `prometheus_tsdb_head_series`.

### 50. Quels standards et conventions sémantiques OpenTelemetry faut-il connaître ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Les semantic conventions définissent les noms d'attributs standard (`http.request.method`, `http.response.status_code`, `db.system`, `messaging.system`, `service.name`, `deployment.environment`). Les respecter garantit que les dashboards et backends interprètent correctement les données quel que soit le langage ou le framework.
