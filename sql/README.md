# 🧮 SQL avancé & PostgreSQL

> Requêtes complexes, modélisation, index, transactions, performance, PostgreSQL

**51 questions**

---

### 1. Dans quel ordre logique une requête SQL est-elle évaluée ?
`🟢 Débutant` · Sujet : **Bases SQL**

**Réponse :** `FROM`/`JOIN` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` (et window functions) → `DISTINCT` → `ORDER BY` → `LIMIT/OFFSET`. Cet ordre explique pourquoi un alias du `SELECT` n'est pas utilisable dans `WHERE`, pourquoi `WHERE` filtre avant l'agrégation et `HAVING` après, et pourquoi les window functions ne peuvent pas être filtrées sans sous-requête ou CTE.

### 2. Différence entre `LEFT JOIN` avec condition dans `ON` et dans `WHERE` ?
`🟢 Débutant` · Sujet : **Bases SQL**

**Réponse :** Une condition sur la table de droite placée dans `ON` filtre les lignes à joindre en conservant les lignes de gauche sans correspondance (NULL) ; la même condition dans `WHERE` élimine ces lignes (le `LEFT JOIN` devient de fait un `INNER JOIN`). Pour « clients sans commande en 2025 », la condition sur la date va dans `ON` et `WHERE commande.id IS NULL`.

### 3. Comment fonctionne `NULL` en SQL et quels pièges ?
`🟢 Débutant` · Sujet : **Bases SQL**

**Réponse :** `NULL` est « inconnu » : `NULL = NULL` est inconnu (utiliser `IS NULL`, `IS DISTINCT FROM`), `NOT IN (sous-requête contenant NULL)` ne renvoie rien, les agrégats ignorent les NULL (`COUNT(col)` vs `COUNT(*)`), `AVG` exclut les NULL du dénominateur, la concaténation avec NULL donne NULL, et les NULL se trient en premier ou dernier selon la base (`NULLS LAST`). `COALESCE` fournit une valeur par défaut.

### 4. Différence entre `EXISTS`, `IN` et un `JOIN` pour filtrer sur une autre table ?
`🟢 Débutant` · Sujet : **Bases SQL**

**Réponse :** `EXISTS` s'arrête à la première correspondance et gère bien les NULL ; `IN` est équivalent pour de petites listes mais dangereux avec NULL et `NOT IN` ; un `JOIN` peut dupliquer les lignes si la table jointe a plusieurs correspondances (nécessitant `DISTINCT`). Les optimiseurs modernes réécrivent souvent ces formes en semi-jointures ; préférer `EXISTS` pour la sémantique « au moins un ».

### 5. Qu'est-ce qu'une sous-requête corrélée et quel est son coût ?
`🟢 Débutant` · Sujet : **Bases SQL**

**Réponse :** Une sous-requête référençant la requête externe (`WHERE prix > (SELECT AVG(prix) FROM p WHERE p.cat = ext.cat)`), évaluée conceptuellement pour chaque ligne. L'optimiseur la transforme parfois en jointure ; sinon elle devient O(n×m). Alternatives : jointure sur une agrégation groupée, window function, ou `LATERAL` quand on veut les k premières lignes par groupe.

### 6. Comment obtenir les N premières lignes par groupe (top-N per group) ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** Window function : `SELECT * FROM (SELECT *, ROW_NUMBER() OVER (PARTITION BY client_id ORDER BY date DESC) rn FROM commandes) t WHERE rn <= 3`. Alternative PostgreSQL : `DISTINCT ON (client_id)` pour N=1, ou `LATERAL` join (`CROSS JOIN LATERAL (SELECT ... WHERE c.client_id = cl.id ORDER BY date DESC LIMIT 3)`) qui exploite bien un index.

### 7. Différence entre `ROW_NUMBER`, `RANK` et `DENSE_RANK` ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** `ROW_NUMBER` numérote sans ex æquo (1,2,3,4), `RANK` donne le même rang aux égalités et saute (1,2,2,4), `DENSE_RANK` ne saute pas (1,2,2,3). `NTILE(n)` répartit en n groupes. Le choix dépend du besoin : pagination/dédoublonnage (`ROW_NUMBER`), classements (`RANK`/`DENSE_RANK`).

### 8. Comment calculer un cumul, une moyenne mobile et une comparaison avec la ligne précédente ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** Cumul : `SUM(montant) OVER (PARTITION BY client ORDER BY date)`. Moyenne mobile 7 jours : `AVG(v) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)`. Ligne précédente : `LAG(v, 1) OVER (ORDER BY date)` (et `LEAD` pour la suivante), utile pour les variations et les écarts entre événements. `RANGE` vs `ROWS` change la sémantique en cas d'égalités.

### 9. Qu'est-ce que le problème des « gaps and islands » et comment le résoudre ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** Identifier des séquences consécutives (jours de connexion d'affilée, plages de numéros) : soustraire un `ROW_NUMBER` à la valeur (`date - ROW_NUMBER() OVER (ORDER BY date) * INTERVAL '1 day'`) donne une constante par île ; grouper dessus pour obtenir début, fin et longueur. Variante avec `LAG` pour détecter les ruptures puis cumuler un compteur de groupe.

### 10. Comment écrire une requête récursive (hiérarchie, graphe) ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** `WITH RECURSIVE arbre AS (SELECT id, parent_id, nom, 1 AS niveau FROM cat WHERE parent_id IS NULL UNION ALL SELECT c.id, c.parent_id, c.nom, a.niveau + 1 FROM cat c JOIN arbre a ON c.parent_id = a.id) SELECT * FROM arbre`. Ajouter un chemin (`ARRAY[id]` ou texte) et une condition `NOT id = ANY(path)` pour éviter les cycles ; `LIMIT`/profondeur maximale par sécurité. Alternatives : `ltree`, closure table.

### 11. Comment pivoter des lignes en colonnes et inversement ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** Pivot : agrégation conditionnelle `SUM(CASE WHEN mois = 1 THEN montant END) AS jan, ...` ou `SUM(montant) FILTER (WHERE mois = 1)` (PostgreSQL), ou `crosstab` (extension tablefunc). Unpivot : `UNION ALL` par colonne, ou `LATERAL (VALUES (...))`/`unnest` en PostgreSQL. Les colonnes dynamiques doivent être générées côté application.

### 12. Comment gérer les doublons : détecter, supprimer, éviter ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** Détecter : `GROUP BY colonnes HAVING COUNT(*) > 1`. Supprimer en gardant une ligne : `DELETE FROM t WHERE id IN (SELECT id FROM (SELECT id, ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) rn FROM t) x WHERE rn > 1)`. Éviter : contrainte `UNIQUE` (éventuellement partielle ou sur une expression comme `lower(email)`) et `INSERT ... ON CONFLICT` pour l'upsert.

### 13. Comment fonctionne `INSERT ... ON CONFLICT` (upsert) et `MERGE` ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** PostgreSQL : `INSERT INTO t (k, v) VALUES (...) ON CONFLICT (k) DO UPDATE SET v = EXCLUDED.v WHERE t.v IS DISTINCT FROM EXCLUDED.v` (ou `DO NOTHING`), atomique et adapté à la concurrence ; nécessite un index unique sur la cible. `MERGE` (PostgreSQL 15+, standard SQL) gère plusieurs conditions `WHEN MATCHED/NOT MATCHED` mais n'est pas protégé contre les insertions concurrentes de la même façon.

### 14. Comment écrire des requêtes sur les dates correctement (fuseaux, intervalles, bornes) ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** Stocker en `timestamptz` (UTC), comparer par bornes semi-ouvertes (`date >= '2025-01-01' AND date < '2025-02-01'`) plutôt que `BETWEEN` ou `DATE(col)` (qui empêche l'index), utiliser `date_trunc` pour grouper, `generate_series` pour remplir les jours sans données, `AT TIME ZONE` pour l'affichage local, et faire attention aux changements d'heure (durées en `interval`, calculs en UTC).

### 15. Quelles sont les fonctions JSON utiles en PostgreSQL et comment indexer JSONB ?
`🟠 Intermédiaire` · Sujet : **Requêtes**

**Réponse :** `->`/`->>` (accès, texte), `#>>` (chemin), `@>` (contient, indexable GIN), `?` (clé existe), `jsonb_set`, `jsonb_build_object`, `jsonb_agg`, `jsonb_array_elements` (unnest), `jsonb_path_query` (JSONPath). Index : GIN sur la colonne (`jsonb_path_ops` plus compact pour `@>`), ou index B-tree sur une expression (`(data->>'email')`) pour les égalités fréquentes. Ne pas remplacer les colonnes structurées par du JSON.

### 16. Comment modéliser l'héritage (sous-types) en relationnel ?
`🟠 Intermédiaire` · Sujet : **Modélisation**

**Réponse :** Table unique avec discriminant (simple, colonnes NULL, contraintes `CHECK` par type), table par sous-type jointe à une table parent (normalisé, jointures), ou table par classe concrète (pas de parent, requêtes globales par `UNION`). Choix selon la fréquence des requêtes polymorphes et des attributs spécifiques ; JPA supporte les trois (`@Inheritance`).

### 17. Comment modéliser une relation plusieurs-à-plusieurs avec attributs et l'historisation ?
`🟠 Intermédiaire` · Sujet : **Modélisation**

**Réponse :** Table d'association avec clé composée (ou surrogate + `UNIQUE`) et ses propres colonnes (rôle, date d'ajout). Historisation : colonnes `valid_from`/`valid_to` (SCD type 2), contrainte d'exclusion PostgreSQL (`EXCLUDE USING gist (id WITH =, tsrange(valid_from, valid_to) WITH &&)`) pour éviter les chevauchements, ou tables d'audit alimentées par trigger/temporal tables (SQL:2011 dans certaines bases).

### 18. Quand dénormaliser et comment garder la cohérence ?
`🟠 Intermédiaire` · Sujet : **Modélisation**

**Réponse :** Dénormaliser (colonnes calculées, compteurs, copies) pour éviter des jointures ou agrégations coûteuses en lecture intensive. Garder la cohérence par colonnes générées (`GENERATED ALWAYS AS ... STORED`), triggers, vues matérialisées rafraîchies, ou mise à jour applicative dans la même transaction, avec des jobs de réconciliation. Documenter chaque redondance et sa source de vérité.

### 19. Quels types de clés primaires choisir : serial, identity, UUID v4, UUID v7, ULID ?
`🟠 Intermédiaire` · Sujet : **Modélisation**

**Réponse :** `IDENTITY`/séquence : compact, index B-tree ordonné (insertions séquentielles efficaces), prédictible (énumération possible via l'API). UUID v4 : globalement unique, généré côté client, mais aléatoire → fragmentation d'index et cache. UUID v7 (PostgreSQL 18 natif) ou ULID : uniques et ordonnés dans le temps, meilleur compromis pour les systèmes distribués. Exposer un identifiant public distinct de la clé interne si nécessaire.

### 20. Quelles contraintes utiliser pour garantir l'intégrité (CHECK, UNIQUE partiel, EXCLUDE, FK avec actions) ?
`🟠 Intermédiaire` · Sujet : **Modélisation**

**Réponse :** `CHECK` pour les domaines de valeurs (`quantite > 0`, énumérations), `UNIQUE` partiel (`WHERE deleted_at IS NULL` pour l'unicité des actifs), contraintes d'exclusion pour les chevauchements de plages, clés étrangères avec `ON DELETE CASCADE|RESTRICT|SET NULL` choisi explicitement, `NOT NULL` systématique sauf raison, `DEFERRABLE INITIALLY DEFERRED` pour les cycles. La base est la dernière ligne de défense de la cohérence.

### 21. Comment concevoir une table d'audit ou de journal d'événements en SQL ?
`🟠 Intermédiaire` · Sujet : **Modélisation**

**Réponse :** Table append-only (id ordonné, timestamp, acteur, entité, type, payload JSONB before/after), remplie par trigger (`row_to_json(OLD/NEW)`) ou par l'application, partitionnée par mois pour la purge, index sur (entité, id) et sur le temps, droits en écriture uniquement pour l'application (pas de `UPDATE/DELETE`), et export vers un entrepôt pour l'analyse. Alternative : CDC/Debezium vers Kafka.

### 22. Quand un index n'est-il pas utilisé par l'optimiseur ?
`🟠 Intermédiaire` · Sujet : **Index**

**Réponse :** Fonction ou cast sur la colonne (`lower(email)`, `date(ts)`) sans index d'expression, `LIKE '%x'` (préfixe inconnu), type incompatible (comparaison texte/entier), sélectivité faible (la table est petite ou le filtre ramène > 5-10 % des lignes : le seq scan est moins cher), statistiques obsolètes, `OR` entre colonnes différentes, première colonne d'un index composite absente du filtre, ou `NOT`/`<>`.

### 23. Qu'est-ce qu'un index partiel, un index d'expression et un index `INCLUDE` ?
`🟠 Intermédiaire` · Sujet : **Index**

**Réponse :** Partiel : `CREATE INDEX ON commandes (client_id) WHERE statut = 'EN_COURS'` (petit, ciblé sur les requêtes fréquentes). Expression : `CREATE INDEX ON users (lower(email))` pour les recherches insensibles à la casse. `INCLUDE (colonnes)` ajoute des colonnes non indexées à la feuille pour obtenir un index-only scan sans alourdir la clé de tri.

### 24. Comment fonctionnent les index GIN, GiST, BRIN et quand les utiliser ?
`🟠 Intermédiaire` · Sujet : **Index**

**Réponse :** GIN : index inversé pour les valeurs multiples (JSONB `@>`, tableaux, full-text `tsvector`, trigrammes `pg_trgm` pour `LIKE '%x%'`). GiST : structures géométriques et plages (PostGIS, `tsrange`, exclusion). BRIN : très compact pour les tables énormes physiquement ordonnées (timestamps append-only), résumé par blocs. B-tree reste le défaut pour égalités et plages.

### 25. Comment diagnostiquer les index manquants, inutiles ou dupliqués ?
`🟠 Intermédiaire` · Sujet : **Index**

**Réponse :** Manquants : `pg_stat_statements` + `EXPLAIN` sur les requêtes lentes montrant des seq scans avec filtres sélectifs ; `pg_stat_user_tables.seq_scan` élevé sur de grandes tables. Inutiles : `pg_stat_user_indexes.idx_scan = 0` depuis longtemps (coût en écriture et en espace). Dupliqués/redondants : un index (a) est couvert par (a, b). Outils : `pg_index`, `hypopg` pour tester un index hypothétique.

### 26. Comment créer ou reconstruire un index sans bloquer la production ?
`🟠 Intermédiaire` · Sujet : **Index**

**Réponse :** `CREATE INDEX CONCURRENTLY` (ne verrouille pas les écritures, plus lent, hors transaction, peut laisser un index invalide en cas d'échec à supprimer), `REINDEX CONCURRENTLY` (PostgreSQL 12+) pour le bloat, et `DROP INDEX CONCURRENTLY`. Planifier hors pic, surveiller `pg_stat_progress_create_index`, et vérifier `indisvalid`.

### 27. Qu'est-ce qu'une écriture perdue (lost update) et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **Transactions**

**Réponse :** Deux transactions lisent la même ligne, calculent et écrivent : la seconde écrase la première. Éviter : mise à jour relative atomique (`UPDATE stock SET qte = qte - 1 WHERE id = ? AND qte >= 1`), verrouillage optimiste (colonne version), `SELECT ... FOR UPDATE` avant modification, ou niveau `REPEATABLE READ`/`SERIALIZABLE` en PostgreSQL qui détecte le conflit (erreur à réessayer).

### 28. Que fait `SELECT ... FOR UPDATE`, `FOR SHARE`, `SKIP LOCKED` et `NOWAIT` ?
`🟠 Intermédiaire` · Sujet : **Transactions**

**Réponse :** `FOR UPDATE` verrouille les lignes lues jusqu'à la fin de la transaction (les autres écrivains attendent). `FOR SHARE` autorise d'autres lecteurs partagés mais bloque les écritures. `SKIP LOCKED` ignore les lignes déjà verrouillées : pattern de file de travail en SQL (`SELECT ... WHERE statut='A_FAIRE' ORDER BY id LIMIT 10 FOR UPDATE SKIP LOCKED`). `NOWAIT` échoue immédiatement au lieu d'attendre.

### 29. Comment fonctionne `SERIALIZABLE` en PostgreSQL (SSI) et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Transactions**

**Réponse :** Serializable Snapshot Isolation détecte les dépendances dangereuses entre transactions concurrentes et en annule une (`serialization_failure`, code 40001) plutôt que de verrouiller pessimistement : l'application doit réessayer. Garantit l'équivalence à une exécution en série sans verrous explicites, idéal pour les invariants complexes (contraintes multi-lignes), au prix de retries et d'un léger surcoût.

### 30. Quelles sont les anomalies de concurrence (dirty read, non-repeatable read, phantom, write skew) ?
`🟠 Intermédiaire` · Sujet : **Transactions**

**Réponse :** Dirty read : lire une écriture non validée (impossible en PostgreSQL). Non-repeatable : relire une ligne modifiée entre-temps (`READ COMMITTED`). Phantom : de nouvelles lignes apparaissent dans une requête répétée. Write skew : deux transactions lisent un état commun et écrivent des lignes différentes violant un invariant global (deux médecins de garde qui se désinscrivent) ; seul `SERIALIZABLE` le prévient.

### 31. Comment fonctionnent les verrous en PostgreSQL et comment diagnostiquer un blocage ?
`🟠 Intermédiaire` · Sujet : **Transactions**

**Réponse :** Verrous de ligne (MVCC, écrivain vs écrivain) et de table (DDL, `ACCESS EXCLUSIVE` bloque tout, y compris les `SELECT`). Diagnostiquer avec `pg_locks` joint à `pg_stat_activity` (`wait_event_type = 'Lock'`, `pg_blocking_pids(pid)`), `log_lock_waits`, et `deadlock_timeout`. Causes fréquentes : transactions longues (`idle in transaction`), migrations DDL en journée, `FOR UPDATE` dans un ordre différent (deadlock).

### 32. Pourquoi les migrations DDL peuvent-elles bloquer la production et comment les rendre sûres ?
`🟠 Intermédiaire` · Sujet : **Transactions**

**Réponse :** `ALTER TABLE` prend un verrou `ACCESS EXCLUSIVE` : s'il attend derrière une longue transaction, toutes les requêtes suivantes attendent derrière lui (file de verrous). Bonnes pratiques : `lock_timeout` court avec retry, opérations non bloquantes (`ADD COLUMN` sans default volatile, `ADD CONSTRAINT ... NOT VALID` puis `VALIDATE`, index `CONCURRENTLY`), éviter la réécriture de table (changement de type), et outils comme `pg-osc`/`gh-ost` (MySQL) pour les grosses tables.

### 33. Comment fonctionne MVCC en PostgreSQL et qu'est-ce que le bloat et le VACUUM ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Chaque `UPDATE`/`DELETE` crée une nouvelle version de ligne et laisse l'ancienne (tuple mort) visible pour les transactions plus anciennes. `VACUUM` (autovacuum) récupère l'espace des tuples morts, met à jour la visibility map (index-only scans) et prévient le wraparound des identifiants de transaction. Un autovacuum insuffisant sur des tables très modifiées provoque du bloat (tables et index gonflés) et des ralentissements : régler `autovacuum_vacuum_scale_factor` par table.

### 34. Quels paramètres PostgreSQL ont le plus d'impact sur les performances ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** `shared_buffers` (25 % de la RAM), `effective_cache_size` (estimation du cache OS, ~75 %), `work_mem` (tri/hash par opération, prudence : multiplié par les connexions), `maintenance_work_mem`, `max_connections` (préférer un pool, PgBouncer), `random_page_cost` (1.1 sur SSD), `checkpoint_completion_target`, `wal_compression`, et `max_parallel_workers_per_gather`. Outils : PGTune comme point de départ, puis mesure.

### 35. Pourquoi et comment utiliser PgBouncer ou un pooler de connexions côté serveur ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Chaque connexion PostgreSQL est un processus (mémoire, contention) ; des centaines de connexions dégradent les performances. PgBouncer (ou pgcat, RDS Proxy) mutualise en mode `transaction` (une connexion serveur par transaction), permettant des milliers de clients. Limites en mode transaction : pas de `prepared statements` nommés persistants (support amélioré en 1.21+), pas de `SET` de session, ni `LISTEN`. Combiner avec HikariCP côté application.

### 36. Comment optimiser une requête d'agrégation sur une grande table ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Index couvrant sur (filtre, colonnes agrégées), partitionnement par période pour élaguer, agrégats pré-calculés (vue matérialisée rafraîchie, table de rollup alimentée par trigger/job), parallélisme (`max_parallel_workers_per_gather`), `work_mem` suffisant pour éviter les tris sur disque, requêtes bornées dans le temps, et pour l'analytique lourde un entrepôt colonnaire (ClickHouse, BigQuery) alimenté par CDC.

### 37. Comment fonctionnent les statistiques de l'optimiseur et quand `ANALYZE` ou créer des statistiques étendues ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Le planificateur estime les cardinalités à partir des statistiques par colonne (`pg_stats` : histogrammes, valeurs fréquentes, distinct) collectées par `ANALYZE` (autovacuum). Après un gros import ou sur des colonnes très asymétriques, lancer `ANALYZE` et augmenter `default_statistics_target`/`ALTER COLUMN SET STATISTICS`. Pour des colonnes corrélées (code postal ↔ ville), `CREATE STATISTICS (dependencies, ndistinct)` corrige les estimations fausses et les mauvais plans.

### 38. Qu'est-ce que le partitionnement déclaratif PostgreSQL et ses pièges ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** `PARTITION BY RANGE (date)` / `LIST` / `HASH` avec des partitions créées à l'avance (job ou `pg_partman`), élagage des partitions à la planification/exécution, `DROP`/`DETACH` instantané des anciennes données, index et contraintes par partition. Pièges : la clé de partition doit faire partie des clés uniques, trop de partitions (milliers) ralentissent la planification, `ATTACH` nécessite une contrainte `CHECK` pour éviter le scan, et les jointures partitionnées nécessitent `enable_partitionwise_join`.

### 39. Comment gérer la pagination profonde et le comptage total efficacement ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Keyset : `WHERE (created_at, id) < (?, ?) ORDER BY created_at DESC, id DESC LIMIT 20` avec index composite, coût constant. `OFFSET 100000` lit et jette 100 000 lignes. Comptage : `COUNT(*)` exact est coûteux sur de grandes tables → estimation (`reltuples`, `EXPLAIN`), comptage mis en cache, ou affichage « plus de 1 000 » ; `COUNT(*) OVER()` dans la requête paginée combine les deux mais coûte autant.

### 40. Comment fonctionne le full-text search en PostgreSQL ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** `to_tsvector('french', texte)` normalise (stemming, stop words), `to_tsquery`/`plainto_tsquery`/`websearch_to_tsquery` construisent la requête, `@@` teste la correspondance, `ts_rank` classe, `ts_headline` surligne. Index GIN sur une colonne `tsvector` générée (`GENERATED ALWAYS AS (to_tsvector(...)) STORED`). Pour les fautes de frappe, `pg_trgm` (`similarity`, `%`). Suffisant pour beaucoup d'applications avant Elasticsearch.

### 41. Comment détecter et corriger les requêtes N+1 et les requêtes trop larges depuis SQL ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** `pg_stat_statements` : une requête `SELECT ... WHERE id = $1` avec un nombre d'appels énorme et un temps unitaire minime signale un N+1 (à corriger côté ORM par un `IN`/jointure). Requêtes larges : `SELECT *` sur des tables avec colonnes volumineuses (TOAST, JSONB, texte), à remplacer par une projection. `auto_explain` avec `log_min_duration` journalise les plans des requêtes lentes en production.

### 42. Comment mesurer et améliorer la latence d'écriture (commit, WAL, fsync) ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Chaque commit attend l'écriture du WAL sur disque (`fsync`) : latence dominée par le stockage. Leviers : `synchronous_commit = off` pour les données tolérant une perte de quelques ms en cas de crash (logs, métriques), regroupement des écritures en transactions par lots, `wal_compression`, disques rapides pour le WAL, et réplication synchrone uniquement si le RPO nul est exigé (coût de latence).

### 43. Comment fonctionnent la réplication logique et les publications/souscriptions ?
`🟠 Intermédiaire` · Sujet : **PostgreSQL**

**Réponse :** `CREATE PUBLICATION pub FOR TABLE ...` sur la source et `CREATE SUBSCRIPTION sub CONNECTION ... PUBLICATION pub` sur la cible répliquent les changements de lignes (pas les DDL) entre versions ou schémas différents : migrations majeures sans interruption, consolidation, alimentation d'un reporting. Debezium utilise la même mécanique (slot de réplication, `wal_level = logical`). Surveiller les slots inactifs qui retiennent le WAL.

### 44. Qu'est-ce que la Row-Level Security et comment l'utiliser pour le multi-tenant ?
`🟠 Intermédiaire` · Sujet : **PostgreSQL**

**Réponse :** `ALTER TABLE t ENABLE ROW LEVEL SECURITY; CREATE POLICY tenant_isolation ON t USING (tenant_id = current_setting('app.tenant_id')::uuid)` : chaque requête est automatiquement filtrée selon une variable de session posée par l'application (`SET LOCAL app.tenant_id`). Cela empêche les fuites inter-tenants même en cas d'oubli dans le code ; attention aux rôles `BYPASSRLS`, aux performances (index sur `tenant_id`) et aux pools de connexions (`SET LOCAL` par transaction).

### 45. Quelles extensions PostgreSQL faut-il connaître ?
`🟠 Intermédiaire` · Sujet : **PostgreSQL**

**Réponse :** `pg_stat_statements` (indispensable), `pg_trgm` (recherche approximative), `uuid-ossp`/`pgcrypto` (UUID, hachage, chiffrement), `postgis` (géo), `pgvector` (embeddings, recherche vectorielle), `pg_partman` (partitions), `timescaledb` (séries temporelles), `citext` (texte insensible à la casse), `hstore`/`ltree`, `pg_cron` (planification), `postgres_fdw` (tables distantes), `hypopg` (index hypothétiques).

### 46. Comment gérer les gros objets binaires et les colonnes volumineuses (TOAST) ?
`🟠 Intermédiaire` · Sujet : **PostgreSQL**

**Réponse :** Les valeurs de plus de ~2 Ko sont compressées et stockées hors ligne (TOAST) transparents mais coûteux à lire/modifier ; `SELECT *` sur des tables avec JSONB/texte volumineux ralentit tout. Bonnes pratiques : projections, séparer les colonnes volumineuses dans une table annexe, stocker les fichiers dans un object storage (S3) avec la référence en base, et `EXTERNAL`/`lz4` pour le stockage TOAST si pertinent.

### 47. Comment sécuriser une base PostgreSQL (rôles, droits, chiffrement, audit) ?
`🟠 Intermédiaire` · Sujet : **PostgreSQL**

**Réponse :** Rôles distincts par application avec droits minimaux (`GRANT SELECT, INSERT ... ON ...`, `DEFAULT PRIVILEGES`), pas d'utilisation du superuser par l'application, `pg_hba.conf` restrictif (scram-sha-256, réseau limité), TLS obligatoire, chiffrement au repos (disque/cloud) et colonne (pgcrypto ou côté application pour les données sensibles), `pgaudit` pour tracer, rotation des mots de passe via un gestionnaire de secrets, et sauvegardes chiffrées testées.

### 48. Comment sauvegarder et restaurer PostgreSQL (logique vs physique, PITR) ?
`🟠 Intermédiaire` · Sujet : **PostgreSQL**

**Réponse :** `pg_dump`/`pg_restore` : sauvegarde logique par base, portable entre versions, restauration sélective, lente sur de gros volumes. Physique : `pg_basebackup` + archivage continu du WAL permettant le Point-In-Time Recovery (restaurer l'état à une seconde donnée avant une erreur humaine). Outils : pgBackRest, Barman, ou snapshots managés (RDS/Cloud SQL avec PITR). Tester régulièrement les restaurations et mesurer le RTO.

### 49. Quelles bonnes pratiques SQL depuis une application Java/Spring ?
`🟠 Intermédiaire` · Sujet : **SQL & Java**

**Réponse :** Requêtes préparées (jamais de concaténation), transactions courtes, `readOnly` pour les lectures, pagination systématique, projections ciblées, batch pour les écritures, timeouts (`statement_timeout` par rôle ou `spring.jpa.properties.jakarta.persistence.query.timeout`), migrations versionnées (Flyway), `EXPLAIN` sur les requêtes JPA générées (logs SQL en dev), index créés pour chaque pattern de requête réel, et surveillance `pg_stat_statements` en production.

### 50. Comment tester du SQL et des migrations de façon fiable ?
`🟠 Intermédiaire` · Sujet : **SQL & Java**

**Réponse :** Tests d'intégration sur la vraie base (Testcontainers PostgreSQL, pas H2 dont la sémantique diffère), jeux de données minimaux, vérification des plans sur des volumes réalistes en préproduction, tests de migration sur une copie anonymisée de production (durée, verrous), et contrôle en CI que chaque migration est rétrocompatible avec la version précédente de l'application (déploiement en deux étapes).

### 51. Comment choisir entre PostgreSQL, MySQL et les bases managées distribuées ?
`🟠 Intermédiaire` · Sujet : **SQL & Java**

**Réponse :** PostgreSQL : richesse fonctionnelle (JSONB, types, extensions, SSI, partitionnement, CTE), standard de facto des nouveaux projets. MySQL/MariaDB : écosystème web historique, réplication simple, moins de fonctionnalités avancées. Distribuées (Aurora, AlloyDB, CockroachDB, Yugabyte, Spanner) : scalabilité horizontale et haute disponibilité multi-région au prix de latence, coût et compatibilité partielle. Commencer par PostgreSQL managé avec réplicas et n'envisager le distribué que sur besoin mesuré.
