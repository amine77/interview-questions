# 🧹 Clean Code & Clean Architecture

> SRP, DRY, code smells, Loi de Déméter, Use Cases, DIP

**12 questions**

---

### 1. Qu'est-ce que le principe de responsabilité unique (SRP) ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Une classe ou fonction ne devrait avoir qu'une seule raison de changer, une seule responsabilité métier, améliorant lisibilité et testabilité.

### 2. Règle de dépendance dans Clean Architecture ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Les dépendances pointent uniquement vers l'intérieur (des couches externes vers le domaine métier), jamais l'inverse.

### 3. Pourquoi éviter les "magic numbers" ?
`🟢 Débutant` · Sujet : **Clean Code**

**Réponse :** Nuisent à la lisibilité/maintenabilité ; préférer une constante nommée documentant l'intention.

### 4. Qu'est-ce qu'une Entity ?
`🟢 Débutant` · Sujet : **Clean Architecture**

**Réponse :** Objet représentant les règles métier fondamentales, indépendant de tout framework, au cœur de l'architecture.

### 5. Qu'est-ce qu'un code smell ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Indicateur symptomatique d'un problème de conception, ex: Long Method à décomposer.

### 6. Qu'est-ce qu'un Use Case ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Classe orchestrant la logique applicative d'une action métier précise, coordonnant entités et ports.

### 7. Principe DRY ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Éviter la duplication de logique/connaissance, chaque élément ayant une représentation unique.

### 8. Port et Adapter (architecture hexagonale) ?
`🟢 Débutant` · Sujet : **Clean Architecture**

**Réponse :** Port = interface de contrat. Adapter = implémentation concrète reliant le domaine à une techno externe.

### 9. Importance du nommage explicite ?
`🟢 Débutant` · Sujet : **Clean Code**

**Réponse :** Rend le code auto-documenté, facilitant la compréhension.

### 10. Pourquoi les frameworks sont des détails ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Interchangeables, ne devraient pas dicter la structure du cœur métier.

### 11. Loi de Déméter ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Un objet ne devrait communiquer qu'avec ses voisins directs, évitant les chaînes d'appels profondes.

### 12. Inversion de dépendance (DIP) ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Modules de haut niveau et bas niveau dépendent tous deux d'abstractions (ports/interfaces).
