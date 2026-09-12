# 📨 Apache Kafka

> Topics, partitions, consumer groups, Streams, exactly-once semantics

**8 questions**

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
