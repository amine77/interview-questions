# 🧹 Clean Code & Clean Architecture

> SRP, DRY, code smells, Loi de Déméter, Use Cases, DIP

**50 questions**

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

### 13. Que signifient les principes SOLID ?
`🟢 Débutant` · Sujet : **Clean Code**

**Réponse :** S : responsabilité unique. O : ouvert à l'extension, fermé à la modification. L : substitution de Liskov (un sous-type doit pouvoir remplacer son type de base sans casser le comportement). I : ségrégation des interfaces (petites interfaces spécifiques). D : inversion de dépendance (dépendre des abstractions). Ils visent un code modulaire et facile à faire évoluer.

### 14. Expliquez le principe Open/Closed avec un exemple.
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Ajouter un comportement sans modifier le code existant. Exemple : un calcul de remise avec un `switch` sur le type de client doit être modifié à chaque nouveau type ; avec une interface `DiscountPolicy` et une implémentation par type (Strategy), on ajoute une classe sans toucher au calculateur. Il s'applique là où le changement est probable, pas partout.

### 15. Expliquez le principe de substitution de Liskov et un contre-exemple classique.
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Le classique `Square extends Rectangle` : `setWidth` sur un carré doit aussi changer la hauteur, cassant les attentes d'un code écrit pour `Rectangle`. Signes de violation : méthodes héritées levant `UnsupportedOperationException`, préconditions renforcées, `instanceof` dans les appelants. Préférer la composition ou une hiérarchie basée sur le comportement.

### 16. Qu'est-ce que la ségrégation des interfaces (ISP) et son lien avec les ports hexagonaux ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Un client ne doit pas dépendre de méthodes qu'il n'utilise pas. Une interface `UserRepository` de 20 méthodes force chaque adaptateur ou mock à tout implémenter. Des ports fins (`FindUserPort`, `SaveUserPort`) rendent explicites les besoins de chaque use case et simplifient les tests.

### 17. Quelles règles pour écrire de bonnes fonctions ?
`🟢 Débutant` · Sujet : **Clean Code**

**Réponse :** Courtes, un seul niveau d'abstraction, un nom qui dit ce qu'elles font, peu de paramètres (max 3, sinon objet paramètre), pas d'effets de bord cachés, pas de flags booléens (deux fonctions), séparation commande/requête (une fonction change l'état ou retourne une valeur, pas les deux).

### 18. Quand un commentaire est-il utile et quand est-il un smell ?
`🟢 Débutant` · Sujet : **Clean Code**

**Réponse :** Utile : expliquer le « pourquoi » (contrainte métier, contournement d'un bug de librairie, décision), avertir des conséquences, Javadoc d'API publique. Smell : paraphraser le code (`// incrémente i`), commenter du code mort, compenser un mauvais nommage, journal de modifications (Git le fait). Le code doit s'expliquer lui-même d'abord.

### 19. Comment gérer les erreurs proprement (exceptions vs codes de retour, `Optional`) ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Utiliser des exceptions non vérifiées pour les erreurs inattendues, avec un contexte utile ; `Optional` pour l'absence légitime d'une valeur en retour (jamais en paramètre ni en champ) ; des types Result/sealed pour les échecs métier attendus. Ne pas retourner ni passer `null`, ne pas avaler les exceptions, et traduire les exceptions techniques à la frontière.

### 20. Qu'est-ce que l'obsession des primitifs (primitive obsession) et les Value Objects ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Représenter un email, un montant ou un identifiant par un `String`/`double` disperse la validation et permet de confondre les paramètres. Un Value Object (`record Email(String value)` validant à la construction, `Money` avec devise) centralise les règles, rend le code auto-documenté et impossible à mal typer.

### 21. Qu'est-ce que le refactoring et quelles techniques courantes ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Modifier la structure du code sans changer son comportement, protégé par des tests. Techniques (Fowler) : extraire méthode/classe, renommer, remplacer condition par polymorphisme, introduire objet paramètre, déplacer méthode, remplacer nombre magique par constante, inliner. À faire en petits pas, commit par commit.

### 22. Qu'est-ce que la règle du Boy Scout ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Laisser le code un peu plus propre qu'on l'a trouvé : à chaque intervention, améliorer un nom, extraire une méthode, supprimer du code mort. L'amélioration continue et opportuniste évite les grands chantiers de refactoring et la dérive progressive vers le legacy.

### 23. Qu'est-ce que la complexité cyclomatique et cognitive ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Cyclomatique : nombre de chemins d'exécution indépendants (branches, boucles) ; au-delà de 10, la fonction est difficile à tester. Cognitive (SonarQube) : mesure l'effort de compréhension, pénalise l'imbrication plus que les branches plates. Les deux orientent le refactoring (early return, extraction, polymorphisme).

### 24. Qu'est-ce que le couplage et la cohésion ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Le couplage mesure la dépendance entre modules (faible souhaité : changer l'un n'impose pas de changer l'autre). La cohésion mesure à quel point les éléments d'un module servent un même but (forte souhaitée). Le couplage afférent/efférent et les métriques d'instabilité aident à repérer les modules à restructurer.

### 25. Différence entre YAGNI, KISS et over-engineering ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** YAGNI (You Aren't Gonna Need It) : ne pas implémenter ce qui n'est pas demandé maintenant. KISS : préférer la solution la plus simple qui fonctionne. L'over-engineering (abstractions spéculatives, configurabilité inutile, microservices prématurés) coûte en maintenance sans valeur. Le bon moment pour une abstraction est la deuxième ou troisième occurrence réelle.

### 26. Qu'est-ce que le code mort et pourquoi le supprimer ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Code jamais exécuté : méthodes non appelées, branches inatteignables, feature flags périmés, fichiers commentés. Il alourdit la lecture, trompe sur le comportement réel, maintient des dépendances inutiles et peut cacher des vulnérabilités. Git conserve l'historique : supprimer sans crainte.

### 27. Comment nommer les tests et structurer un fichier de test lisible ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Nom décrivant le comportement et la condition (`shouldThrowWhenAmountIsNegative`, ou `@DisplayName` en langage naturel), une assertion logique par test, données de test construites par des builders/Object Mothers pour éviter le bruit, pas de logique conditionnelle dans les tests, et un test doit se lire comme une spécification.

### 28. Qu'est-ce que le TDD et le cycle red-green-refactor ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Écrire d'abord un test qui échoue (red), écrire le minimum de code pour le faire passer (green), puis améliorer la structure (refactor) en gardant les tests verts. Bénéfices : conception guidée par l'usage, couverture naturelle, petits pas, feedback rapide. Difficile sur du code exploratoire ou très couplé à l'infrastructure.

### 29. Comment appliquer Clean Code aux tests eux-mêmes ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Les tests sont du code de production : DRY raisonné (mais lisibilité avant réutilisation), pas de duplication de la logique testée, fixtures explicites, noms parlants, pas de tests dépendant d'un ordre, suppression des tests obsolètes. Un test illisible ne sera pas maintenu et finira commenté.

### 30. Qu'est-ce que la revue de code efficace et que vérifier ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Petites PR (<400 lignes), description claire du pourquoi, revue de la conception avant le style (les linters gèrent le style), tests présents et pertinents, nommage, gestion d'erreurs, sécurité, lisibilité. Commentaires bienveillants et précis, distinction bloquant/suggestion, et réponse rapide pour ne pas bloquer le flux.

### 31. Qu'est-ce que le pattern « Tell, Don't Ask » ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Plutôt que d'interroger un objet sur son état pour décider à sa place (`if (account.getBalance() > amount) account.setBalance(...)`), on lui demande d'agir (`account.withdraw(amount)`) et il applique lui-même ses règles. Cela protège les invariants et évite le modèle anémique où toute la logique vit dans les services.

### 32. Qu'est-ce qu'un modèle de domaine anémique ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Des entités réduites à des getters/setters, toute la logique métier étant dans des services procéduraux. C'est un anti-pattern DDD : les règles sont dispersées, les invariants non protégés, et le code duplique les validations. Remède : déplacer les comportements dans les entités/agrégats et les Value Objects.

### 33. Qu'est-ce que l'immutabilité et pourquoi la favoriser ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Un objet immuable ne change pas après création (records, `final`, collections immuables `List.of`). Avantages : thread-safety sans verrou, raisonnement simplifié, pas d'effets de bord cachés, clés de map sûres, cache et memoization. On crée de nouvelles instances via `with` methods ou builders.

### 34. Qu'est-ce que la séparation commande/requête (CQS) au niveau des méthodes ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Une méthode est soit une commande qui modifie l'état sans retourner de valeur (ou juste un statut), soit une requête qui retourne une valeur sans effet de bord. Cela rend le code prévisible et testable ; `stack.pop()` est une exception connue. CQRS est l'application de ce principe à l'échelle de l'architecture.

### 35. Qu'est-ce que le principe de moindre surprise ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Une méthode ou API doit se comporter comme son nom et sa signature le laissent supposer : un getter ne modifie rien, `save` ne supprime pas, une méthode ne lève pas d'exception inattendue. Les surprises coûtent du temps de débogage et minent la confiance dans le code.

### 36. Quelles sont les couches de la Clean Architecture et le sens des dépendances ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Du centre vers l'extérieur : Entities (règles métier d'entreprise), Use Cases (règles applicatives), Interface Adapters (contrôleurs, presenters, gateways), Frameworks & Drivers (web, base, UI). Les dépendances pointent toujours vers l'intérieur ; les couches externes implémentent les interfaces définies par les couches internes.

### 37. Comment organiser les packages d'un projet Spring Boot en architecture hexagonale ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** `domain` (modèle, ports, services métier, sans dépendance Spring), `application` (use cases, orchestrations, transactions), `adapters/in` (REST controllers, consumers Kafka, mappers DTO→commandes), `adapters/out` (JPA repositories implémentant les ports, clients HTTP), et `config` pour le câblage. ArchUnit vérifie que `domain` n'importe rien d'`adapters`.

### 38. Faut-il séparer entités JPA et entités du domaine ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Idéalement oui : les entités JPA sont des détails de persistance (annotations, proxies, cycles) et le domaine reste pur et testable sans base. Le coût est un mapping supplémentaire (MapStruct). Un compromis pragmatique dans les petits projets est d'utiliser les entités JPA comme domaine, en acceptant le couplage.

### 39. Qu'est-ce qu'un agrégat en DDD et quelles règles respecter ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Un groupe d'objets (racine + entités/VO) traité comme une unité de cohérence transactionnelle. Règles : on n'accède aux membres que via la racine, les invariants sont garantis dans l'agrégat, une transaction ne modifie qu'un agrégat, les références entre agrégats se font par identifiant, et les agrégats restent petits.

### 40. Qu'est-ce qu'un événement de domaine et comment le publier dans Spring ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Un fait métier survenu (`OrderPlaced`), exprimé au passé, émis par un agrégat. Spring permet de les collecter avec `@DomainEvents` sur l'agrégat ou `ApplicationEventPublisher`, et de les traiter via `@TransactionalEventListener(phase = AFTER_COMMIT)` pour ne réagir qu'après validation de la transaction. Spring Modulith les persiste pour la fiabilité.

### 41. Différence entre couche « application » et couche « domaine » ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Le domaine contient les règles invariantes de l'entreprise (calculs, validations, états). La couche application orchestre les cas d'usage : charge les agrégats via les ports, appelle le domaine, persiste, publie les événements, gère la transaction et la sécurité. Elle ne contient pas de règle métier elle-même.

### 42. Qu'est-ce que le « Screaming Architecture » ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** La structure du projet doit crier son intention métier (`orders`, `billing`, `shipping`) et non sa technologie (`controllers`, `services`, `repositories`). Organiser par fonctionnalité (package by feature / vertical slices) améliore la cohésion et facilite la localisation du code.

### 43. Différence entre architecture en couches classique, hexagonale, onion et clean ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** L'architecture en couches classique fait dépendre le métier de la persistance (le service appelle le DAO). Hexagonale, onion et clean inversent cette dépendance : le métier définit des ports, l'infrastructure les implémente. Elles diffèrent surtout par le vocabulaire et le nombre de cercles ; l'idée centrale est la même.

### 44. Où placer la validation dans une architecture propre ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Validation syntaxique/format à la frontière (DTO avec Bean Validation dans l'adaptateur entrant). Validation des invariants métier dans le domaine (constructeurs de Value Objects, méthodes d'agrégat). Validation des règles applicatives (unicité en base, droits) dans le use case. Ne jamais faire confiance à la seule validation front.

### 45. Qu'est-ce qu'un DTO, un mapper et pourquoi ne pas exposer les entités ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Un DTO transporte des données entre couches sans logique. Exposer une entité JPA dans une API couple le contrat externe au schéma de base, provoque des fuites (champs sensibles, lazy loading, cycles JSON) et bloque le refactoring. Un mapper (MapStruct, manuel) convertit explicitement ; le coût est justifié par le découplage.

### 46. Comment gérer les transactions sans coupler le domaine à Spring ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Placer `@Transactional` sur le use case (couche application) ou définir un port `TransactionRunner`/`UnitOfWork` que l'infrastructure implémente avec `TransactionTemplate`. Le domaine ne connaît ni annotations ni `EntityManager` ; ses méthodes sont de purs calculs sur des objets en mémoire.

### 47. Qu'est-ce que le pattern « Vertical Slice Architecture » ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Organiser le code par fonctionnalité de bout en bout (une requête/commande = un dossier avec son handler, sa validation, son accès données) plutôt que par couches horizontales. Chaque slice est indépendante et peut choisir sa complexité (CRUD simple ou domaine riche). Elle réduit le couplage entre fonctionnalités et facilite les équipes en parallèle.

### 48. Qu'est-ce que l'ADR (Architecture Decision Record) ?
`🟠 Intermédiaire` · Sujet : **Clean Architecture**

**Réponse :** Un court document versionné avec le code décrivant une décision d'architecture : contexte, options considérées, décision, conséquences. Il conserve le « pourquoi » (choix de Kafka, d'une architecture hexagonale), évite de rouvrir les débats et facilite l'onboarding. Un ADR est immuable ; on le remplace par un nouveau si la décision change.

### 49. Qu'est-ce que la dette technique et comment la gérer ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Le coût futur d'un compromis pris aujourd'hui (délibéré ou accidentel). La gérer : la rendre visible (backlog, commentaires `TODO` liés à des tickets, métriques Sonar), la rembourser en continu (règle du Boy Scout, 10-20 % du temps), prioriser par impact (zones modifiées souvent), et éviter la dette « imprudente et involontaire » par la revue et les standards.

### 50. Comment lire et améliorer du code legacy sans tests ?
`🟠 Intermédiaire` · Sujet : **Clean Code**

**Réponse :** Écrire d'abord des tests de caractérisation (approval/golden master) capturant le comportement actuel, identifier les seams (points où injecter des dépendances) pour isoler le code, refactorer en petits pas (extraire, introduire des interfaces), et appliquer le strangler pour remplacer progressivement. Ne pas réécrire tout d'un coup.
