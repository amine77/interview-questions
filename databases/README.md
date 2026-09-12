# 🗄️ Databases

> SQL, MongoDB, Redis, Elasticsearch, distributed databases, migrations

**51 questions**

---

### 1. Quelle est la différence entre `INNER JOIN` et `LEFT JOIN` ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** `INNER JOIN` retourne uniquement les lignes ayant une correspondance dans les deux tables. `LEFT JOIN` retourne toutes les lignes de la table de gauche, avec `NULL` pour les colonnes de la table de droite si aucune correspondance n'existe.

### 2. Différence entre base relationnelle et MongoDB ?
`🟢 Débutant` · Sujet : **MongoDB**

**Réponse :** MongoDB est NoSQL orienté documents (BSON, sans schéma rigide) vs tables avec schéma fixe et clés étrangères.

### 3. À quoi sert une clé étrangère ?
`🟢 Débutant` · Sujet : **SQL**

**Réponse :** Établit une relation entre deux tables référençant une clé primaire, garantissant l'intégrité référentielle.

### 4. Qu'est-ce que l'aggregation pipeline ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Framework de traitement de documents via étapes ($match, $group, $sort, $project...), similaire à GROUP BY SQL.

### 5. Qu'est-ce qu'un index ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Structure (B-tree) accélérant la recherche, au prix d'espace disque et de ralentissement des écritures.

### 6. Qu'est-ce qu'un document MongoDB ?
`🟢 Débutant` · Sujet : **MongoDB**

**Réponse :** Unité de stockage BSON, équivalent conceptuel d'une ligne relationnelle mais structure flexible/imbriquée.

### 7. Différence `WHERE` / `HAVING` ?
`🟢 Débutant` · Sujet : **SQL**

**Réponse :** WHERE filtre avant regroupement. HAVING filtre les groupes après agrégation.

### 8. Propriétés ACID ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Atomicité, Cohérence, Isolation, Durabilité.

### 9. Qu'est-ce que le sharding ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Partitionnement horizontal des données sur plusieurs shards selon une clé de sharding.

### 10. Différence `DELETE` / `TRUNCATE` / `DROP` ?
`🟢 Débutant` · Sujet : **SQL**

**Réponse :** DELETE = suppression conditionnelle journalisée. TRUNCATE = suppression rapide de toutes les lignes. DROP = suppression de la structure.

### 11. Différence `find()` / `findOne()` ?
`🟢 Débutant` · Sujet : **MongoDB**

**Réponse :** find() retourne un curseur (plusieurs résultats). findOne() retourne le premier document ou null.

### 12. Qu'est-ce qu'une vue (VIEW) ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Requête stockée présentée comme table virtuelle, simplifiant l'accès à des requêtes complexes.

### 13. Qu'est-ce qu'un replica set ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Groupe de serveurs maintenant les mêmes données, avec primaire/secondaires et élection automatique.

### 14. Qu'est-ce qu'une procédure stockée ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Instructions SQL précompilées et stockées, appelables comme une fonction.

### 15. Quels sont les principaux cas d'usage de Redis au-delà du simple cache ?
`🟠 Intermédiaire` · Sujet : **Redis**

**Réponse :** Pub/Sub pour la messagerie temps réel, structures de données avancées (listes, sets, sorted sets, hashes) pour des leaderboards ou files d'attente, gestion de sessions distribuées, rate limiting via des compteurs atomiques, et verrous distribués (Redlock).

### 16. Qu'est-ce que Flyway ou Liquibase et pourquoi les utiliser ?
`🟢 Débutant` · Sujet : **Migrations de schéma**

**Réponse :** Des outils de gestion versionnée des migrations de schéma de base de données, appliquant automatiquement des scripts SQL (ou changelogs) dans un ordre déterminé et traçable, garantissant que tous les environnements restent synchronisés sans intervention manuelle.

### 17. Quelle est la différence entre une recherche full-text avec Elasticsearch et une requête SQL LIKE ?
`🟢 Débutant` · Sujet : **Elasticsearch**

**Réponse :** Elasticsearch utilise un index inversé optimisé, offrant scoring de pertinence, tolérance aux fautes, analyse linguistique et performances supérieures à grande échelle, contrairement à LIKE qui effectue un scan de texte simple.

### 18. Qu'est-ce que le théorème CAP et comment influence-t-il le choix d'une base distribuée ?
`🟠 Intermédiaire` · Sujet : **Cassandra/CockroachDB**

**Réponse :** Un système distribué ne peut garantir que deux des trois propriétés (Cohérence, Disponibilité, Tolérance au partitionnement). Cassandra privilégie AP, CockroachDB vise CP avec consensus distribué (Raft).

### 19. Différence entre EXPIRE et PERSIST ?
`🟢 Débutant` · Sujet : **Redis**

**Réponse :** EXPIRE définit un TTL après lequel la clé est supprimée. PERSIST retire ce TTL, rendant la clé permanente.

### 20. Qu'est-ce qu'un "analyzer" dans Elasticsearch ?
`🟠 Intermédiaire` · Sujet : **Elasticsearch**

**Réponse :** Pipeline combinant un tokenizer et des filtres (minuscules, mots vides, stemming), déterminant comment le texte est transformé en termes recherchables.

### 21. Quels sont les niveaux d'isolation des transactions et quels phénomènes évitent-ils ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** `READ UNCOMMITTED` (lectures sales possibles), `READ COMMITTED` (défaut PostgreSQL/Oracle, évite les dirty reads), `REPEATABLE READ` (défaut MySQL, évite aussi les non-repeatable reads), `SERIALIZABLE` (évite les phantom reads, comme si les transactions étaient séquentielles). Plus le niveau est élevé, plus le risque de contention/deadlock augmente.

### 22. Qu'est-ce que le MVCC ?
`🔴 Avancé` · Sujet : **SQL**

**Réponse :** Le Multi-Version Concurrency Control conserve plusieurs versions d'une ligne pour que les lecteurs ne bloquent pas les écrivains et inversement : chaque transaction voit un snapshot cohérent. PostgreSQL stocke les anciennes versions dans la table (d'où le besoin de `VACUUM`), Oracle et MySQL/InnoDB dans des segments d'undo.

### 23. Comment lire un plan d'exécution (`EXPLAIN ANALYZE`) ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** On repère les nœuds coûteux : `Seq Scan` sur une grande table (index manquant), `Nested Loop` sur de gros volumes, estimation de lignes très différente du réel (statistiques obsolètes → `ANALYZE`), tri sur disque (`work_mem` insuffisant). `EXPLAIN (ANALYZE, BUFFERS)` ajoute les I/O réelles.

### 24. Différence entre index B-tree, Hash, GIN et BRIN ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** B-tree : usage général, égalité et plages, tri. Hash : égalité seule. GIN (inversé) : valeurs multiples par ligne, JSONB, tableaux, full-text. BRIN : résumés par bloc pour les très grandes tables physiquement ordonnées (séries temporelles), très compact. GiST couvre la géométrie et les données spatiales.

### 25. Qu'est-ce qu'un index composite et pourquoi l'ordre des colonnes compte-t-il ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Un index sur `(a, b)` est trié d'abord par `a`, puis par `b` : il sert les requêtes filtrant sur `a` ou sur `a et b`, mais pas sur `b` seul (règle du préfixe le plus à gauche). On place en premier la colonne la plus sélective utilisée en égalité, puis les colonnes de plage.

### 26. Qu'est-ce qu'un index couvrant (covering index) ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Un index contenant toutes les colonnes nécessaires à la requête, permettant un `Index Only Scan` sans accéder à la table. En PostgreSQL, `CREATE INDEX ... INCLUDE (col)` ajoute des colonnes non triées à la feuille de l'index.

### 27. Qu'est-ce qu'une fonction de fenêtrage (window function) ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Une fonction calculée sur un ensemble de lignes liées à la ligne courante sans les agréger : `ROW_NUMBER()`, `RANK()`, `LAG()`, `LEAD()`, `SUM() OVER (PARTITION BY ... ORDER BY ...)`. Idéale pour les classements, cumuls, comparaisons avec la ligne précédente, et la déduplication.

### 28. Qu'est-ce qu'une CTE (`WITH`) et une CTE récursive ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Une Common Table Expression nomme une sous-requête temporaire pour améliorer la lisibilité. La forme `WITH RECURSIVE` permet de parcourir des hiérarchies (organigramme, arbre de catégories) ou des graphes. En PostgreSQL 12+, une CTE est inlinée sauf si `MATERIALIZED` est précisé.

### 29. Différence entre `UNION` et `UNION ALL` ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** `UNION` supprime les doublons (tri/hachage coûteux). `UNION ALL` concatène simplement les résultats, plus rapide. Utiliser `UNION ALL` par défaut sauf si la déduplication est réellement nécessaire.

### 30. Qu'est-ce que la normalisation (1NF, 2NF, 3NF) et quand dénormaliser ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** 1NF : valeurs atomiques ; 2NF : pas de dépendance partielle à une partie de la clé ; 3NF : pas de dépendance transitive entre attributs non-clés. Dénormaliser (dupliquer, précalculer) se justifie pour la performance en lecture (reporting, vues matérialisées), au prix de la cohérence à maintenir.

### 31. Qu'est-ce qu'une vue matérialisée ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Une vue dont le résultat est stocké physiquement, rafraîchi à la demande (`REFRESH MATERIALIZED VIEW CONCURRENTLY`) ou par planification. Elle accélère les requêtes d'agrégation lourdes au prix de données potentiellement périmées.

### 32. Qu'est-ce qu'un deadlock en base de données et comment l'éviter ?
`🔴 Avancé` · Sujet : **SQL**

**Réponse :** Deux transactions attendent chacune un verrou tenu par l'autre ; le SGBD en tue une. Prévention : acquérir les verrous dans un ordre constant, transactions courtes, indexes adéquats (moins de lignes verrouillées), `SELECT ... FOR UPDATE SKIP LOCKED` pour les files de travail, et réessayer côté application.

### 33. Différence entre clé primaire naturelle, séquentielle et UUID ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Une clé naturelle (email, SIRET) peut changer. Un entier auto-incrémenté est compact et localement ordonné (bonnes performances d'index) mais devine-able et difficile en multi-région. Un UUIDv4 est unique globalement mais fragmente les index B-tree ; UUIDv7 (ordonné dans le temps) combine les deux avantages.

### 34. Comment paginer efficacement une grande table ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** `OFFSET n` oblige à lire et jeter n lignes, de plus en plus lent. La pagination par curseur (keyset) filtre sur la dernière clé vue : `WHERE (created_at, id) < (?, ?) ORDER BY created_at DESC, id DESC LIMIT 20`, ce qui reste O(log n) grâce à l'index.

### 35. Qu'est-ce que le partitionnement de tables ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Découper une table logique en sous-tables physiques par plage (dates), liste (région) ou hachage. Le planificateur ne lit que les partitions pertinentes (partition pruning), et supprimer d'anciennes données devient un `DROP PARTITION` instantané. Contrepartie : contraintes d'unicité globales limitées.

### 36. Comment fonctionne la réplication (streaming) et quelle différence entre synchrone et asynchrone ?
`🔴 Avancé` · Sujet : **SQL**

**Réponse :** Le primaire envoie son journal de transactions (WAL/binlog) aux réplicas. En asynchrone, le commit n'attend pas les réplicas (rapide, risque de perte au failover). En synchrone, il attend l'accusé d'au moins un réplica (durabilité garantie, latence accrue). Les réplicas servent les lectures et permettent le failover.

### 37. Qu'est-ce que JSONB en PostgreSQL et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **SQL**

**Réponse :** Un type JSON binaire indexable (GIN) supportant les opérateurs `->`, `->>`, `@>`, `?`. Il convient aux attributs semi-structurés ou variables (métadonnées, préférences). Ne pas y stocker ce qui doit être joint, contraint ou agrégé fréquemment : garder un modèle relationnel pour le cœur du domaine.

### 38. Quelle stratégie choisir entre embarquer et référencer des documents ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Embarquer (sous-documents) quand les données sont lues ensemble et ont un cardinalité bornée (adresse d'un client). Référencer (`ObjectId` + `$lookup` ou seconde requête) pour les relations many-to-many, les données volumineuses ou mises à jour indépendamment. Limite : 16 Mo par document.

### 39. Comment fonctionnent les transactions multi-documents dans MongoDB ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Depuis la 4.0 (replica set) et 4.2 (sharded), une session peut englober plusieurs opérations avec `startTransaction()`/`commitTransaction()` en respectant ACID. Elles coûtent plus cher que les écritures atomiques sur un seul document : privilégier une modélisation qui rend les opérations mono-document.

### 40. Quelle est la différence entre `write concern` et `read concern` ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Le write concern définit combien de membres doivent confirmer une écriture (`w: 1`, `w: "majority"`, `j: true` pour le journal). Le read concern définit la fraîcheur/durabilité des lectures (`local`, `majority`, `linearizable`). `majority` des deux côtés évite de lire des données pouvant être annulées lors d'un rollback.

### 41. Qu'est-ce qu'un index TTL et un index partiel ?
`🟠 Intermédiaire` · Sujet : **MongoDB**

**Réponse :** Un index TTL (`expireAfterSeconds`) sur un champ date supprime automatiquement les documents expirés (sessions, logs). Un index partiel (`partialFilterExpression`) n'indexe que les documents satisfaisant un filtre, réduisant sa taille (ex : commandes `status: "open"` seulement).

### 42. Quelles structures de données propose Redis et pour quels usages ?
`🟠 Intermédiaire` · Sujet : **Redis**

**Réponse :** Strings (cache, compteurs `INCR`), Hashes (objets), Lists (files simples), Sets (unicité, tags), Sorted Sets (classements, files avec priorité/temps), Streams (log d'événements avec consumer groups), HyperLogLog (comptage approximatif d'uniques), Bitmaps, Geo. Choisir la structure évite de sérialiser du JSON en bloc.

### 43. Comment Redis assure-t-il la persistance et quelle stratégie choisir ?
`🟠 Intermédiaire` · Sujet : **Redis**

**Réponse :** RDB : snapshots périodiques compacts, rapide au redémarrage, perte possible des dernières minutes. AOF : journal de chaque écriture (`appendfsync everysec`), plus durable, fichiers plus gros. En production on combine souvent les deux ; un cache pur peut se passer de persistance.

### 44. Comment implémenter un verrou distribué avec Redis et quelles sont ses limites ?
`🔴 Avancé` · Sujet : **Redis**

**Réponse :** `SET key token NX PX 30000` acquiert le verrou de façon atomique avec expiration ; la libération vérifie le token via un script Lua. Limites : expiration pendant un traitement long (livrer un « fencing token »), pas de garantie forte en cas de failover asynchrone (débat Redlock). Pour des garanties fortes, préférer un verrou en base ou ZooKeeper/etcd.

### 45. Quelles stratégies d'éviction et de cache existent ?
`🟠 Intermédiaire` · Sujet : **Redis**

**Réponse :** Politiques d'éviction quand `maxmemory` est atteint : `allkeys-lru`, `volatile-lru`, `allkeys-lfu`, `volatile-ttl`, `noeviction`. Stratégies applicatives : cache-aside (l'application lit/écrit le cache), read-through, write-through, write-behind. Toujours prévoir un TTL et gérer la « cache stampede » (verrou ou jitter sur l'expiration).

### 46. Différence entre un `match`, un `term` et un `keyword` field ?
`🔴 Avancé` · Sujet : **Elasticsearch**

**Réponse :** `term` cherche la valeur exacte non analysée, à utiliser sur un champ `keyword` (ids, statuts). `match` analyse la requête (tokenisation, minuscules) et cherche dans un champ `text` avec scoring de pertinence. Chercher `term` sur un champ `text` échoue souvent car la valeur stockée est déjà tokenisée.

### 47. Différence entre shard primaire et réplica, et comment dimensionner ?
`🟠 Intermédiaire` · Sujet : **Elasticsearch**

**Réponse :** Un index est découpé en shards primaires (parallélisme, fixé à la création) dupliqués en réplicas (haute disponibilité, débit de lecture). Règle empirique : 10 à 50 Go par shard, éviter des milliers de petits shards (surcharge mémoire du master). Utiliser ILM et les rollovers pour les données temporelles.

### 48. Qu'est-ce qu'une agrégation et la différence bucket/metric ?
`🟠 Intermédiaire` · Sujet : **Elasticsearch**

**Réponse :** Les agrégations calculent des statistiques sur les résultats. Les agrégations *metric* produisent une valeur (`avg`, `sum`, `cardinality`), les *bucket* regroupent les documents (`terms`, `date_histogram`, `range`) et peuvent s'imbriquer. C'est le moteur des dashboards Kibana.

### 49. Comment modélise-t-on les données dans Cassandra (query-first) ?
`🔴 Avancé` · Sujet : **Cassandra/CockroachDB**

**Réponse :** On part des requêtes : chaque table est conçue pour une requête, avec la partition key choisie pour répartir uniformément et regrouper ce qui est lu ensemble, et les clustering columns pour l'ordre. La dénormalisation est la norme (pas de jointure), et les tombstones des suppressions massives doivent être surveillés.

### 50. Qu'est-ce qu'une base NewSQL comme CockroachDB ou YugabyteDB ?
`🔴 Avancé` · Sujet : **Cassandra/CockroachDB**

**Réponse :** Une base distribuée offrant SQL et transactions ACID sérialisables tout en étant horizontalement scalable et résiliente aux pannes de nœud, via le consensus Raft par plage de données. Compromis : latence d'écriture supérieure à PostgreSQL mono-nœud, coût des transactions multi-régions, quelques fonctionnalités SQL manquantes.

### 51. Comment faire évoluer un schéma sans interruption de service (zero-downtime) ?
`🟠 Intermédiaire` · Sujet : **Migrations de schéma**

**Réponse :** Pattern expand/contract : ajouter la nouvelle colonne nullable, déployer le code qui écrit dans l'ancienne et la nouvelle, migrer les données par lots, basculer les lectures, puis supprimer l'ancienne colonne dans une release ultérieure. Éviter les `ALTER` bloquants (`NOT NULL` avec défaut sur grosse table, index sans `CONCURRENTLY`).
