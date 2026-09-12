# ☕ Java & JVM

> Java 8-21, Virtual Threads, GC, JIT, concurrency, memory leaks, thread dumps

**100 questions**

---

### 1. Quelle est la différence entre `==` et `.equals()` pour les objets en Java ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** `==` compare les références mémoire (l'objet est-il exactement le même en mémoire), tandis que `.equals()` compare le contenu logique des objets selon l'implémentation définie dans la classe. Pour les `String`, il faut toujours utiliser `.equals()` pour comparer le contenu.

### 2. Différence entre classe abstraite et interface ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Classe abstraite : champs d'état, constructeurs, héritage simple. Interface : contrat, méthodes par défaut possibles, héritage multiple, sans état propre.

### 3. Différence `ArrayList` / `LinkedList` ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** ArrayList = tableau redimensionnable, accès O(1), insertions milieu O(n). LinkedList = liste chaînée, insertions O(1), accès séquentiel O(n).

### 4. Rôle du garbage collector ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Libère automatiquement les objets non référencés, évitant fuites mémoire et erreurs manuelles (double free).

### 5. Différence `StringBuilder` / `StringBuffer` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** StringBuffer est synchronisé (thread-safe), StringBuilder ne l'est pas (plus performant mono-thread).

### 6. Autoboxing/unboxing ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Conversion automatique primitif <-> wrapper, risque de NullPointerException à l'unboxing d'un null.

### 7. Exception checked / unchecked ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** Checked doit être déclarée/capturée. Unchecked (RuntimeException) n'impose pas cette obligation.

### 8. Interface fonctionnelle ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Interface avec une seule méthode abstraite, implémentable via lambda (ex: Runnable, Function<T,R>).

### 9. Qu'est-ce que les Virtual Threads (Project Loom) introduits en Java 21 ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** Ce sont des threads légers gérés par la JVM (et non par l'OS), permettant de créer des millions de threads sans épuiser les ressources système. Ils simplifient le code concurrent bloquant tout en offrant la scalabilité d'un modèle asynchrone, particulièrement utile pour les applications à fort I/O.

### 10. Quelle est la différence entre `synchronized` et `ReentrantLock` en Java ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `synchronized` est un mot-clé natif, plus simple mais moins flexible (pas de tentative de verrouillage avec timeout, pas d'interruption). `ReentrantLock` offre plus de contrôle (`tryLock()`, `lockInterruptibly()`, verrous équitables) au prix d'une gestion manuelle explicite (`unlock()` dans un `finally`).

### 11. Comment identifier une fuite mémoire dans une application Java en production ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** En analysant un heap dump (via `jmap` ou VisualVM) pour repérer des objets qui s'accumulent anormalement, en surveillant les métriques GC via JFR (Java Flight Recorder), et en vérifiant les références statiques ou listeners non désenregistrés qui empêchent le GC de libérer la mémoire.

### 12. Que permet de faire un thread dump et comment l'obtenir ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Java**

**Réponse :** Il capture l'état de tous les threads d'une JVM à un instant donné, utile pour diagnostiquer des blocages (deadlocks), une forte consommation CPU ou des threads bloqués. On l'obtient via `jstack <pid>`, `/actuator/threaddump`, ou `kill -3` sur le processus.

### 13. Qu'est-ce qu'un ExecutorService et pourquoi l'utiliser plutôt que de créer des Thread manuellement ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Abstraction de gestion de pool de threads (Executors.newFixedThreadPool(), etc.) qui réutilise des threads existants plutôt que d'en créer un nouveau à chaque tâche, réduisant l'overhead de création/destruction et permettant un contrôle centralisé (limitation de concurrence, file d'attente de tâches).

### 14. Qu'est-ce que les Records Patterns et le Pattern Matching for switch introduits en Java 21 ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** Les Records Patterns permettent de déstructurer un record directement dans un switch ou instanceof, extrayant ses composants. Combinés au Pattern Matching for switch, ils simplifient l'écriture de code conditionnel basé sur le type et la structure des données.

### 15. Qu'est-ce que le "Structured Concurrency" (preview en Java 21) ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** API traitant un groupe de tâches concurrentes liées comme une seule unité de travail, simplifiant la gestion du cycle de vie, de l'annulation et de la propagation des erreurs (via StructuredTaskScope).

### 16. Qu'est-ce qu'une race condition et comment l'éviter ?
`🟢 Débutant` · Sujet : **Multithreading**

**Réponse :** Situation où le résultat dépend de l'ordre d'exécution imprévisible de threads concurrents accédant à une ressource partagée. Évitée via synchronisation, structures thread-safe, ou immutabilité.

### 17. Qu'est-ce que l'échappement d'objets (escape analysis) et son rôle dans l'optimisation JVM ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Technique du JIT déterminant si un objet reste local à une méthode. Si oui, la JVM peut l'allouer sur la pile plutôt que le tas, réduisant la pression sur le GC.

### 18. Que permet de diagnostiquer un "heap dump" et quand le générer ?
`🟢 Débutant` · Sujet : **Troubleshooting Java**

**Réponse :** Capture un instantané complet de la mémoire heap, permettant d'analyser les objets et leurs références. Utile pour fuites mémoire ou OutOfMemoryError, via jmap -dump ou -XX:+HeapDumpOnOutOfMemoryError.

### 19. Qu'est-ce que les Sequenced Collections introduites en Java 21 ?
`🟢 Débutant` · Sujet : **Java 21**

**Réponse :** Nouvelle hiérarchie d'interfaces (SequencedCollection, SequencedSet, SequencedMap) uniformisant l'accès au premier/dernier élément et l'itération inversée, via getFirst(), getLast(), reversed().

### 20. Qu'est-ce que le problème producteur-consommateur et comment le résoudre en Java ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Threads producteurs ajoutant des données à une file partagée pendant que des consommateurs les retirent. Résolu via BlockingQueue qui gère nativement attente et notification.

### 21. Qu'est-ce que le JIT compiler et comment améliore-t-il les performances ?
`🟢 Débutant` · Sujet : **Optimisation Java**

**Réponse :** Composant de la JVM compilant le bytecode en code machine natif à l'exécution, optimisant les hot spots, meilleur qu'une interprétation pure.

### 22. Virtual Threads pinning et pourquoi les éviter ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** Situation où un virtual thread reste épinglé à son carrier thread lors d'un appel bloquant (synchronized, JNI), annulant les bénéfices de scalabilité. Préférer ReentrantLock.

### 23. Deadlock et ses quatre conditions nécessaires ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Blocage mutuel entre threads. Conditions : exclusion mutuelle, détention et attente, absence de préemption, attente circulaire. Éliminer une condition empêche le deadlock.

### 24. String pooling et son impact mémoire ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Pool de chaînes littérales évitant la duplication de String identiques. String.intern() ajoute une chaîne dynamique au pool.

### 25. Memory leak logique malgré le garbage collector ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Java**

**Réponse :** Objets restant référencés involontairement (listeners, caches sans éviction), empêchant le GC de les libérer, menant à un OutOfMemoryError.

### 26. Unnamed Patterns and Variables (preview) ?
`🟢 Débutant` · Sujet : **Java 21**

**Réponse :** Syntaxe utilisant _ pour ignorer explicitement une variable ou un composant de pattern matching non utilisé.

### 27. Mot-clé volatile et quand l'utiliser ?
`🟢 Débutant` · Sujet : **Multithreading**

**Réponse :** Garantit la visibilité immédiate des lectures/écritures entre threads. Utile pour des flags booléens, insuffisant pour opérations composées (préférer AtomicInteger).

### 28. Warm-up d'une JVM et impact sur les benchmarks ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Période où le JIT optimise progressivement le code chaud. Avant sa fin, le code s'exécute peu optimisé, faussant les mesures si non pris en compte.

### 29. Generational ZGC ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** Évolution du ZGC séparant objets jeunes et vieux en générations, appliquant l'hypothèse générationnelle pour réduire davantage les pauses de collecte.

### 30. CompletableFuture vs Future classique ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Future ne permet que get() bloquant. CompletableFuture permet de chaîner des transformations, combiner plusieurs futures, gérer les erreurs fonctionnellement.

### 31. Lazy initialization et son compromis ?
`🟢 Débutant` · Sujet : **Optimisation Java**

**Réponse :** Différer la création d'un objet coûteux jusqu'à son premier usage. Compromis : complexité accrue en multi-thread, léger surcoût au premier accès.

### 32. Preview Feature en Java et pourquoi certaines fonctionnalités le sont ?
`🟢 Débutant` · Sujet : **Java 21**

**Réponse :** Fonctionnalité complète mais non finalisée, exposée pour recueillir des retours avant stabilisation, nécessitant --enable-preview.

### 33. Fork/Join Framework et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Divise récursivement une tâche en sous-tâches parallèles puis combine les résultats, adapté au diviser-pour-régner, via work-stealing.

### 34. Tiered compilation dans la JVM ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Combine plusieurs niveaux JIT (C1 rapide, C2 optimisé), démarrage rapide puis performances optimales sur le code critique.

### 35. Named Capture Group en regex ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** Groupe de capture nommé (?<nom>...) référençable par un nom explicite plutôt qu'un index, via Matcher.group("nom").

### 36. Thread daemon vs thread normal ?
`🟢 Débutant` · Sujet : **Multithreading**

**Réponse :** Un thread daemon ne bloque pas l'arrêt de la JVM ; utilisé pour des tâches de fond comme le garbage collector.

### 37. False sharing et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Deux threads modifiant des variables sur la même ligne de cache CPU, causant des invalidations. Évité via padding mémoire ou @Contended.

### 38. Foreign Function & Memory API (preview) et problème résolu ?
`🟠 Intermédiaire` · Sujet : **Java 21**

**Réponse :** Interagir avec du code natif et mémoire hors-tas sans JNI, syntaxe plus sûre et performante pour intégration système.

### 39. ThreadLocal et piège avec les pools de threads ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Variable propre à chaque thread. Piège : oubli de remove() dans un pool, causant fuite mémoire/contexte entre requêtes.

### 40. Connection pooling JDBC (HikariCP) ?
`🟢 Débutant` · Sujet : **Optimisation Java**

**Réponse :** Maintient un pool de connexions réutilisables, évitant le coût d'ouverture/fermeture. Pool par défaut de Spring Boot 2+.

### 41. Pourquoi une app Java peut être OOMKilled malgré -Xmx correct ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Java/K8s**

**Réponse :** La limite mémoire du conteneur doit couvrir aussi la mémoire native (metaspace, stacks, buffers directs), souvent sous-estimée.

### 42. Qu'est-ce qu'un `record` et quelles contraintes impose-t-il ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Un record est une classe immuable déclarée de façon concise (`record Point(int x, int y)`) qui génère automatiquement constructeur canonique, accesseurs, `equals`, `hashCode` et `toString`. Ses champs sont `final`, il ne peut pas hériter d'une autre classe (mais peut implémenter des interfaces) et on peut y ajouter des constructeurs compacts pour valider les invariants.

### 43. Qu'est-ce qu'une `sealed class` et quel problème résout-elle ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Une classe/interface `sealed` restreint explicitement la liste de ses sous-types (`permits`). Combinée au pattern matching sur `switch`, elle permet au compilateur de vérifier l'exhaustivité des cas, ce qui rend la modélisation de types algébriques (ex : `Result = Success | Failure`) sûre et lisible.

### 44. Expliquez le Java Memory Model (JMM) et la relation happens-before.
`🔴 Avancé` · Sujet : **Multithreading**

**Réponse :** Le JMM définit quand une écriture effectuée par un thread est visible par un autre. La relation happens-before est garantie par `synchronized`, `volatile`, le démarrage/join de threads, les `java.util.concurrent` locks et les classes atomiques. Sans elle, le compilateur et le CPU peuvent réordonner les instructions et un thread peut lire une valeur périmée en cache.

### 45. Différence entre `ConcurrentHashMap` et `Collections.synchronizedMap()` ?
`🔴 Avancé` · Sujet : **Multithreading**

**Réponse :** `synchronizedMap` verrouille toute la map à chaque opération (un seul thread à la fois). `ConcurrentHashMap` utilise un verrouillage fin par bucket/nœud et des lectures sans verrou, offrant un débit bien supérieur en forte concurrence, plus des opérations atomiques composées (`computeIfAbsent`, `merge`).

### 46. Quelles sont les principales différences entre `HashMap`, `LinkedHashMap` et `TreeMap` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `HashMap` : accès O(1), aucun ordre garanti. `LinkedHashMap` : même performance, conserve l'ordre d'insertion (ou d'accès, utile pour un cache LRU). `TreeMap` : arbre rouge-noir, clés triées, opérations en O(log n), permet les requêtes par plage (`headMap`, `ceilingKey`).

### 47. Pourquoi doit-on redéfinir `hashCode()` quand on redéfinit `equals()` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Le contrat impose que deux objets égaux selon `equals` aient le même `hashCode`. Sinon, deux objets « égaux » atterrissent dans des buckets différents d'une `HashMap`/`HashSet`, et la structure ne les retrouvera plus (doublons, `contains` faux).

### 48. Différence entre `Stream` séquentiel et `parallelStream()` : quand le parallélisme est-il contre-productif ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** `parallelStream()` découpe le traitement sur le `ForkJoinPool` commun. C'est rentable sur de grandes collections avec des opérations CPU-bound et sans état partagé. C'est contre-productif sur de petites collections, des opérations I/O bloquantes (le pool commun se retrouve saturé), ou des sources difficiles à découper (`LinkedList`, `iterate`).

### 49. Comment diagnostiquer une consommation CPU anormale d'une JVM en production ?
`🔴 Avancé` · Sujet : **Troubleshooting Java**

**Réponse :** Identifier le thread natif fautif avec `top -H -p <pid>`, convertir son id en hexadécimal, puis le retrouver dans un `jstack` (`nid=0x...`). On peut aussi utiliser JFR (`jcmd <pid> JFR.start`) ou async-profiler pour obtenir un flame graph. Les causes fréquentes : boucle infinie, GC excessif (vérifier avec `jstat -gcutil`), regex catastrophique, sérialisation JSON massive.

### 50. Qu'est-ce que le GraalVM Native Image et quels compromis implique-t-il ?
`🔴 Avancé` · Sujet : **Optimisation Java**

**Réponse :** Native Image compile l'application en exécutable natif via une analyse statique à la compilation (closed-world). Avantages : démarrage en millisecondes, empreinte mémoire réduite, idéal pour serverless et scale-to-zero. Compromis : build long, réflexion/proxies/JNI à déclarer explicitement (hints), pas de JIT adaptatif donc un débit de pointe parfois inférieur à HotSpot.

### 51. Qu'est-ce qu'une expression lambda et quelle est sa syntaxe ?
`🟢 Débutant` · Sujet : **Java 8**

**Réponse :** Une fonction anonyme concise implémentant une interface fonctionnelle : `(a, b) -> a + b`, `x -> x * 2`, `() -> System.out.println("ok")`. Le type des paramètres est inféré. Elle capture les variables locales à condition qu'elles soient effectivement finales. Elle remplace les classes anonymes verbeuses pour `Runnable`, `Comparator`, callbacks.

### 52. Que sont les références de méthode (`::`) ?
`🟢 Débutant` · Sujet : **Java 8**

**Réponse :** Une notation abrégée pour une lambda qui ne fait qu'appeler une méthode : `String::length` (méthode d'instance via paramètre), `System.out::println` (méthode d'instance d'un objet), `Integer::parseInt` (statique), `ArrayList::new` (constructeur). Elles améliorent la lisibilité quand la lambda n'apporte pas de logique.

### 53. Quelles sont les principales interfaces fonctionnelles de `java.util.function` ?
`🟢 Débutant` · Sujet : **Java 8**

**Réponse :** `Function<T,R>` (transforme), `Predicate<T>` (teste, retourne boolean), `Consumer<T>` (consomme sans retour), `Supplier<T>` (fournit), `UnaryOperator<T>`/`BinaryOperator<T>`, et les variantes `Bi*` (deux arguments) et primitives (`IntFunction`, `ToLongFunction`) qui évitent le boxing.

### 54. Qu'est-ce que l'API Stream et quelle est la différence avec une collection ?
`🟢 Débutant` · Sujet : **Java 8**

**Réponse :** Un pipeline de traitement déclaratif sur une séquence d'éléments (filtrage, transformation, agrégation). Contrairement à une collection, un stream ne stocke pas les données, est consommé une seule fois, évalué paresseusement (les opérations intermédiaires ne s'exécutent qu'à l'opération terminale) et peut être infini.

### 55. Différence entre opérations intermédiaires et terminales d'un Stream ?
`🟢 Débutant` · Sujet : **Java 8**

**Réponse :** Intermédiaires (`filter`, `map`, `sorted`, `distinct`, `limit`, `flatMap`) : retournent un nouveau stream et sont paresseuses. Terminales (`collect`, `forEach`, `reduce`, `count`, `findFirst`, `anyMatch`) : déclenchent l'exécution et produisent un résultat ou un effet. Sans opération terminale, rien ne s'exécute.

### 56. Différence entre `map` et `flatMap` ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** `map` applique une fonction à chaque élément (1 → 1). `flatMap` applique une fonction retournant un stream et aplatit le résultat (1 → 0..n) : utile pour une liste de listes, ou pour chaîner des `Optional`. `Stream<List<String>>` → `flatMap(List::stream)` → `Stream<String>`.

### 57. Comment fonctionne `Collectors` et quels collecteurs faut-il connaître ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** `toList()`/`toSet()`/`toMap(k, v, merge)`, `joining(", ")`, `groupingBy(classifier, downstream)` (avec `counting()`, `summingInt`, `mapping`), `partitioningBy(predicate)`, `averagingDouble`, `teeing` (Java 12) pour combiner deux collecteurs. `Stream.toList()` (Java 16) retourne une liste non modifiable.

### 58. Qu'est-ce que `reduce` et quelle est la différence avec `collect` ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** `reduce` combine les éléments en une seule valeur immuable via une opération associative (`reduce(0, Integer::sum)`), créant une nouvelle valeur à chaque étape. `collect` accumule dans un conteneur mutable (liste, map, StringBuilder), plus efficace pour construire des structures. Pour les sommes, préférer `mapToInt(...).sum()`.

### 59. Pourquoi les variables capturées par une lambda doivent-elles être effectivement finales ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** La lambda peut s'exécuter plus tard ou dans un autre thread : Java copie la valeur au moment de la capture, comme pour les classes anonymes. Autoriser la modification créerait des incohérences entre la copie et la variable locale. Contournement (à éviter) : un tableau d'un élément ou `AtomicInteger` ; préférer les collecteurs.

### 60. Qu'est-ce que `Optional` et quelles sont ses bonnes et mauvaises pratiques ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** Un conteneur signalant explicitement l'absence de valeur pour éviter les `NullPointerException`. Bien : type de retour, `map`/`flatMap`/`filter`/`orElseGet`/`orElseThrow`/`ifPresentOrElse`. Mal : `isPresent()` + `get()`, `Optional` en champ, en paramètre, en collection, ou `orElse(calculCoûteux())` (évalué même si présent).

### 61. Que sont les méthodes `default` et `static` dans les interfaces ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** Depuis Java 8, une interface peut fournir une implémentation par défaut (`default`) pour faire évoluer une API sans casser les implémentations existantes (`Collection.stream()`, `List.sort`), et des méthodes statiques utilitaires. Si deux interfaces fournissent la même méthode par défaut, la classe doit la redéfinir (`A.super.m()`). Java 9 ajoute les méthodes privées d'interface.

### 62. Qu'est-ce que l'API `java.time` et pourquoi remplace-t-elle `Date`/`Calendar` ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** Une API immuable et thread-safe inspirée de Joda-Time : `LocalDate`, `LocalDateTime` (sans fuseau), `ZonedDateTime`, `Instant` (point sur la ligne du temps), `Duration`/`Period`, `DateTimeFormatter`. `Date` était mutable, mal nommée, avec des mois indexés à 0 et une gestion de fuseaux confuse. Stocker en `Instant`/UTC, afficher en `ZonedDateTime`.

### 63. Comment fonctionne `Comparator` avec les lambdas ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** `Comparator.comparing(Person::getName)`, chaînage avec `.thenComparing(Person::getAge)`, inversion `.reversed()`, gestion des nulls `Comparator.nullsFirst(...)`, et versions primitives `comparingInt`. Ces combinateurs remplacent les classes anonymes et clarifient l'ordre de tri multi-critères.

### 64. Qu'est-ce que `CompletableFuture` et ses principales méthodes de composition ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** Un `Future` composable : `supplyAsync` (lancer), `thenApply` (transformer), `thenCompose` (chaîner une autre future, équivalent flatMap), `thenCombine` (joindre deux), `allOf`/`anyOf`, `exceptionally`/`handle` (erreurs), `orTimeout` (Java 9). Par défaut il utilise le `ForkJoinPool.commonPool()` ; fournir son propre executor pour les tâches bloquantes.

### 65. Quels sont les pièges des streams parallèles ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** Ils utilisent le `commonPool` partagé (une tâche bloquante le paralyse), le coût de découpage dépasse le gain pour les petites collections ou les sources mal découpables (`LinkedList`, `iterate`), les opérations avec état (`sorted`, `distinct`, `limit`) sont coûteuses, et les effets de bord non thread-safe (`ArrayList` partagée dans `forEach`) corrompent les données. Mesurer avant d'utiliser.

### 66. Différence entre `Iterator` et Stream pour parcourir une collection ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** L'itération externe (`for`, `Iterator`) contrôle explicitement le parcours, permet de modifier la collection via `iterator.remove()` et de sortir avec `break`. Le stream est une itération interne déclarative, composable, potentiellement parallèle, mais ne permet pas de modifier la source ni de « break » (sauf `takeWhile` Java 9, `findFirst`).

### 67. Qu'est-ce que le `Spliterator` ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** L'abstraction sous-jacente aux streams pour parcourir et découper (`trySplit`) une source, permettant le parallélisme. Ses caractéristiques (`SIZED`, `ORDERED`, `DISTINCT`, `SORTED`) permettent des optimisations (par exemple `count()` sans parcourir si `SIZED`). On l'implémente pour exposer une source personnalisée en stream efficace.

### 68. Comment gérer les exceptions checked dans les lambdas ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** Les interfaces fonctionnelles standard ne déclarent pas d'exceptions checked. Solutions : envelopper dans une exception non checked dans la lambda, écrire une interface fonctionnelle déclarant `throws`, ou un utilitaire `unchecked(ThrowingFunction)` (Vavr, Lombok `@SneakyThrows`). Éviter d'avaler silencieusement les exceptions.

### 69. Qu'est-ce que `Stream.iterate`, `generate` et les streams infinis ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** `Stream.iterate(seed, f)` et `Stream.generate(supplier)` créent des streams infinis, à borner par `limit`, `takeWhile` (Java 9) ou la variante `iterate(seed, hasNext, next)`. Utile pour les suites, les tentatives de retry, ou la génération de données de test.

### 70. Qu'est-ce que le pattern « Collectors.groupingBy » multi-niveaux et le downstream ?
`🟠 Intermédiaire` · Sujet : **Java 8**

**Réponse :** `groupingBy(Order::getCountry, groupingBy(Order::getYear, summingDouble(Order::getAmount)))` produit une `Map<String, Map<Integer, Double>>`. Le collecteur aval (downstream) transforme chaque groupe : `counting`, `mapping(f, toList())`, `maxBy`, `collectingAndThen(toList(), List::size)`. Le type de map se contrôle avec `TreeMap::new` en second argument.

### 71. Différence entre concurrence et parallélisme ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** La concurrence est la gestion de plusieurs tâches dont les exécutions se chevauchent dans le temps (même sur un seul cœur, par entrelacement). Le parallélisme est l'exécution simultanée réelle sur plusieurs cœurs. Le multithreading Java permet les deux ; les virtual threads visent la concurrence massive d'I/O, les parallel streams et Fork/Join le parallélisme CPU.

### 72. Comment créer et démarrer un thread, et pourquoi `start()` et non `run()` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `new Thread(runnable).start()` ou `Thread.ofVirtual().start(runnable)` (Java 21). `start()` demande à la JVM de créer un thread natif et d'y exécuter `run()` ; appeler `run()` directement exécute le code dans le thread courant, sans concurrence. Un thread ne peut être démarré qu'une fois.

### 73. Quels sont les états d'un thread Java ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `NEW` (créé, non démarré), `RUNNABLE` (exécutable, en cours ou en attente de CPU), `BLOCKED` (attend un moniteur `synchronized`), `WAITING` (`wait()`, `join()`, `LockSupport.park()` sans timeout), `TIMED_WAITING` (`sleep`, `wait(timeout)`), `TERMINATED`. Un thread dump affiche ces états, précieux pour diagnostiquer contention et blocages.

### 74. Comment fonctionnent `wait()`, `notify()` et `notifyAll()` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Méthodes de `Object` utilisables uniquement dans un bloc `synchronized` sur le même moniteur. `wait()` libère le moniteur et suspend le thread jusqu'à `notify`/`notifyAll` (toujours dans une boucle vérifiant la condition, à cause des réveils intempestifs). `notifyAll` est plus sûr que `notify`. Aujourd'hui, préférer `Condition`, `BlockingQueue` ou `CountDownLatch`.

### 75. Comment interrompre un thread proprement ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `thread.interrupt()` positionne un flag : les méthodes bloquantes (`sleep`, `wait`, `join`, `BlockingQueue.take`) lèvent `InterruptedException` ; le code CPU doit vérifier `Thread.currentThread().isInterrupted()`. Quand on attrape `InterruptedException` sans pouvoir la propager, restaurer le flag avec `Thread.currentThread().interrupt()`. Jamais `Thread.stop()`.

### 76. Qu'est-ce qu'un `ThreadPoolExecutor` et quels sont ses paramètres clés ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `corePoolSize` (threads permanents), `maximumPoolSize` (plafond), `keepAliveTime`, la file de tâches (`LinkedBlockingQueue` illimitée : max n'est jamais atteint ; `SynchronousQueue` ; `ArrayBlockingQueue` bornée), la `ThreadFactory` (nommage) et la `RejectedExecutionHandler` (`AbortPolicy`, `CallerRunsPolicy`). Les `Executors.newFixedThreadPool` masquent ces choix ; en production, construire explicitement.

### 77. Comment dimensionner un pool de threads ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Tâches CPU : nombre de cœurs (+1). Tâches I/O bloquantes : cœurs × (1 + temps d'attente / temps de calcul), souvent plusieurs dizaines. Séparer les pools par type de tâche pour isoler les pannes (bulkhead), borner la file, monitorer taille active et file. Avec Java 21, les virtual threads suppriment la question pour les tâches I/O.

### 78. Différence entre `Runnable` et `Callable` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `Runnable.run()` ne retourne rien et ne peut lever d'exception checked. `Callable<V>.call()` retourne une valeur et peut lever `Exception`. `ExecutorService.submit(Callable)` retourne un `Future<V>` pour récupérer le résultat ou l'exception (`ExecutionException`). Une exception dans un `Runnable` soumis via `submit` est silencieusement stockée dans le `Future` si `get()` n'est jamais appelé.

### 79. Que sont `CountDownLatch`, `CyclicBarrier` et `Semaphore` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `CountDownLatch` : attendre qu'un compte atteigne zéro (N tâches terminées), à usage unique. `CyclicBarrier` : N threads s'attendent mutuellement à un point de rendez-vous, réutilisable, avec action de barrière. `Semaphore` : limiter l'accès concurrent à N permis (pool de connexions, rate limiting). `Phaser` généralise les deux premiers.

### 80. Qu'est-ce que `ReadWriteLock` et `StampedLock` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `ReentrantReadWriteLock` autorise plusieurs lecteurs simultanés ou un seul écrivain, utile quand les lectures dominent. `StampedLock` (Java 8) ajoute le verrouillage optimiste : `tryOptimisticRead()` lit sans verrou puis `validate(stamp)` vérifie qu'aucune écriture n'est intervenue ; non réentrant et sans `Condition`, à réserver aux cas mesurés.

### 81. Que sont les classes atomiques (`AtomicInteger`, `AtomicReference`, `LongAdder`) ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Des opérations lock-free basées sur CAS (compare-and-swap) : `incrementAndGet`, `compareAndSet`, `updateAndGet(f)`. `LongAdder`/`LongAccumulator` répartissent les mises à jour sur plusieurs cellules pour réduire la contention des compteurs très sollicités (métriques), au prix d'une lecture plus coûteuse. `AtomicReference` permet des mises à jour atomiques d'objets immuables.

### 82. Qu'est-ce que le CAS (compare-and-swap) et l'algorithme lock-free ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Une instruction atomique du processeur : « si la valeur vaut encore X, remplace-la par Y », renvoyant succès ou échec. Les structures lock-free bouclent jusqu'au succès au lieu de bloquer, évitant les deadlocks et les changements de contexte, mais peuvent souffrir de contention (spinning) et du problème ABA (résolu par `AtomicStampedReference`).

### 83. Quelles collections concurrentes connaître et quand les utiliser ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `ConcurrentHashMap` (verrouillage par segment, `compute`, `merge`), `CopyOnWriteArrayList` (lectures fréquentes, écritures rares : listeners), `ConcurrentLinkedQueue` (non bloquante), `BlockingQueue` (`ArrayBlockingQueue`, `LinkedBlockingQueue`, `PriorityBlockingQueue`) pour producteur-consommateur, `ConcurrentSkipListMap` (triée). Éviter `Vector`/`Hashtable` et les wrappers `synchronized*`.

### 84. Qu'est-ce qu'un livelock et une famine (starvation) ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Livelock : des threads répondent sans cesse aux actions des autres sans progresser (deux threads qui se cèdent mutuellement une ressource). Famine : un thread n'obtient jamais le CPU ou un verrou parce que d'autres sont prioritaires ou monopolisent (verrous non équitables, `synchronized` sous forte contention). Remèdes : backoff aléatoire, verrous équitables (`new ReentrantLock(true)`), limiter la durée des sections critiques.

### 85. Comment rendre une classe thread-safe ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Par ordre de préférence : immuabilité (champs `final`, pas de setter, copies défensives), confinement (l'objet n'est visible que d'un thread), synchronisation interne cohérente (un seul verrou protégeant tous les invariants), ou délégation à des composants thread-safe (`ConcurrentHashMap`, atomiques). Documenter la politique de synchronisation ; un mélange de champs `volatile` et de blocs `synchronized` partiels est le piège classique.

### 86. Qu'est-ce que le double-checked locking et pourquoi nécessite-t-il `volatile` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Un singleton paresseux qui vérifie `instance == null` avant et après avoir pris le verrou pour éviter de synchroniser à chaque accès. Sans `volatile`, la réorganisation des instructions peut publier une référence vers un objet non encore construit. Alternatives plus simples : initialisation statique, holder idiom (classe interne), ou `enum`.

### 87. Qu'est-ce que `ScheduledExecutorService` et quelle différence entre `scheduleAtFixedRate` et `scheduleWithFixedDelay` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Un executor planifiant des tâches différées ou périodiques. `scheduleAtFixedRate` déclenche à intervalle fixe depuis le début de chaque exécution (rattrape le retard, exécutions consécutives si la tâche est lente) ; `scheduleWithFixedDelay` attend le délai après la fin de chaque exécution. Une exception non capturée arrête silencieusement la planification : toujours envelopper dans un try/catch.

### 88. Comment utiliser les virtual threads avec `ExecutorService` et quels changements dans le code existant ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** `Executors.newVirtualThreadPerTaskExecutor()` crée un thread virtuel par tâche, sans pool. Le code bloquant classique (JDBC, HTTP) fonctionne tel quel. Précautions : éviter `synchronized` autour d'I/O longs (pinning, corrigé en Java 24), limiter les ressources avec des `Semaphore` plutôt que par la taille du pool, et ne pas mettre en cache d'objets coûteux dans des `ThreadLocal` (préférer `ScopedValue`).

### 89. Qu'est-ce que `ScopedValue` ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Une alternative à `ThreadLocal` (Java 21 preview, finalisée en Java 25) : une valeur immuable liée à une portée d'exécution (`ScopedValue.where(USER, u).run(() -> ...)`), automatiquement visible dans les threads enfants de la concurrence structurée, sans coût de copie ni risque de fuite avec les virtual threads. Idéale pour le contexte de requête (utilisateur, trace id).

### 90. Comment tester du code concurrent ?
`🟠 Intermédiaire` · Sujet : **Multithreading**

**Réponse :** Difficile car non déterministe : utiliser des `CountDownLatch` pour forcer des entrelacements, répéter les tests, `ExecutorService` avec beaucoup de tâches pour provoquer la contention, des outils spécialisés (jcstress pour le JMM, ThreadSanitizer via Lincheck), et privilégier une conception qui isole la logique concurrente (petits composants testables) du métier.

### 91. Comment mesurer correctement les performances Java (JMH) ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Java Microbenchmark Harness gère les pièges des benchmarks JVM : warm-up (JIT), élimination de code mort (`Blackhole`), constant folding, plusieurs forks pour l'isolation, modes (throughput, temps moyen, percentiles). Un `System.nanoTime()` autour d'une boucle donne des résultats faux. Benchmarker le cas réel avec des données réalistes, et interpréter les erreurs statistiques.

### 92. Quels sont les principaux collecteurs de déchets et comment choisir ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Serial (petits heaps, conteneurs mono-cœur), Parallel (débit maximal, pauses acceptables : batch), G1 (défaut, équilibre débit/latence, régions), ZGC (pauses sub-milliseconde, gros heaps, générationnel depuis Java 21), Shenandoah (similaire, Red Hat). Choisir selon l'objectif latence vs débit, la taille du heap et le CPU disponible, puis valider avec les logs GC (`-Xlog:gc*`).

### 93. Comment lire et interpréter les logs GC ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Activer `-Xlog:gc*:file=gc.log`. Observer la fréquence et la durée des pauses (young vs full), l'occupation avant/après collecte (une occupation qui remonte toujours plus haut après full GC indique une fuite), le temps total passé en GC (> 5-10 % est un problème), et les promotions prématurées. Outils : GCViewer, GCEasy, JFR.

### 94. Quels paramètres JVM de mémoire faut-il connaître ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** `-Xms`/`-Xmx` (heap min/max), `-XX:MaxRAMPercentage` (préféré en conteneur), `-XX:MaxMetaspaceSize`, `-Xss` (taille de pile par thread), `-XX:+HeapDumpOnOutOfMemoryError`, `-XX:MaxDirectMemorySize`. La mémoire totale d'un processus = heap + metaspace + piles + code cache + mémoire native (buffers, GC) : prévoir 25-50 % au-delà de `-Xmx` dans les limites Kubernetes.

### 95. Qu'est-ce que Java Flight Recorder (JFR) et JDK Mission Control ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** JFR est un profileur intégré à la JVM, à très faible surcoût (< 2 %), enregistrant événements GC, allocations, verrous, I/O, exceptions, échantillonnage CPU, activable en production (`-XX:StartFlightRecording` ou `jcmd JFR.start`). JMC visualise les enregistrements. C'est le premier outil à utiliser pour un problème de performance en production.

### 96. Comment optimiser les allocations et réduire la pression sur le GC ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Éviter les objets temporaires dans les boucles chaudes (boxing, `String` concaténées, streams sur de petites collections), réutiliser les buffers, préférer les primitives et tableaux, dimensionner les collections (`new ArrayList<>(n)`), utiliser `StringBuilder`. Mais mesurer d'abord : l'escape analysis du JIT élimine beaucoup d'allocations, et la lisibilité prime hors des chemins critiques.

### 97. Quel est le coût réel des exceptions et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Créer une exception capture la pile (`fillInStackTrace`), coûteux (microsecondes) surtout avec des piles profondes ; les lever pour le contrôle de flux normal (parsing, validation en masse) dégrade les performances. Alternatives : retours `Optional`/résultats, validation préalable, ou exceptions sans trace (`super(msg, null, false, false)`) pour les cas fréquents et attendus.

### 98. Comment optimiser les accès aux bases de données depuis Java ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** Éviter le N+1 (fetch join, `@EntityGraph`, batch fetching), paginer, sélectionner uniquement les colonnes utiles (projections, DTO), batcher les insertions (`hibernate.jdbc.batch_size`, `rewriteBatchedStatements`), utiliser des requêtes préparées, dimensionner le pool HikariCP (formule cœurs × 2 + disques), et surveiller les requêtes lentes avec les logs de la base et les métriques du pool.

### 99. Qu'est-ce que Class Data Sharing (CDS/AppCDS) et comment accélérer le démarrage ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** CDS archive les classes chargées dans un fichier mappé en mémoire partagé entre JVM, réduisant le temps de démarrage et la mémoire. AppCDS l'étend aux classes applicatives (`-XX:ArchiveClassesAtExit`, Spring Boot 3.3+ le supporte via des images Docker en couches). Autres leviers : `-XX:TieredStopAtLevel=1` en développement, initialisation paresseuse, Project Leyden, GraalVM Native Image.

### 100. Comment profiler une application Java en production sans la perturber ?
`🟠 Intermédiaire` · Sujet : **Optimisation Java**

**Réponse :** JFR en continu avec enregistrement circulaire, async-profiler (échantillonnage précis, sans biais de safepoint, flame graphs CPU/allocations/verrous), `jcmd` pour thread dumps et diagnostics ponctuels, métriques Micrometer exposées à Prometheus (GC, pools, latences). Éviter les profileurs par instrumentation en production. Corréler les flame graphs avec les traces distribuées pour cibler le bon service.
