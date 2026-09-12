# 🧩 Microservices & Architecture Patterns

> Circuit Breaker, Saga, CQRS, Event Sourcing, gRPC, GraphQL, WebSockets

**13 questions**

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
