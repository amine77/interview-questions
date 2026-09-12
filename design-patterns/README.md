# 🎨 Design Patterns

> Singleton, Factory, Strategy, Builder, Adapter, Decorator, Observer, Facade

**50 questions**

---

### 1. Expliquez le pattern Singleton et un cas d'usage.
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Garantit qu'une classe n'a qu'une seule instance et fournit un point d'accès global à celle-ci. Utile pour une configuration partagée ou une connexion à une ressource unique.

### 2. Pattern Factory ?
`🟢 Débutant` · Sujet : **Design Pattern**

**Réponse :** Délègue la création d'objets à une méthode/classe dédiée plutôt que `new` direct, découplant le client du type concret.

### 3. Pattern Strategy ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Famille d'algorithmes interchangeables encapsulés, permettant de changer le comportement à l'exécution.

### 4. Pattern Observer ?
`🟢 Débutant` · Sujet : **Design Pattern**

**Réponse :** Dépendance un-à-plusieurs : un sujet notifie automatiquement ses observateurs abonnés lors d'un changement d'état.

### 5. Pattern Decorator ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Ajoute dynamiquement des responsabilités à un objet en l'enveloppant, alternative à l'héritage.

### 6. Pattern Adapter ?
`🟢 Débutant` · Sujet : **Design Pattern**

**Réponse :** Fait fonctionner ensemble deux interfaces incompatibles via une classe adaptatrice.

### 7. Pattern Builder ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Sépare la construction d'un objet complexe de sa représentation, via une interface fluide.

### 8. Pattern Facade ?
`🟢 Débutant` · Sujet : **Design Pattern**

**Réponse :** Interface simplifiée unique masquant la complexité d'un sous-système.

### 9. Quelles sont les trois familles de patterns du GoF ?
`🟢 Débutant` · Sujet : **Design Pattern**

**Réponse :** Créationnels (comment créer les objets : Singleton, Factory Method, Abstract Factory, Builder, Prototype), structurels (comment composer classes et objets : Adapter, Decorator, Facade, Proxy, Composite, Bridge, Flyweight), comportementaux (comment les objets interagissent : Strategy, Observer, Command, State, Template Method, Chain of Responsibility, Iterator, Mediator, Memento, Visitor, Interpreter).

### 10. Différence entre Factory Method et Abstract Factory ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Factory Method : une méthode (souvent abstraite, redéfinie par les sous-classes) crée un objet d'un type donné. Abstract Factory : une interface créant des familles d'objets liés (boutons + fenêtres pour un thème) sans préciser leurs classes concrètes. Le second regroupe plusieurs factory methods cohérentes.

### 11. Pattern Prototype et son équivalent Java ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Créer un objet en clonant une instance existante plutôt qu'en instanciant, utile quand la construction est coûteuse ou la configuration complexe. En Java : `Cloneable`/`clone()` (fragile, copie superficielle), ou mieux un constructeur de copie ou des méthodes `with*` sur des records immuables.

### 12. Pattern Proxy et ses variantes ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Un objet qui contrôle l'accès à un autre en exposant la même interface : proxy virtuel (chargement paresseux, comme les entités Hibernate), proxy de protection (contrôle d'accès), proxy distant (stub RPC), proxy de cache/logging. Spring AOP repose sur des proxies dynamiques (JDK ou CGLIB) pour `@Transactional`, `@Cacheable`, `@Async`.

### 13. Pattern Composite ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Traiter uniformément des objets individuels et des compositions (arbre) via une interface commune : un `Component` avec `operation()`, implémenté par `Leaf` et `Composite` (qui délègue à ses enfants). Exemples : arbre de fichiers, composants UI, expressions de filtres (`Specification` and/or/not).

### 14. Pattern Bridge ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Séparer une abstraction de son implémentation pour qu'elles évoluent indépendamment : `Notification` (alerte, rappel) référence un `Channel` (email, SMS, push) plutôt que de multiplier les sous-classes (`AlertEmail`, `AlertSms`…). Il évite l'explosion combinatoire par composition.

### 15. Pattern Flyweight ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Partager les données intrinsèques communes entre de nombreux objets pour économiser la mémoire, en externalisant l'état extrinsèque. Exemples : `Integer.valueOf()` (cache -128..127), pool de chaînes, caractères d'un éditeur de texte, glyphes de police.

### 16. Pattern Command ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Encapsuler une requête en objet (`execute()`, éventuellement `undo()`), permettant de la paramétrer, la mettre en file, la journaliser ou l'annuler. Exemples : actions d'une UI, tâches d'un `ExecutorService` (`Runnable`), commandes CQRS, transactions compensables.

### 17. Pattern Template Method et sa relation avec Strategy ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Une classe abstraite définit le squelette d'un algorithme et délègue certaines étapes à des méthodes abstraites redéfinies par les sous-classes (héritage). Strategy fait varier tout l'algorithme par composition. Template Method est plus rigide ; on le trouve dans `AbstractList`, les `JdbcTemplate` et les tests (`setUp`).

### 18. Pattern State ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Un objet change de comportement selon son état interne, chaque état étant une classe implémentant les transitions. Il remplace les `switch` sur un enum d'état par du polymorphisme : machine à états d'une commande (Created → Paid → Shipped), workflow de document. Spring StateMachine l'industrialise.

### 19. Pattern Chain of Responsibility ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Une requête traverse une chaîne de handlers, chacun la traitant ou la passant au suivant. Exemples : filtres de servlet et `SecurityFilterChain`, intercepteurs HTTP Angular, middlewares Express, gestion d'exceptions par niveaux, validation en cascade.

### 20. Pattern Mediator ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Centraliser les interactions entre objets dans un médiateur pour qu'ils ne se référencent pas mutuellement, réduisant le couplage many-to-many. Exemples : un contrôleur d'écran coordonnant des widgets, un bus de commandes/événements applicatif (Spring `ApplicationEventPublisher`), un chat room.

### 21. Pattern Memento ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Capturer l'état interne d'un objet dans un memento opaque pour le restaurer plus tard sans violer l'encapsulation : undo/redo, snapshots, sauvegarde de session. Le snapshot d'Event Sourcing est une application à grande échelle.

### 22. Pattern Visitor ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Ajouter des opérations à une hiérarchie d'objets sans la modifier : chaque élément accepte un visiteur (`accept(visitor)`) qui a une méthode par type (`visit(Circle)`). Utile pour les AST, exports multiples. Avec les sealed interfaces et le pattern matching `switch` de Java 21, Visitor devient souvent inutile.

### 23. Pattern Iterator ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Parcourir une collection sans exposer sa structure interne. En Java, `Iterable`/`Iterator` alimentent la boucle for-each ; `Spliterator` les streams. Les générateurs et `Iterable` de JavaScript/TypeScript jouent le même rôle.

### 24. Pattern Null Object ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Remplacer `null` par un objet au comportement neutre (`NoOpLogger`, `EmptyList`, `Collections.emptyList()`) pour éliminer les vérifications `if (x != null)` et les NPE. `Optional` est une alternative quand l'absence doit être explicitement traitée.

### 25. Différence entre Adapter, Decorator, Proxy et Facade ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Tous enveloppent un objet. Adapter change l'interface (compatibilité). Decorator garde l'interface et ajoute du comportement (empilable). Proxy garde l'interface et contrôle l'accès (lazy, sécurité, distant). Facade simplifie l'accès à un sous-système en offrant une interface de plus haut niveau.

### 26. Pourquoi Singleton est-il souvent considéré comme un anti-pattern ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** État global caché, couplage fort, tests difficiles (impossible à remplacer par un mock), problèmes de concurrence et de cycle de vie. Dans Spring, les beans sont singletons par défaut mais injectés : on obtient l'unicité sans les inconvénients. Si nécessaire, l'enum singleton est l'implémentation Java la plus sûre.

### 27. Comment implémenter un Singleton thread-safe en Java ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Enum (`enum Config { INSTANCE; }`) : simple, sérialisable, réflexion-safe. Ou initialisation par holder (`private static class Holder { static final X INSTANCE = new X(); }`), paresseuse et sans synchronisation grâce au chargement de classe. Le double-checked locking exige `volatile`.

### 28. Pattern Dependency Injection et Inversion of Control ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** L'IoC confie le contrôle du cycle de vie et du câblage des objets à un conteneur. La DI en est une forme : les dépendances sont fournies (constructeur, setter) plutôt que créées par l'objet. Bénéfices : découplage, testabilité, configuration centralisée. Spring, Angular et NestJS en sont des implémentations.

### 29. Pattern Repository ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Une abstraction de collection d'objets du domaine (`findById`, `save`, requêtes métier) masquant la persistance. Il appartient au domaine (interface) et est implémenté dans l'infrastructure. Spring Data génère les implémentations ; le piège est d'y exposer des détails techniques (JPQL, entités) au domaine.

### 30. Pattern Unit of Work ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Suivre les objets modifiés pendant une opération métier et écrire toutes les modifications en une transaction unique à la fin. Le `EntityManager`/session Hibernate est un Unit of Work : le dirty checking flush automatiquement au commit, ce qui explique qu'un `save()` explicite est parfois inutile sur une entité managée.

### 31. Pattern Specification ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Encapsuler une règle métier en objet composable (`and`, `or`, `not`) réutilisable pour la validation, la sélection en mémoire et la construction de requêtes. Spring Data JPA `Specification<T>` traduit ces objets en `Predicate` Criteria pour les recherches dynamiques.

### 32. Pattern Object Mother et Test Data Builder ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Deux façons de construire des données de test lisibles : l'Object Mother expose des méthodes nommées (`aValidCustomer()`), le Builder permet de ne surcharger que ce qui compte (`anOrder().withStatus(PAID).build()`). Ils évitent la duplication des fixtures et rendent les tests expressifs.

### 33. Pattern Registry / Service Locator et pourquoi le déconseiller ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Un objet central où l'on enregistre et récupère des services par clé (`ServiceLocator.get(Foo.class)`). Il cache les dépendances (invisibles dans la signature), complique les tests et le refactoring. La DI par constructeur rend les dépendances explicites ; un registre reste acceptable pour des plugins découverts dynamiquement.

### 34. Pattern Pipeline / Pipes and Filters ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Décomposer un traitement en étapes indépendantes chaînées, chaque étape recevant la sortie de la précédente. Exemples : Java Streams, opérateurs RxJS, `ItemReader → Processor → Writer` de Spring Batch, filtres de gateway, pipelines CI. Il favorise la réutilisation et le parallélisme.

### 35. Pattern Producer-Consumer avec `BlockingQueue` ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Découpler les producteurs et les consommateurs par une file bornée thread-safe : les producteurs bloquent quand elle est pleine (backpressure), les consommateurs quand elle est vide. `ArrayBlockingQueue`, `LinkedBlockingQueue` ; les `ExecutorService` l'utilisent en interne. Kafka est sa version distribuée.

### 36. Pattern Circuit Breaker : quels sont ses états ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Closed (appels normaux, comptage des échecs), Open (appels rejetés immédiatement pendant un délai après dépassement du seuil), Half-Open (quelques appels de test ; succès → Closed, échec → Open). Il évite les cascades de pannes et laisse le temps au service défaillant de récupérer.

### 37. Pattern Retry et ses règles ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Réessayer une opération échouée pour une erreur transitoire, avec limite de tentatives, backoff exponentiel et jitter, uniquement pour des opérations idempotentes et des erreurs retriables. À combiner avec timeout et circuit breaker ; sans ces garde-fous, les retries aggravent les pannes.

### 38. Pattern Cache-Aside et ses alternatives ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** L'application vérifie le cache, lit la base en cas de miss et alimente le cache (Spring `@Cacheable`). Alternatives : read-through (le cache charge lui-même), write-through (écriture synchrone dans cache et base), write-behind (écriture asynchrone en base). L'invalidation (`@CacheEvict`, TTL) est le point délicat.

### 39. Pattern Idempotency Key ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Le client envoie un identifiant unique avec une requête non idempotente (paiement) ; le serveur stocke le résultat associé et renvoie la même réponse en cas de rejeu, sans réexécuter l'opération. Indispensable pour les retries réseau et les consommateurs de messages ; l'identifiant est stocké avec un TTL.

### 40. Pattern Rate Limiter : token bucket vs sliding window ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Token bucket : des jetons sont ajoutés à débit constant dans un seau de capacité fixe ; chaque requête en consomme un, autorisant des rafales bornées. Sliding window compte les requêtes sur une fenêtre glissante, plus strict. Bucket4j (Java), Resilience4j et les gateways les implémentent, souvent avec Redis en distribué.

### 41. Pattern MVC, MVP et MVVM côté frontend ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** MVC : le contrôleur reçoit les entrées et met à jour modèle et vue. MVP : le presenter fait toute la logique de présentation, la vue est passive. MVVM : la vue se lie déclarativement à un ViewModel via data binding (Angular, Vue). Angular mélange MVVM (composant = ViewModel + template) et services pour le modèle.

### 42. Pattern Container/Presentational (smart/dumb components) ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Séparer les composants qui gèrent l'état et les appels (containers, connectés aux services/store) des composants purement visuels recevant des `@Input` et émettant des `@Output` (presentational, `OnPush`, faciles à tester et réutiliser). Il structure les applications Angular/React et facilite Storybook.

### 43. Pattern Facade côté frontend (facade service avec store) ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Un service Angular exposant une API simple (signals/observables d'état + méthodes d'action) aux composants, en masquant la complexité du store (NgRx) ou des appels HTTP. Les composants ne dépendent plus de l'implémentation de l'état, ce qui permet de changer de solution de state management.

### 44. Pattern Higher-Order Component / Render Props / Hooks en React ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Trois techniques de réutilisation de logique : HOC (fonction enveloppant un composant), render props (composant recevant une fonction de rendu), hooks (fonctions `useX` composables, approche moderne). Les hooks ont largement remplacé les deux autres pour leur lisibilité et l'absence de « wrapper hell ».

### 45. Pattern Module et Revealing Module en JavaScript ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Utiliser une closure/IIFE pour encapsuler un état privé et n'exposer qu'une API publique. Les modules ES (`export`) rendent ce pattern natif : tout ce qui n'est pas exporté est privé. Les champs privés de classe (`#field`) complètent l'encapsulation.

### 46. Pattern Pub/Sub vs Observer ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Observer : les observateurs s'abonnent directement au sujet (couplage direct, synchrone, en mémoire). Pub/Sub : un intermédiaire (bus, broker) découple éditeurs et abonnés qui ne se connaissent pas, souvent asynchrone et distribué (Kafka, EventBridge). RxJS `Subject` est un Observer ; un topic Kafka est du Pub/Sub.

### 47. Pattern Saga vs pattern Process Manager ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** La saga coordonne une séquence de transactions locales avec compensations. Le Process Manager (orchestrateur) est un composant à état qui décide des prochaines étapes selon les événements reçus, pouvant gérer des flux plus complexes que linéaires. En pratique, un orchestrateur de saga est un process manager.

### 48. Qu'est-ce qu'un anti-pattern et lesquels sont fréquents ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Une solution récurrente qui semble bonne mais crée plus de problèmes : God Object (classe qui fait tout), Spaghetti Code, Golden Hammer (même outil partout), Copy-Paste Programming, Premature Optimization, Magic Strings, Lava Flow (code mort conservé), Big Ball of Mud, Anemic Domain Model, Distributed Monolith.

### 49. Comment les fonctionnalités modernes de Java rendent-elles certains patterns inutiles ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Les lambdas remplacent Strategy/Command à une méthode ; records les DTO/Value Objects et Builder simples ; sealed interfaces + pattern matching remplacent Visitor ; `Optional` le Null Object ; streams le pattern Iterator ; enums le Singleton et les State simples. Le pattern survit comme concept, sa mise en œuvre se simplifie.

### 50. Comment choisir un pattern et éviter la « pattern-ite » ?
`🟠 Intermédiaire` · Sujet : **Design Pattern**

**Réponse :** Partir du problème (variation à isoler, couplage à réduire, création complexe) et non du pattern. Introduire un pattern quand la douleur est réelle (troisième duplication, `switch` grandissant), le nommer dans le code pour la communication, et préférer la solution la plus simple. Les patterns sont un vocabulaire, pas un objectif.
