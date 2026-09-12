# 📨 Apache Kafka

> Topics, partitions, consumer groups, Streams, exactly-once semantics

**50 questions**

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
