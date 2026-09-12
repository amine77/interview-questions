# 📨 Apache Kafka

> Topics, partitions, consumer groups, Streams, exactly-once semantics

**100 questions**

---

### 1. Quelle est la différence entre un topic et une partition dans Kafka ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Un topic est une catégorie/flux logique de messages. Une partition est une subdivision physique d'un topic permettant la parallélisation et la scalabilité horizontale.

### 2. Qu'est-ce qu'un consumer group ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Ensemble de consommateurs partageant la lecture des partitions d'un topic, chaque partition lue par un seul consommateur du groupe à la fois.

### 3. Rôle de Zookeeper (ou KRaft) ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Gère métadonnées, élection du leader, coordination des brokers. KRaft remplace Zookeeper nativement.

### 4. Sémantique "exactly-once" ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Garantit qu'un message est traité exactement une fois, via producteurs idempotents et transactions Kafka.

### 5. Qu'est-ce qu'un offset ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Identifiant numérique de la position d'un message dans une partition.

### 6. Qu'est-ce que Kafka Streams ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Bibliothèque cliente pour construire des applications de traitement de flux sur Kafka.

### 7. Qu'est-ce que la rétention ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Politique définissant la durée/taille de conservation des messages dans un topic.

### 8. Différence producer / consumer ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Producer publie des messages. Consumer s'abonne et lit les messages.

### 9. Qu'est-ce qu'un broker et un cluster Kafka ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Un broker est un serveur Kafka stockant des partitions et servant producteurs/consommateurs. Un cluster regroupe plusieurs brokers ; les partitions sont réparties entre eux avec réplication. Un broker est « controller » (élu via KRaft) et gère les métadonnées et l'élection des leaders de partition.

### 10. Comment un message est-il assigné à une partition ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Si une clé est fournie, le partitionneur hache la clé (murmur2) modulo le nombre de partitions : même clé → même partition, ce qui garantit l'ordre par clé. Sans clé, le producteur utilise le « sticky partitioner » (remplit un batch sur une partition puis change). Ajouter des partitions change le mapping des clés.

### 11. Qu'est-ce que la garantie d'ordre dans Kafka ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** L'ordre n'est garanti qu'au sein d'une partition. Pour ordonner les événements d'une entité (commande, client), on utilise son identifiant comme clé. Avec `max.in.flight.requests.per.connection > 1` sans idempotence, un retry peut réordonner ; activer `enable.idempotence=true` préserve l'ordre.

### 12. Que signifient `acks=0`, `acks=1` et `acks=all` ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `acks=0` : le producteur n'attend rien (perte possible, débit max). `acks=1` : le leader confirme l'écriture (perte si le leader tombe avant réplication). `acks=all` : tous les réplicas in-sync confirment, combiné à `min.insync.replicas=2` pour une durabilité forte. C'est le défaut depuis Kafka 3.0.

### 13. Qu'est-ce que le facteur de réplication et les ISR ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Chaque partition est répliquée sur N brokers (leader + followers). Les In-Sync Replicas sont les réplicas à jour avec le leader. Si le leader tombe, un ISR est élu. `min.insync.replicas` définit combien doivent accuser une écriture `acks=all` ; sinon le producteur reçoit `NotEnoughReplicasException`. `unclean.leader.election=false` évite d'élire un réplica en retard.

### 14. Qu'est-ce qu'un producteur idempotent et une transaction Kafka ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le producteur idempotent (`enable.idempotence=true`) attache un identifiant et un numéro de séquence à chaque batch, permettant au broker de dédupliquer les retries : exactly-once par partition. Les transactions (`transactional.id`) étendent cela à plusieurs partitions et au commit d'offsets consommés (pattern consume-transform-produce), base de l'EOS de Kafka Streams.

### 15. Comment fonctionne le commit d'offset et quelle différence entre auto et manuel ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le consommateur enregistre sa position dans le topic interne `__consumer_offsets`. `enable.auto.commit=true` commite périodiquement (risque de perte si crash après commit avant traitement, ou doublon inverse). Le commit manuel (`commitSync`/`commitAsync`, ou `AckMode.MANUAL` dans Spring) après traitement donne du at-least-once maîtrisé.

### 16. Qu'est-ce que le rebalance d'un consumer group et pourquoi est-il coûteux ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Quand un consommateur rejoint/quitte le groupe ou que des partitions changent, les partitions sont réassignées. En mode eager, tous les consommateurs arrêtent de consommer (stop-the-world). Le protocole coopératif (`CooperativeStickyAssignor`) et les membres statiques (`group.instance.id`) réduisent l'impact. Le nouveau protocole KIP-848 (Kafka 4.0) déplace la logique côté broker.

### 17. Que signifient `max.poll.records`, `max.poll.interval.ms` et `session.timeout.ms` ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `max.poll.records` limite le nombre de messages par `poll()`. `max.poll.interval.ms` : délai max entre deux `poll()` ; dépassé (traitement trop long), le consommateur est exclu du groupe → rebalance. `session.timeout.ms`/`heartbeat.interval.ms` détectent un consommateur mort via les heartbeats d'un thread séparé.

### 18. Qu'est-ce qu'une Dead Letter Topic et comment gérer les messages en erreur ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un message dont le traitement échoue de façon répétée est publié sur un topic `.DLT` avec des headers décrivant l'erreur, puis l'offset est commité pour ne pas bloquer la partition. Spring Kafka fournit `DefaultErrorHandler` avec backoff et `DeadLetterPublishingRecoverer`, plus des retry topics non bloquants (`@RetryableTopic`).

### 19. Comment garantir l'idempotence côté consommateur ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Kafka livre en at-least-once par défaut : le consommateur peut recevoir un doublon. Le traitement doit être idempotent : clé unique/upsert en base, table de déduplication par identifiant d'événement (avec TTL), opérations naturellement idempotentes (set plutôt qu'increment), ou transactions Kafka pour les pipelines Kafka→Kafka.

### 20. Différence entre rétention par temps/taille et log compaction ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** La rétention classique supprime les segments plus vieux que `retention.ms` ou au-delà de `retention.bytes`. La compaction (`cleanup.policy=compact`) conserve uniquement la dernière valeur de chaque clé (une valeur `null` = tombstone supprime la clé), ce qui donne un « changelog » infini : idéal pour les tables de référence et les state stores.

### 21. Comment choisir le nombre de partitions d'un topic ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Il fixe le parallélisme maximal des consommateurs d'un groupe (plus de consommateurs que de partitions = inactifs). Estimer à partir du débit cible / débit par consommateur, prévoir la croissance (on peut ajouter mais pas retirer, et l'ajout casse le mapping des clés), sans excès (chaque partition coûte en fichiers, mémoire et temps de failover).

### 22. Qu'est-ce que le batching et la compression côté producteur ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `linger.ms` attend quelques ms pour remplir un batch (`batch.size`), réduisant le nombre de requêtes ; `compression.type` (lz4, zstd, snappy) compresse le batch entier, économisant réseau et disque. Ces réglages augmentent le débit au prix d'une latence légèrement supérieure.

### 23. Comment les producteurs et consommateurs découvrent-ils les brokers (`bootstrap.servers`) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le client contacte un des `bootstrap.servers` pour obtenir les métadonnées du cluster (liste des brokers, leaders de partitions), puis se connecte directement aux leaders. `advertised.listeners` doit exposer des adresses joignables par les clients, source classique de problèmes dans Docker/Kubernetes.

### 24. Qu'est-ce que le Schema Registry et pourquoi l'utiliser avec Avro/Protobuf ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un service stockant les schémas des messages, référencés par identifiant dans chaque message (préfixe de 5 octets), au lieu d'embarquer le schéma. Il impose des règles de compatibilité (backward, forward, full) à l'enregistrement, empêchant un producteur de casser les consommateurs, et permet des payloads compacts et typés.

### 25. Différence entre compatibilité backward, forward et full d'un schéma ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Backward : les nouveaux consommateurs lisent les anciens messages (on peut supprimer des champs ou ajouter des champs avec défaut). Forward : les anciens consommateurs lisent les nouveaux messages (ajouter des champs, supprimer ceux avec défaut). Full : les deux. Backward est le mode par défaut car on met généralement à jour les consommateurs d'abord.

### 26. Comment configurer un consumer Kafka dans Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `spring.kafka.consumer.*` (bootstrap, group-id, deserializers, `auto-offset-reset`), `@KafkaListener(topics = "orders", groupId = "billing")` sur une méthode, avec `concurrency` pour plusieurs threads (≤ partitions), un `ConcurrentKafkaListenerContainerFactory` personnalisé pour l'error handler, le ack mode et le filtrage. `@EmbeddedKafka` ou Testcontainers pour les tests.

### 27. Que signifie `auto.offset.reset` et quand `earliest` vs `latest` ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Position initiale d'un groupe sans offset commité (nouveau groupe ou offsets expirés) : `earliest` lit depuis le début (retraitement complet, choix des projections/CQRS), `latest` ne lit que les nouveaux messages (choix des notifications temps réel). `none` lève une exception. Ne s'applique pas si un offset valide existe.

### 28. Comment rejouer des messages (reset d'offsets) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `kafka-consumer-groups.sh --reset-offsets --to-earliest|--to-datetime|--shift-by --execute` sur un groupe arrêté. Cas d'usage : reconstruire une projection, retraiter après un bug. Nécessite des consommateurs idempotents et une attention à la rétention (les messages doivent encore exister).

### 29. Qu'est-ce que Kafka Connect et un connecteur source/sink ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un framework d'intégration sans code : les connecteurs source lisent des systèmes externes vers Kafka (Debezium pour le CDC, JDBC, S3), les sinks écrivent de Kafka vers des cibles (Elasticsearch, S3, JDBC, BigQuery). Il gère scalabilité (tasks), offsets, transformations simples (SMT) et tourne en cluster distribué.

### 30. Différence entre KStream, KTable et GlobalKTable ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `KStream` : flux d'événements immuables (chaque record est un fait). `KTable` : vue « dernière valeur par clé » d'un topic (changelog), partitionnée comme le topic. `GlobalKTable` : table entièrement répliquée sur chaque instance, permettant des jointures sans co-partitionnement, réservée aux petites tables de référence.

### 31. Qu'est-ce que le co-partitionnement pour les jointures Kafka Streams ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Pour joindre deux flux/tables par clé, ils doivent avoir le même nombre de partitions et la même stratégie de partitionnement, afin que les clés identiques soient traitées par la même tâche. Sinon Kafka Streams repartitionne automatiquement via un topic interne, avec un coût réseau.

### 32. Qu'est-ce qu'un state store et comment est-il tolérant aux pannes ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un stockage local (RocksDB) utilisé par les opérations à état (agrégations, jointures, fenêtres). Chaque modification est écrite dans un topic changelog compacté ; en cas de perte d'une instance, l'état est reconstruit depuis ce topic sur une autre instance (standby replicas accélèrent la reprise).

### 33. Quels types de fenêtres existent dans Kafka Streams ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Tumbling (fixes, non chevauchantes), hopping (fixes, chevauchantes), sliding (basées sur l'écart entre événements), session (regroupent l'activité avec un gap d'inactivité). Le grace period accepte les événements en retard ; `suppress()` n'émet que le résultat final d'une fenêtre.

### 34. Différence entre event time, processing time et ingestion time ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Event time : horodatage porté par l'événement (quand il s'est produit) ; processing time : quand il est traité ; ingestion time : quand le broker l'a reçu. Les fenêtres doivent se baser sur l'event time pour des résultats corrects malgré les retards et le rejeu, ce qu'un `TimestampExtractor` configure.

### 35. Qu'est-ce que le pattern « consume-transform-produce » exactly-once ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Lire d'un topic, transformer, écrire sur un autre en garantissant qu'un message d'entrée produit exactement une fois sa sortie, malgré les pannes. Kafka Streams (`processing.guarantee=exactly_once_v2`) englobe production et commit d'offset dans une transaction atomique. Cela ne couvre pas les effets de bord externes (base, email).

### 36. Comment sécuriser un cluster Kafka ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Chiffrement TLS des connexions, authentification SASL (SCRAM, OAUTHBEARER, Kerberos) ou mTLS, autorisation par ACL (ou RBAC dans les distributions commerciales) par topic/groupe/opération, chiffrement des disques, et audit. Dans Kubernetes, Strimzi automatise certificats et utilisateurs via CRDs.

### 37. Qu'est-ce que KRaft et pourquoi ZooKeeper a-t-il été retiré ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** KRaft intègre le consensus Raft directement dans Kafka pour gérer les métadonnées, supprimant ZooKeeper (Kafka 4.0 ne le supporte plus). Avantages : une seule technologie à opérer, démarrage et failover plus rapides, support de bien plus de partitions par cluster. La migration depuis ZooKeeper est possible sur les versions 3.x.

### 38. Qu'est-ce que le tiered storage ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Une fonctionnalité (Kafka 3.6+) déplaçant les segments anciens vers un stockage objet (S3) tout en gardant les récents sur disque local. Elle permet une rétention longue à bas coût, des brokers plus légers, et un rééquilibrage plus rapide puisque moins de données locales à copier.

### 39. Comment diagnostiquer un lag de consommateur croissant ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Vérifier le débit du consommateur vs la production, le temps de traitement par message (appel synchrone lent ?), le nombre de consommateurs vs partitions, les rebalances répétés (logs, `max.poll.interval.ms`), les erreurs répétées bloquant une partition, et les ressources (CPU, GC). Solutions : paralléliser, batcher, augmenter les partitions, traitement asynchrone avec ordre préservé par clé.

### 40. Qu'est-ce que le pattern « Kafka comme source de vérité » et ses limites ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Utiliser des topics compactés comme stockage durable de l'état (event sourcing léger, KTable). Avantage : rejouable, découplé. Limites : pas de requêtes ad hoc (il faut des projections), taille des topics, rétention à gérer, et complexité RGPD. Kafka reste un journal, pas une base de données transactionnelle.

### 41. Comment gérer les messages volumineux ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** La limite par défaut est ~1 Mo (`message.max.bytes`, `max.request.size`). Plutôt que l'augmenter fortement, appliquer le « claim check » : stocker le payload dans S3 et publier une référence, ou découper en chunks. Compresser aide pour les messages textuels.

### 42. Qu'est-ce que la réplication inter-clusters (MirrorMaker 2, Cluster Linking) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** MirrorMaker 2 (basé sur Kafka Connect) réplique topics, configurations, offsets et ACLs entre clusters pour la reprise d'activité, la géo-distribution ou la migration. Cluster Linking (Confluent) fait de même nativement sans Connect avec conservation des offsets. La réplication est asynchrone.

### 43. Comment dimensionner et monitorer les brokers ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Disques rapides et volumineux (les écritures sont séquentielles, le page cache compte), RAM pour le page cache, réseau 10 Gb+, JVM heap modérée (6-8 Go). Surveiller : partitions sous-répliquées, élections de leader, latence de requête, utilisation disque, nombre de fichiers ouverts, saturation réseau et threads (`RequestHandlerAvgIdlePercent`).

### 44. Différence entre Kafka et RabbitMQ ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Kafka : journal distribué persistant, consommateurs pull avec offsets rejouables, très haut débit, ordre par partition, rétention configurable ; adapté aux événements, streaming, intégration. RabbitMQ : broker de messages traditionnel (AMQP), routage riche (exchanges), push aux consommateurs, acquittement par message, files supprimées après consommation ; adapté aux tâches et RPC.

### 45. Différence entre Kafka et des files cloud comme SQS/Pub/Sub ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** SQS/Pub/Sub sont entièrement managés, sans partitions à gérer, facturés à l'usage, mais avec un ordre limité (FIFO restreint), pas de rejeu au-delà de la rétention et des débits par file. Kafka (ou MSK/Confluent Cloud managé) offre rejeu, ordre par clé, streaming et écosystème Connect/Streams, avec plus d'exploitation.

### 46. Qu'est-ce que Strimzi et comment déployer Kafka sur Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Strimzi est un operator qui gère des clusters Kafka via CRDs (`Kafka`, `KafkaTopic`, `KafkaUser`, `KafkaConnect`) : provisioning, mises à jour rolling, certificats, quotas, exporters Prometheus. Il demande des StorageClass performantes et une anti-affinité entre brokers. Alternative managée : MSK, Confluent Cloud, Aiven.

### 47. Qu'est-ce que le « poison pill » et comment s'en protéger ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un message impossible à désérialiser ou à traiter, qui fait crasher le consommateur en boucle et bloque la partition. Protections : `ErrorHandlingDeserializer` de Spring Kafka (le message devient une erreur traitée plutôt qu'une exception fatale), DLT après N tentatives, validation par Schema Registry côté producteur.

### 48. Comment tester l'ordre et la concurrence des consommateurs en local ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Testcontainers `KafkaContainer` (ou `ConfluentKafkaContainer`), création de topics avec plusieurs partitions, production de messages avec clés, puis assertions sur l'ordre par clé et le traitement parallèle entre clés. `Awaitility` pour attendre la consommation. Pour Kafka Streams, `TopologyTestDriver` teste la topologie sans broker.

### 49. Qu'est-ce qu'un quota Kafka ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Des limites par client/utilisateur sur le débit de production, de consommation et le taux de requêtes, appliquées par les brokers en ralentissant (throttling) les clients dépassant le seuil. Ils protègent un cluster partagé contre un client abusif ou une application mal configurée.

### 50. Quels headers et métadonnées ajouter à un message pour une bonne gouvernance ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Identifiant unique d'événement (déduplication), type et version de schéma, timestamp métier, identifiant de corrélation/trace (`traceparent`), producteur/source, éventuellement tenant. Un contrat d'événement documenté (AsyncAPI) et une convention de nommage des topics (`domaine.entite.evenement.v1`) facilitent la découverte.

### 51. Comment est structuré un log de partition Kafka sur disque (segments, index) ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Chaque partition est un répertoire contenant des segments (fichiers `.log` append-only, taille `segment.bytes`), avec un index d'offsets (`.index`) et un index temporel (`.timeindex`). Seul le segment actif reçoit les écritures ; les anciens sont éligibles à la rétention ou au compactage. Cette structure séquentielle explique le débit élevé (écritures séquentielles, zero-copy `sendfile` vers les consommateurs).

### 52. Qu'est-ce qu'un record Kafka (clé, valeur, headers, timestamp) ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Un enregistrement contient une clé (optionnelle, détermine la partition et l'ordre), une valeur (payload octets, sérialisé), des headers (métadonnées : type d'événement, trace id, version de schéma), un timestamp (`CreateTime` du producteur ou `LogAppendTime` du broker), et reçoit un offset. Les records sont regroupés en batches compressés.

### 53. Que sont leader, followers et ISR pour une partition ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** Chaque partition a un leader (seul broker qui sert lectures et écritures, sauf `follower fetching`) et des followers qui répliquent. L'ISR (in-sync replicas) est l'ensemble des réplicas à jour ; `acks=all` attend l'ISR, et `min.insync.replicas` fixe le minimum pour accepter une écriture. Si le leader tombe, un membre de l'ISR est élu (`unclean.leader.election.enable=false` évite la perte de données).

### 54. Comment fonctionne `KafkaProducer.send()` en interne ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** `send()` sérialise, choisit la partition (partitioner), place le record dans un accumulateur par partition (batch, `batch.size`, `linger.ms`) ; un thread I/O envoie les batches au leader, gère les retries (`retries`, `delivery.timeout.ms`), l'idempotence (sequence numbers) et appelle le callback/complète le `Future` avec les métadonnées (partition, offset) ou une exception. `flush()` force l'envoi.

### 55. Comment fonctionne la boucle `poll()` d'un consommateur ?
`🟢 Débutant` · Sujet : **Kafka**

**Réponse :** `poll(timeout)` gère en une fois : jointure/heartbeat du groupe (thread séparé pour les heartbeats depuis 0.10.1), fetch des records depuis les leaders (`fetch.min.bytes`, `max.partition.fetch.bytes`), commit automatique éventuel, et retour d'un `ConsumerRecords`. Ne pas appeler `poll` dans `max.poll.interval.ms` fait sortir le consommateur du groupe : traiter vite ou déléguer et gérer les offsets manuellement.

### 56. Que sont `enable.auto.commit`, `commitSync`, `commitAsync` et le commit par offset précis ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Auto-commit valide périodiquement (`auto.commit.interval.ms`) les offsets retournés par `poll`, risquant la perte si le traitement échoue après. Commit manuel : `commitSync` (bloquant, fiable, à la fin d'un batch), `commitAsync` (non bloquant, avec callback ; combiner `commitAsync` en routine et `commitSync` à la fermeture), et commit par partition/offset précis (`Map<TopicPartition, OffsetAndMetadata>`) pour valider exactement ce qui a été traité (offset + 1).

### 57. Quelles stratégies d'assignation de partitions existent (range, round-robin, sticky, cooperative) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `RangeAssignor` (défaut historique, déséquilibré avec plusieurs topics), `RoundRobin`, `StickyAssignor` (minimise les mouvements), `CooperativeStickyAssignor` (rebalance incrémental : seules les partitions réassignées sont révoquées, sans stop-the-world). Le nouveau protocole de groupe KIP-848 (Kafka 4.0) déplace la logique côté broker et rend les rebalances beaucoup plus rapides.

### 58. Qu'est-ce que le static membership (`group.instance.id`) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un identifiant stable par instance de consommateur : lors d'un redémarrage rapide (déploiement, crash), le broker conserve son assignation jusqu'à `session.timeout.ms` sans déclencher de rebalance. Utile pour les déploiements Kubernetes (Pods de StatefulSet) et les applications Kafka Streams avec de gros state stores, pour éviter les tempêtes de rebalance.

### 59. Comment fonctionne le partitioner par défaut et le sticky partitioning ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Avec clé : hash murmur2 de la clé modulo le nombre de partitions (stable tant que le nombre de partitions ne change pas). Sans clé : le sticky partitioner (2.4+) remplit un batch pour une partition avant de passer à une autre, améliorant la compression et la latence ; depuis 3.3, l'assignation uniforme adaptative tient compte de la vitesse des brokers. Un partitioner personnalisé permet des règles métier (tenant prioritaire).

### 60. Pourquoi ne peut-on pas réduire le nombre de partitions, et que se passe-t-il quand on l'augmente ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Réduire impliquerait de fusionner des logs et casserait l'ordre : non supporté (recréer un topic). Augmenter change le résultat du hash modulo : les nouvelles clés d'un même identifiant peuvent aller dans une autre partition, rompant l'ordre relatif et le co-partitionnement pour Kafka Streams. Sur-provisionner raisonnablement dès le départ et prévoir une migration par nouveau topic si nécessaire.

### 61. Comment fonctionne le log compaction en détail (tombstones, `min.cleanable.dirty.ratio`) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le cleaner conserve la dernière valeur de chaque clé dans les segments non actifs ; une valeur `null` (tombstone) supprime la clé après `delete.retention.ms`. Le compactage se déclenche selon `min.cleanable.dirty.ratio` et `min.compaction.lag.ms`. Cas d'usage : changelog de state stores, topics de configuration, CDC (dernier état par entité). Attention : les consommateurs peuvent voir des anciennes valeurs avant le compactage.

### 62. Comment configurer un producteur pour la durabilité maximale ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `acks=all`, `enable.idempotence=true` (implique `max.in.flight.requests.per.connection<=5` avec ordre garanti, `retries` élevé), `min.insync.replicas=2` sur un topic à réplication 3, `delivery.timeout.ms` adapté, `unclean.leader.election.enable=false` côté broker, et gestion explicite des exceptions non réessayables (`RecordTooLargeException`, sérialisation). Le débit baisse légèrement par rapport à `acks=1`.

### 63. Comment configurer un producteur pour le débit maximal ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `linger.ms` de 5-50 ms et `batch.size` plus grand pour remplir les batches, `compression.type=lz4` ou `zstd`, `buffer.memory` suffisant, `acks=1` si la perte rare est acceptable (sinon `all`), plusieurs partitions pour paralléliser, et envois asynchrones avec callbacks (pas de `get()` sur chaque `send`). Mesurer `record-send-rate`, `batch-size-avg` et `compression-rate-avg`.

### 64. Comment fonctionnent les transactions Kafka de bout en bout (producteur, consommateur `read_committed`) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le producteur transactionnel (`transactional.id`, `initTransactions`, `beginTransaction`, `sendOffsetsToTransaction`, `commitTransaction`) écrit atomiquement dans plusieurs partitions et valide les offsets consommés dans la même transaction ; le coordinateur écrit des marqueurs de commit/abort. Les consommateurs en `isolation.level=read_committed` ne voient pas les messages abandonnés. L'exactly-once vaut à l'intérieur de Kafka ; une écriture externe (base) reste à rendre idempotente.

### 65. Quel est le rôle des `__consumer_offsets` et `__transaction_state` ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Topics internes compactés : `__consumer_offsets` stocke les offsets committés par groupe/partition (et les métadonnées de groupe), géré par le group coordinator ; `__transaction_state` stocke l'état des transactions par `transactional.id`, géré par le transaction coordinator. Leur facteur de réplication (`offsets.topic.replication.factor`) doit être ≥ 3 en production ; leur `retention` (`offsets.retention.minutes`) efface les offsets des groupes inactifs.

### 66. Comment fonctionne KRaft en détail (quorum, controller, métadonnées) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un quorum de contrôleurs (3 ou 5 nœuds, rôles `controller` ou `combined`) réplique le log de métadonnées `__cluster_metadata` via Raft ; le leader actif traite les changements (topics, ISR, leaders) et les brokers suivent ce log, ce qui rend les failovers et les démarrages beaucoup plus rapides que ZooKeeper (millions de partitions possibles). Kafka 4.0 supprime le mode ZooKeeper : migrer en 3.x avant.

### 67. Quelles nouveautés majeures dans Kafka 4.x ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** KRaft uniquement, nouveau protocole de consumer group (KIP-848, rebalance côté serveur), files partagées (« Queues for Kafka », KIP-932 : share groups permettant plusieurs consommateurs par partition avec acquittement individuel, en early access), Java 17 minimum pour les brokers, suppression d'APIs dépréciées, améliorations de Kafka Streams et Connect. Vérifier les notes de version pour l'état de chaque fonctionnalité.

### 68. Comment fonctionne le fetch depuis les followers (`replica.selector.class`) et pourquoi ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Par défaut les consommateurs lisent depuis le leader. Avec `RackAwareReplicaSelector` et `client.rack` côté consommateur, un consommateur lit depuis le réplica situé dans sa zone de disponibilité, réduisant le trafic inter-AZ (coût cloud) et la latence, au prix d'une légère latence de réplication. Les producteurs écrivent toujours au leader.

### 69. Comment fonctionne le contrôle du débit côté consommateur (`pause`/`resume`, backpressure) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `consumer.pause(partitions)` arrête temporairement le fetch de partitions tout en continuant à `poll` (heartbeats maintenus), puis `resume`. Utile quand le traitement aval est saturé (file interne pleine, base lente) pour éviter de dépasser `max.poll.interval.ms`. Spring Kafka expose `pause`/`resume` sur le conteneur et gère la backpressure via `max.poll.records` et l'ack mode.

### 70. Comment traiter les messages en parallèle au sein d'une partition sans perdre l'ordre par clé ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le parallélisme natif est limité au nombre de partitions. Pour aller plus loin : le Confluent Parallel Consumer ou une exécution par clé (dispatcher qui affecte chaque clé à un worker déterminé, commit des offsets une fois tous les messages précédents traités), ou augmenter les partitions. Spring Kafka 3.x ne le fait pas nativement au-delà de la concurrence par partition.

### 71. Quels métriques et alertes surveiller côté broker ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `UnderReplicatedPartitions` (> 0 = problème de réplication), `OfflinePartitionsCount`, `ActiveControllerCount` (doit être 1), `RequestHandlerAvgIdlePercent` (< 30 % = saturation), latences `Produce`/`Fetch` p99, utilisation disque et `LogFlushRateAndTimeMs`, taux d'ISR shrink/expand, nombre de connexions, et le lag par groupe (Burrow, Kafka Exporter, `kafka-consumer-groups --describe`).

### 72. Quels métriques surveiller côté client (producteur et consommateur) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Producteur : `record-error-rate`, `record-retry-rate`, `request-latency-avg`, `buffer-available-bytes`, `batch-size-avg`, `compression-rate-avg`. Consommateur : `records-lag-max`, `fetch-latency-avg`, `commit-latency-avg`, `records-consumed-rate`, temps entre `poll` (`time-between-poll-max` vs `max.poll.interval.ms`), et rebalances (`rebalance-rate-per-hour`). Exposés via JMX et Micrometer (`KafkaClientMetrics`).

### 73. Comment dimensionner la rétention et la taille des disques ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Volume = débit entrant × rétention × facteur de réplication (+ marge 30 %). Exemple : 10 Mo/s × 7 jours × 3 ≈ 18 To. Le tiered storage (3.6+) déporte les segments anciens vers l'object storage et permet une rétention longue avec des disques locaux courts. Surveiller la croissance, et distinguer rétention métier (rejeu) et rétention technique.

### 74. Comment gérer la sérialisation JSON, Avro et Protobuf, et choisir ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** JSON : lisible, sans schéma imposé (JSON Schema possible), verbeux. Avro : compact, schéma évolutif avec registry, écosystème Kafka historique, génération de classes. Protobuf : compact, multi-langage, adapté aux équipes gRPC, évolution par numéros de champs. Choisir selon les consommateurs et l'écosystème ; toujours un schéma versionné pour les contrats entre équipes.

### 75. Comment fonctionne le Schema Registry en détail (subjects, stratégies de nommage, références) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un schéma est enregistré sous un subject (par défaut `topic-value`, `TopicNameStrategy` ; `RecordNameStrategy` pour plusieurs types d'événements par topic), reçoit un id global inclus dans chaque message (magic byte + id) ; les clients cachent les schémas. Les modes de compatibilité par subject empêchent les évolutions incompatibles. Les références de schéma permettent la composition ; Apicurio est l'alternative open source à Confluent.

### 76. Comment concevoir les événements : event-carried state transfer vs event notification, et le versionnement ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Notification : événement léger (id, type) obligeant le consommateur à rappeler la source (couplage temporel). State transfer : l'événement porte l'état nécessaire (autonomie, plus gros). Versionner par schéma compatible (ajouter des champs optionnels), header `event-type`/`version`, nouveaux topics pour les ruptures, et documenter avec AsyncAPI. Inclure identifiant unique, timestamp, source et corrélation.

### 77. Comment modéliser les topics : un par type d'événement, par entité ou par domaine ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Regrouper par entité/agrégat (`orders`) avec plusieurs types d'événements dans l'ordre (nécessaire pour les séquences créé → modifié → annulé sur une même clé), plutôt qu'un topic par type (ordre perdu entre types). Éviter les topics fourre-tout par domaine. Nommage : `<domaine>.<entité>.<type>` avec conventions, et propriété claire par équipe productrice.

### 78. Qu'est-ce que le CDC avec Debezium et ses patterns (outbox, snapshot) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Debezium (connecteur Kafka Connect) lit le journal de transactions (WAL PostgreSQL, binlog MySQL) et publie chaque changement de ligne (before/after, op, ts) sans impact sur l'application : réplication vers d'autres systèmes, cache, recherche, event sourcing léger. Le pattern outbox via Debezium (`EventRouter` SMT) publie des événements métier fiables. Prévoir le snapshot initial, la gestion du schéma et les données sensibles.

### 79. Comment fonctionnent les Single Message Transforms (SMT) et les converters de Kafka Connect ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Les converters (JSON, Avro, Protobuf) sérialisent entre le format interne de Connect et Kafka. Les SMT transforment chaque message en vol (`ExtractField`, `MaskField`, `TimestampRouter`, `Filter`, `RegexRouter`) sans code, chaînables par connecteur. Pour des transformations complexes, préférer Kafka Streams/Flink en aval plutôt que des SMT lourds.

### 80. Comment gérer les erreurs dans Kafka Connect (`errors.tolerance`, DLQ, retries) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `errors.tolerance=all` avec `errors.deadletterqueue.topic.name` envoie les messages non convertibles/transformables en DLQ (headers d'erreur si `errors.deadletterqueue.context.headers.enable`), `errors.retry.timeout`/`errors.retry.delay.max.ms` pour les erreurs transitoires, `errors.log.enable`. Les erreurs côté sink (base injoignable) font échouer la tâche : surveiller l'état des connecteurs (`/connectors/x/status`) et prévoir des redémarrages automatiques.

### 81. Comment fonctionne Kafka Streams en interne (topologie, tâches, threads, changelogs) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** La topologie (sources, processeurs, sinks) est découpée en sous-topologies ; chaque partition d'entrée crée une tâche (unité de parallélisme) répartie sur les `num.stream.threads` et instances. Les state stores locaux (RocksDB) sont sauvegardés dans des topics changelog compactés pour la restauration ; les repartitions internes créent des topics `-repartition`. `standby.replicas` accélèrent le failover.

### 82. Comment gérer l'exactly-once dans Kafka Streams (`processing.guarantee=exactly_once_v2`) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Il active les transactions : offsets consommés, écritures dans les state stores (changelog) et sorties sont validés atomiquement par `commit.interval.ms` (100 ms par défaut en EOS). `exactly_once_v2` (2.5+) utilise un producteur par thread et non par tâche, réduisant le coût. Les side effects externes (appels HTTP dans un processeur) ne sont pas couverts.

### 83. Comment implémenter une jointure stream-table et stream-stream, et quels pièges ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Stream-table (`KStream.join(KTable)`) : enrichissement par clé, la table doit être co-partitionnée (même clé et nombre de partitions) ou être une `GlobalKTable`. Stream-stream : jointure fenêtrée (`JoinWindows`) avec state stores des deux côtés, ordre d'arrivée et `grace` pour les retardataires. Pièges : clés non alignées (rekey = repartition), tables non préchargées au démarrage (timing), taille des fenêtres et mémoire.

### 84. Qu'est-ce que le suppress, les fenêtres avec grace period et la gestion des retardataires ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Par défaut, les agrégations fenêtrées émettent une mise à jour à chaque événement (résultats intermédiaires). `suppress(untilWindowCloses(...))` n'émet que le résultat final à la fermeture de la fenêtre + `grace` (période acceptant les événements en retard). Les événements arrivant après le grace sont ignorés (métriques `dropped-records`). Dimensionner le grace selon le retard réel observé.

### 85. Comment tester une topologie Kafka Streams ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `TopologyTestDriver` exécute la topologie en mémoire sans broker : `TestInputTopic.pipeInput(key, value, timestamp)`, `TestOutputTopic.readKeyValue()`, accès aux state stores, contrôle du temps (`advanceWallClockTime`) pour les fenêtres et punctuations. Compléter par des tests d'intégration avec Testcontainers pour la sérialisation et la configuration réelle.

### 86. Comment fonctionnent les Interactive Queries de Kafka Streams ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Chaque instance expose ses state stores locaux en lecture (`store(...)`), et connaît via `queryMetadataForKey` quelle instance héberge une clé donnée (par le `application.server`) : on construit une API qui route la requête vers la bonne instance. Cela permet de servir des vues matérialisées (compteurs, dernier état) directement depuis l'application sans base externe, avec les limites de disponibilité pendant les rebalances.

### 87. Kafka Streams ou Apache Flink : comment choisir ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Kafka Streams : bibliothèque embarquée dans une application Java, déploiement simple (Kubernetes standard), état local, adaptée aux transformations et agrégations Kafka→Kafka. Flink : moteur distribué avec cluster dédié, SQL, fenêtres et état avancés, sources/sinks multiples (non Kafka), checkpoints, adapté aux pipelines analytiques complexes et aux gros volumes. Flink demande plus d'exploitation ; Confluent propose Flink managé.

### 88. Qu'est-ce que les Share Groups (« Queues for Kafka », KIP-932) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Un nouveau mode de consommation (Kafka 4.0+, early access) où plusieurs consommateurs d'un share group peuvent lire la même partition, avec acquittement (ack/release/reject) par message et redélivrance, comme une file traditionnelle : ordre non garanti mais parallélisme indépendant du nombre de partitions. Il vise les cas d'usage type worker queue jusque-là mieux servis par RabbitMQ/SQS.

### 89. Comment sécuriser finement Kafka avec les ACLs et OAuth ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Authentification : SASL/SCRAM, mTLS, ou SASL/OAUTHBEARER avec un IdP (Keycloak) pour des jetons courts. Autorisation : ACLs par principal sur topics, groupes, transactional ids et cluster (`--allow-principal User:app --operation Read --topic orders --group app`), avec préfixes (`--resource-pattern-type prefixed`) pour les conventions de nommage, et `allow.everyone.if.no.acl.found=false`. Chiffrement TLS et audit des accès via les logs d'autorisation.

### 90. Comment gérer le multi-tenant sur un cluster Kafka partagé ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Conventions de nommage par équipe/domaine avec ACLs préfixées, quotas par principal (produce/fetch/requests), topics créés par un processus (GitOps : Strimzi `KafkaTopic`, Terraform) et non `auto.create.topics.enable`, tags/labels de propriété, Schema Registry avec droits par subject, et supervision du coût par tenant (débit, stockage). Isoler les tenants critiques sur des clusters séparés si nécessaire.

### 91. Comment planifier une migration ou un changement de cluster Kafka sans interruption ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** MirrorMaker 2 (ou Cluster Linking Confluent) réplique topics, offsets traduits et ACLs vers le nouveau cluster ; migrer d'abord les consommateurs (avec offsets traduits via `MirrorCheckpointConnector`/`RemoteClusterUtils`), puis les producteurs, en gardant les deux clusters synchronisés le temps de la bascule ; prévoir l'idempotence des consommateurs pendant la période de recouvrement. Tester le rollback.

### 92. Comment gérer la reprise après sinistre (DR) et le multi-région ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Actif-passif : MirrorMaker 2 vers une région secondaire, bascule DNS/configuration des clients, RPO = lag de réplication. Actif-actif : chaque région produit localement et réplique vers l'autre (topics préfixés pour éviter les boucles), avec des consommateurs lisant les deux ; complexité de l'ordre et des doublons. Stretch cluster (une seule instance sur plusieurs AZ proches, `rack awareness`) pour la haute disponibilité intra-région.

### 93. Quelles sont les limites de Kafka et quand ne pas l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Pas de file avec acquittement par message ni de priorités (share groups en cours), pas de requêtes par contenu, latence de quelques ms (pas des µs), coût d'exploitation (ou managé), overkill pour de petits volumes ou des cas simples de requête/réponse. Alternatives : RabbitMQ/SQS pour les worker queues, base de données pour l'état, gRPC/REST pour le synchrone, NATS/Pulsar selon les besoins.

### 94. Comment fonctionne Apache Pulsar ou Redpanda par rapport à Kafka ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Redpanda : réimplémentation compatible API Kafka en C++, sans JVM ni ZooKeeper, un seul binaire, latence plus faible et exploitation simplifiée. Pulsar : architecture séparée calcul (brokers)/stockage (BookKeeper), multi-tenant natif, files et streams unifiés, géo-réplication intégrée, mais écosystème plus restreint. Kafka reste la référence par son écosystème (Connect, Streams, registry, offres managées).

### 95. Comment consommer Kafka de façon réactive (Reactor Kafka, Spring Cloud Stream réactif) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** `reactor-kafka` fournit `KafkaReceiver` (flux de records avec acquittement/commit manuel via `ReceiverOffset`) et `KafkaSender` : intégration avec la backpressure Reactor, traitement par `flatMap` borné, commit groupé. Pièges : ordre par partition à préserver (`groupBy(partition)` + `concatMap`), gestion des erreurs et retries dans la chaîne. Avec les virtual threads, le consommateur bloquant classique est souvent plus simple.

### 96. Comment fonctionne l'idempotence des producteurs en détail (PID, sequence numbers) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Le broker attribue un Producer ID ; chaque batch porte un numéro de séquence par partition ; le broker rejette les doublons (`DuplicateSequenceException` ignorée côté client) et détecte les trous (`OutOfOrderSequenceException`). Cela garantit exactly-once par session de producteur et par partition ; le `transactional.id` étend la garantie aux redémarrages (fencing des anciens producteurs via epoch).

### 97. Comment configurer les timeouts client cohérents (`request.timeout.ms`, `delivery.timeout.ms`, `session.timeout.ms`) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Producteur : `delivery.timeout.ms` (borne totale, ≥ `linger.ms` + `request.timeout.ms`) englobe retries ; `max.block.ms` borne `send()` quand le buffer est plein ou les métadonnées absentes. Consommateur : `session.timeout.ms` (détection de panne, avec `heartbeat.interval.ms` ≈ 1/3) et `max.poll.interval.ms` (temps max de traitement par poll). Aligner avec les timeouts applicatifs et le graceful shutdown.

### 98. Comment réaliser un audit ou un rejeu ciblé (par période, par clé) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Rejeu par période : `kafka-consumer-groups --reset-offsets --to-datetime` (ou `offsetsForTimes` via l'API) sur un groupe dédié. Rejeu par clé : consommer la plage et filtrer (Kafka n'indexe pas par clé) ; pour des besoins fréquents, maintenir une vue indexée (Kafka Streams, base) ou utiliser un topic compacté. Documenter la procédure et l'impact sur les consommateurs (idempotence obligatoire).

### 99. Comment documenter et gouverner les topics (AsyncAPI, catalogue, propriété) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** AsyncAPI décrit les canaux, messages et schémas comme OpenAPI pour le REST (générateurs de docs et de code). Un catalogue (Conduktor, Confluent Stream Catalog, Backstage plugin) recense propriétaires, SLA, rétention, schémas, consommateurs. Politiques : revue des nouveaux topics, conventions de nommage, dépréciation avec préavis, et alertes sur les topics sans consommateurs.

### 100. Comment estimer la capacité d'un cluster (brokers, partitions, réseau) ?
`🟠 Intermédiaire` · Sujet : **Kafka**

**Réponse :** Partir du débit entrant (Mo/s) × réplication pour le réseau et le disque (écriture) plus la lecture par le nombre de groupes de consommateurs ; limiter à quelques milliers de partitions par broker (KRaft relève la limite globale) ; CPU dominé par la compression/TLS ; mémoire pour le page cache (les consommateurs à jour lisent en cache). Prévoir 30-50 % de marge et tester avec `kafka-producer-perf-test`/`kafka-consumer-perf-test`.
