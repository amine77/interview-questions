# 🗄️ Databases

> SQL, MongoDB, Redis, Elasticsearch, distributed databases, migrations

**20 questions**

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
