# 📐 System Design (exercices d'entretien)

> Raccourcisseur d'URL, file de notifications, système de réservation, et méthode générale

**50 questions**

---

### 1. Comment aborder un exercice de system design en entretien ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** En quatre temps : clarifier le besoin (cas d'usage, utilisateurs, ce qui est hors périmètre), estimer les ordres de grandeur (trafic, volume, latence), concevoir à haut niveau (composants, flux de données, API), puis approfondir les points sensibles (stockage, scalabilité, pannes, compromis). L'évaluateur juge la démarche, les questions posées et la capacité à justifier des choix, pas une réponse unique.

### 2. Quelles questions poser avant de concevoir ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** Fonctionnelles : quelles opérations principales ? qui sont les utilisateurs ? lectures ou écritures dominantes ? Non fonctionnelles : nombre d'utilisateurs et de requêtes par seconde, latence attendue, disponibilité cible, cohérence forte ou éventuelle acceptable, rétention des données, contraintes (budget, cloud, équipe). Ces réponses orientent tous les choix ensuite.

### 3. Comment faire une estimation « back-of-the-envelope » ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** Partir des utilisateurs actifs par jour, en déduire les requêtes par seconde (1 M/jour ≈ 12 rps en moyenne, prévoir un pic ×5-10), estimer la taille d'un enregistrement pour le stockage annuel, et la bande passante. Connaître quelques repères : 1 jour ≈ 86 400 s, une lecture SSD ≈ 100 µs, un aller-retour réseau intra-datacenter ≈ 0,5 ms, inter-continents ≈ 100 ms.

### 4. Quels composants reviennent dans presque toutes les architectures ?
`🟢 Débutant` · Sujet : **Méthode**

**Réponse :** Un load balancer, des serveurs d'application stateless, une base de données (avec réplicas), un cache (Redis), un stockage d'objets (S3), une file de messages (Kafka/SQS) pour découpler, un CDN pour le contenu statique, et l'observabilité. Connaître le rôle et les limites de chacun permet d'assembler rapidement une première version.

### 5. Comment présenter les compromis (trade-offs) ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Chaque choix se justifie par rapport aux exigences : SQL vs NoSQL (cohérence et requêtes riches vs échelle horizontale), synchrone vs asynchrone (simplicité vs résilience), cache vs fraîcheur, monolithe vs microservices (vitesse initiale vs autonomie des équipes). Énoncer explicitement ce qu'on gagne, ce qu'on perd et dans quelles conditions on changerait d'avis.

### 6. Qu'est-ce que le théorème CAP et comment l'utiliser en design ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** En cas de partition réseau, un système distribué doit choisir entre cohérence (refuser ou attendre) et disponibilité (répondre avec des données potentiellement périmées). En pratique, décider par fonctionnalité : un solde bancaire ou une réservation exige la cohérence ; un compteur de vues ou un fil d'actualité tolère la cohérence éventuelle. PACELC ajoute le compromis latence/cohérence hors partition.

### 7. Comment concevoir pour la haute disponibilité ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Éliminer les points uniques de défaillance : plusieurs instances derrière un load balancer, réplication de la base avec failover automatique, déploiement multi-zones, files persistantes, retries avec backoff et idempotence, circuit breakers, dégradation gracieuse. Calculer la disponibilité composée : des dépendances en série multiplient les indisponibilités.

### 8. Comment gérer la montée en charge : scaling vertical vs horizontal ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Vertical : machine plus grosse, simple mais plafonné et point unique. Horizontal : ajouter des instances, exige des services stateless (session externalisée), un partitionnement des données (sharding) et un load balancing. La base de données est en général le premier goulot : réplicas en lecture, cache, puis sharding par clé bien choisie.

### 9. Qu'est-ce que le sharding et comment choisir la clé ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Répartir les données sur plusieurs bases selon une clé (utilisateur, région, hash de l'id). Une bonne clé répartit uniformément la charge et regroupe les données accédées ensemble ; une mauvaise crée des hot spots (célébrités, dates) ou des requêtes cross-shard coûteuses. Le hachage cohérent facilite l'ajout de shards ; le resharding reste une opération lourde à anticiper.

### 10. Quand utiliser un cache et quelles stratégies ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Quand les lectures dominent et tolèrent une légère obsolescence. Cache-aside (l'application lit le cache puis la base et remplit), read-through/write-through (le cache gère l'accès), write-behind (écriture asynchrone). Prévoir le TTL, l'invalidation, la protection contre le cache stampede (verrou, early refresh) et le comportement en cas de panne du cache (dégradé mais fonctionnel).

### 11. Comment concevoir une API pour un système à grande échelle ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** REST ou gRPC selon les consommateurs, pagination par curseur (pas par offset sur les gros volumes), idempotence des écritures (clé d'idempotence), versionnement, rate limiting par client, réponses partielles pour limiter la bande passante, et documentation OpenAPI. Les opérations longues renvoient 202 avec un identifiant de suivi plutôt que de bloquer.

### 12. Comment garantir l'idempotence des opérations ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Le client envoie une clé unique par opération (`Idempotency-Key`) ; le serveur stocke le résultat associé (avec TTL) et renvoie la même réponse en cas de rejeu. Côté messages, les consommateurs dédupliquent par identifiant d'événement ou rendent le traitement naturellement idempotent (upsert). Indispensable dès qu'il y a des retries.

### 13. Quelles sont les exigences d'un raccourcisseur d'URL ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Fonctionnelles : créer une URL courte pour une URL longue (éventuellement alias personnalisé et expiration), rediriger, statistiques de clics. Non fonctionnelles : ratio lectures/écritures très élevé (100:1 ou plus), latence de redirection minimale, très haute disponibilité, URLs non prédictibles (ou l'inverse selon le besoin), échelle de centaines de millions d'URLs.

### 14. Comment estimer les volumes d'un raccourcisseur ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Exemple : 100 M de nouvelles URLs par mois ≈ 40 écritures/s, 10 G de redirections par mois ≈ 4 000 lectures/s. Chaque enregistrement ≈ 500 octets → 50 Go par mois, 6 To sur 10 ans. Un code de 7 caractères en base 62 offre 62^7 ≈ 3,5 × 10^12 combinaisons, largement suffisant.

### 15. Comment générer les codes courts ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Options : (1) hacher l'URL (MD5/SHA) et prendre 7 caractères, avec gestion des collisions par vérification et re-hachage ; (2) un compteur unique (base, Snowflake, ou plages pré-allouées par serveur) encodé en base 62, sans collision mais prédictible (à brouiller si nécessaire) ; (3) un service de génération de clés pré-calculées (KGS) distribuant des codes uniques. Le compteur avec plages est le plus simple à grande échelle.

### 16. Quel stockage pour un raccourcisseur d'URL ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Un modèle clé-valeur simple (code → URL, dates, propriétaire) sans relations : une base NoSQL (DynamoDB, Cassandra) ou un PostgreSQL shardé fonctionne. Redis en cache devant pour les 20 % d'URLs générant 80 % des lectures. Indexer le code court (clé primaire) et éventuellement l'utilisateur pour lister ses liens.

### 17. 301 ou 302 pour la redirection ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** 301 (permanent) : le navigateur met en cache et ne repasse plus par le service, ce qui réduit la charge mais empêche de compter les clics et de modifier la cible. 302/307 (temporaire) : chaque clic revient au service, permettant analytics et mise à jour au prix de plus de trafic. Le choix dépend de l'importance des statistiques.

### 18. Comment gérer les statistiques de clics sans ralentir la redirection ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Ne jamais écrire en base sur le chemin de redirection : publier un événement (Kafka) ou incrémenter un compteur Redis, puis agréger en asynchrone (stream processing, batch) vers un entrepôt analytique (ClickHouse, BigQuery). Les statistiques sont donc légèrement différées, ce qui est acceptable.

### 19. Comment gérer expiration, suppression et abus ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Expiration : stocker une date et purger par job ou TTL natif (DynamoDB, Redis), vérifier à la lecture. Abus : rate limiting par IP/utilisateur à la création, vérification des URLs contre des listes de sites malveillants (Safe Browsing), page interstitielle pour les liens suspects, possibilité de désactiver un lien.

### 20. Comment rendre le raccourcisseur hautement disponible et global ?
`🟠 Intermédiaire` · Sujet : **Raccourcisseur d'URL**

**Réponse :** Services stateless derrière un load balancer dans plusieurs régions, base répliquée (la lecture depuis n'importe quelle région, écriture centralisée ou multi-master si la base le permet), cache régional, DNS géographique (Route 53 latency-based) et éventuellement redirection au niveau CDN/edge pour les liens les plus populaires.

### 21. Quelles sont les exigences d'un système de notifications ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Envoyer des notifications multi-canaux (push mobile, e-mail, SMS, in-app) déclenchées par des événements métier ou des campagnes, avec préférences utilisateur, gabarits, limitation de fréquence, priorités, garantie de livraison au moins une fois sans doublons visibles, et suivi de l'état (envoyé, délivré, ouvert). Échelle : millions d'utilisateurs, pics lors des campagnes.

### 22. Quelle architecture globale pour un service de notifications ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Des producteurs (services métier, planificateur de campagnes) publient des demandes dans une file (Kafka/SQS). Un service de notification consomme, applique préférences et règles (opt-out, fréquence, fenêtres horaires), rend les gabarits, puis route vers des workers par canal (APNs/FCM, fournisseur e-mail, SMS). Les statuts remontent par webhooks vers un magasin de suivi.

### 23. Pourquoi une file de messages est-elle centrale ici ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Elle découple les producteurs des fournisseurs externes lents ou en panne, absorbe les pics (campagne de 10 M d'e-mails), permet de scaler les workers indépendamment par canal, offre les retries et la persistance, et sépare les priorités (file « transactionnel » traitée avant « marketing »). Sans file, une panne de fournisseur SMS bloquerait les services métier.

### 24. Comment gérer les priorités et éviter qu'une campagne bloque les notifications critiques ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Files séparées par priorité (critique : code OTP, alerte sécurité ; normale ; marketing) avec des pools de workers dédiés et des quotas, plutôt qu'une file unique triée. Les campagnes massives sont émises progressivement (throttling) pour respecter les limites des fournisseurs et ne pas saturer.

### 25. Comment garantir la livraison sans envoyer de doublons ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** La file assure « au moins une fois » ; les workers doivent être idempotents : chaque notification porte un identifiant unique, stocké (Redis/base) avant l'appel au fournisseur ; en cas de rejeu, on vérifie l'état. Les retries utilisent un backoff exponentiel et une dead-letter queue après N échecs, avec alerte.

### 26. Comment gérer les préférences utilisateur et la limitation de fréquence ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Un service de préférences (canaux acceptés, catégories, ne pas déranger, langue) consulté avant envoi, avec cache. Rate limiting par utilisateur et catégorie (max N marketing par jour) via compteurs Redis à fenêtre glissante. Regroupement (digest) des notifications peu urgentes pour éviter la saturation.

### 27. Comment gérer les gabarits et la personnalisation ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Un référentiel de templates versionnés par canal et langue (Handlebars/Mustache, MJML pour l'e-mail), rendus par le service avec les données de l'événement ; validation à la création, prévisualisation, et A/B testing des variantes. Les données personnelles ne doivent pas transiter dans les logs.

### 28. Comment suivre les statuts et fournir des analytics ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Chaque étape émet un événement (créée, envoyée, délivrée, échouée, ouverte, cliquée) stocké dans un magasin append-only (Kafka → ClickHouse/BigQuery) ; les webhooks des fournisseurs (bounces, ouvertures) sont ingérés de la même manière. Tableaux de bord par canal et par campagne, alertes sur les taux d'échec.

### 29. Comment intégrer les fournisseurs externes de façon résiliente ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Un adaptateur par fournisseur avec timeouts, circuit breaker, respect des quotas, et possibilité de basculer sur un fournisseur secondaire (SMS) en cas de panne. Les clés d'API sont gérées par un gestionnaire de secrets. Tester avec des environnements sandbox et surveiller la latence de chaque fournisseur.

### 30. Comment gérer les notifications planifiées et les fuseaux horaires ?
`🟠 Intermédiaire` · Sujet : **File de notifications**

**Réponse :** Stocker l'heure d'envoi souhaitée en UTC avec le fuseau de l'utilisateur ; un planificateur (job scannant les échéances par fenêtre, ou files à délai type SQS delay/Redis sorted set) publie les demandes au moment voulu. Les campagnes « 9h heure locale » sont découpées par fuseau.

### 31. Quelles sont les exigences d'un système de réservation (hôtel, cinéma, billetterie) ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Rechercher les disponibilités, réserver une ressource pour un créneau (chambre/siège/date) sans double réservation, payer, annuler, avec des pics extrêmes (ouverture de ventes), une cohérence forte sur l'inventaire, et une expérience acceptable en cas de forte concurrence (file d'attente virtuelle). La double réservation est l'erreur inacceptable.

### 32. Comment modéliser les données d'une réservation ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Entités : ressource (hôtel/salle), unité (chambre type, siège), inventaire par unité et par date/séance (quantité disponible), réservation (utilisateur, unités, dates, statut : en attente, confirmée, annulée, expirée), paiement. La table d'inventaire par date est la clé des performances et de la cohérence.

### 33. Comment éviter la double réservation ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Avec une base relationnelle : transaction et verrouillage. Pessimiste : `SELECT ... FOR UPDATE` sur la ligne d'inventaire puis décrément. Optimiste : colonne `version`, `UPDATE inventory SET available = available - 1, version = version + 1 WHERE id = ? AND version = ? AND available > 0`, échec si aucune ligne modifiée. Ou une contrainte unique (siège + séance) qui rejette physiquement le doublon. L'optimiste convient aux hôtels ; la contrainte unique aux sièges nominatifs.

### 34. Qu'est-ce que la réservation temporaire (hold) et comment l'implémenter ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Bloquer l'inventaire pendant que l'utilisateur paie (10 minutes) : statut « en attente » avec date d'expiration, décrément immédiat de l'inventaire, puis un job (ou un TTL Redis avec événement) libère les réservations expirées. Le paiement confirme la réservation ; l'échec ou le timeout la libère. Cela évite que deux utilisateurs paient le même siège.

### 35. Comment intégrer le paiement de façon fiable ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Le paiement est une opération externe non transactionnelle : réserver d'abord (hold), initier le paiement avec une clé d'idempotence, confirmer sur webhook du prestataire (pas seulement sur la réponse synchrone), et compenser (annuler la réservation, rembourser) en cas d'incohérence. Une saga orchestrée modélise ces étapes ; journaliser chaque transition.

### 36. Comment gérer les pics d'ouverture de ventes (billetterie) ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** File d'attente virtuelle en amont (l'utilisateur reçoit un jeton et un tour), limitation du nombre d'utilisateurs simultanés dans le tunnel d'achat, inventaire des sièges chauds en mémoire (Redis avec scripts Lua atomiques) synchronisé vers la base, pré-scaling des services, et protection contre les bots (CAPTCHA, limites par compte).

### 37. Comment concevoir la recherche de disponibilités ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** La recherche est la charge dominante (lectures) : index sur (unité, date) ou table d'inventaire par jour, cache des résultats fréquents avec courte durée de vie, réplicas en lecture, et éventuellement un moteur dédié (Elasticsearch) pour la recherche par critères (ville, prix, équipements) qui renvoie des candidats vérifiés ensuite contre l'inventaire réel.

### 38. Cohérence forte ou éventuelle pour un système de réservation ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** L'inventaire et la confirmation exigent la cohérence forte (une seule source de vérité transactionnelle, souvent PostgreSQL shardé par ressource/hôtel). La recherche, les recommandations, l'historique et les notifications tolèrent la cohérence éventuelle via des événements. Le message d'erreur « plus disponible » à la confirmation est acceptable ; la double vente ne l'est pas.

### 39. Comment sharder un système de réservation ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Par ressource (hôtel, salle, événement) : toutes les données d'inventaire d'une ressource résident sur le même shard, rendant les transactions locales. Les requêtes transverses (réservations d'un utilisateur) passent par un index secondaire ou une vue matérialisée alimentée par événements. Les événements très populaires (hot shard) peuvent nécessiter un traitement dédié.

### 40. Comment gérer annulations, modifications et surbooking ?
`🟠 Intermédiaire` · Sujet : **Système de réservation**

**Réponse :** Annulation : transaction restituant l'inventaire, application des règles tarifaires, remboursement asynchrone. Modification : nouvelle réservation en hold puis libération de l'ancienne (jamais l'inverse). Surbooking (compagnies aériennes, hôtels) : inventaire vendable > inventaire physique selon un taux configuré, avec processus de gestion des dépassements.

### 41. Comment concevoir un fil d'actualité (news feed) ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Deux approches : fan-out on write (à la publication, pousser le post dans le cache de feed de chaque abonné : lecture rapide, coûteux pour les comptes à millions d'abonnés) ou fan-out on read (assembler à la lecture : simple, lent). Hybride : push pour les utilisateurs normaux, pull pour les célébrités. Classement par pertinence via un service de ranking, pagination par curseur.

### 42. Comment concevoir un service de chat temps réel ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Connexions persistantes (WebSocket) vers des serveurs de passerelle, un service de présence (Redis avec heartbeat), stockage des messages dans une base orientée écriture (Cassandra, clé = conversation + timestamp), file pour la livraison aux destinataires déconnectés (notifications push), synchronisation multi-appareils par identifiants de séquence, chiffrement de bout en bout selon les exigences.

### 43. Comment concevoir un rate limiter distribué ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Algorithmes : token bucket (bursts autorisés), sliding window log/counter (précision). Implémentation : compteurs Redis avec scripts Lua atomiques, clé par client et fenêtre, TTL automatique ; placement dans la gateway ; réponse 429 avec headers `Retry-After`/`X-RateLimit-*`. Tolérer une légère imprécision en multi-région plutôt que synchroniser globalement.

### 44. Comment concevoir un système de stockage de fichiers type Dropbox ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Découpage des fichiers en blocs (chunks) dédupliqués par hash, stockage des blocs dans un object storage, métadonnées (arborescence, versions) dans une base relationnelle, service de synchronisation notifiant les clients des changements (long polling/WebSocket), upload résumable et direct vers le stockage via URLs présignées, gestion des conflits par versions.

### 45. Comment concevoir un moteur de recherche d'autocomplétion ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Un trie (arbre de préfixes) en mémoire avec les top-k suggestions pré-calculées par nœud, alimenté périodiquement par l'agrégation des requêtes (pipeline batch/stream), shardé par préfixe, servi avec un cache et une latence < 100 ms. Filtrage des termes inappropriés, personnalisation optionnelle par utilisateur.

### 46. Comment concevoir un service de géolocalisation type « restaurants à proximité » ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Indexer les positions avec un geohash ou un quadtree/S2 pour requêter efficacement une zone, base avec support géospatial (PostGIS, Redis GEO, Elasticsearch geo), séparer les données statiques (établissements) des positions mobiles (chauffeurs, mises à jour fréquentes en mémoire), et calculer la distance réelle sur les candidats retournés.

### 47. Comment concevoir un système de traitement de paiements ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Exigences : exactitude absolue, idempotence, audit. Ledger en double entrée append-only comme source de vérité, transitions d'état explicites, intégration des PSP avec retries idempotents et webhooks, réconciliation quotidienne avec les rapports des prestataires, conformité PCI DSS (tokenisation, jamais de numéro de carte en clair), et observabilité fine sur les échecs.

### 48. Comment concevoir un système de métriques et monitoring ?
`🟠 Intermédiaire` · Sujet : **Autres exercices**

**Réponse :** Collecte par pull (Prometheus) ou push (agents), ingestion via file, stockage en base de séries temporelles (Prometheus/Thanos, VictoriaMetrics, InfluxDB) avec downsampling et rétention par âge, requêtes d'agrégation, alerting avec déduplication et routage, tableaux de bord. Attention à la cardinalité des labels, principal facteur de coût.

### 49. Quelles erreurs éviter en entretien de system design ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Se lancer dans les détails sans clarifier le besoin, proposer des microservices et Kafka par réflexe, ignorer les ordres de grandeur, ne pas parler des pannes, rester silencieux (penser à voix haute), ne pas savoir justifier un choix, et oublier les aspects transverses (sécurité, observabilité, coût). Terminer par les limites de la solution et les évolutions possibles.

### 50. Comment estimer et discuter le coût d'une architecture ?
`🟠 Intermédiaire` · Sujet : **Méthode**

**Réponse :** Identifier les postes dominants : calcul (instances, serverless), stockage (Go stockés, IOPS), transfert sortant (souvent sous-estimé), services managés (bases, files) et observabilité (volume de logs). Comparer des variantes (réplicas vs cache, région unique vs multi-région) en ordre de grandeur mensuel et relier chaque dépense à une exigence ; un coût élevé sans exigence correspondante est un signal de sur-conception.
