# ☕ Java & JVM

> Java 8-21, Virtual Threads, GC, JIT, concurrency, memory leaks, thread dumps

**253 questions**

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

### 101. Qu'est-ce que la JVM, le JDK et le JRE ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** JVM : la machine virtuelle qui exécute le bytecode (classes chargées, JIT, GC). JRE : JVM + bibliothèques standard pour exécuter des programmes (plus distribué séparément depuis Java 11 ; on crée un runtime avec `jlink`). JDK : JRE + outils de développement (`javac`, `jar`, `jshell`, `jcmd`, `jfr`). Distributions : Temurin, Corretto, Zulu, Oracle, GraalVM.

### 102. Quel est le cycle de vie d'une classe dans la JVM (chargement, liaison, initialisation) ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** Chargement par un class loader (bootstrap, platform, application, hiérarchie parent-first), liaison (vérification du bytecode, préparation des champs statiques, résolution des références), initialisation (blocs `static`, exécutée paresseusement au premier usage actif). Comprendre l'ordre explique les `NoClassDefFoundError`, `ExceptionInInitializerError` et le holder idiom pour les singletons.

### 103. Différence entre `String`, `StringBuilder` et comment `String` est-elle stockée ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** `String` est immuable (sûre, partageable, hashCode mis en cache, pool de littéraux) ; depuis Java 9, les chaînes Latin-1 sont stockées en `byte[]` compact. `StringBuilder` est mutable pour les concaténations en boucle. La concaténation `a + b` est compilée via `invokedynamic` (`StringConcatFactory`) et est efficace pour une expression unique.

### 104. Que sont les génériques et l'effacement de type (type erasure) ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** Les génériques apportent la sûreté de type à la compilation (`List<String>`). À l'exécution, le type paramétré est effacé (`List`), d'où : pas de `new T()`, pas de `T[]`, pas d'`instanceof List<String>`, et des avertissements « unchecked ». Les jokers `? extends T` (lecture, covariant) et `? super T` (écriture, contravariant) suivent la règle PECS (Producer Extends, Consumer Super).

### 105. Différence entre surcharge (overloading) et redéfinition (overriding) ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** Surcharge : même nom, paramètres différents, résolue à la compilation selon les types statiques des arguments. Redéfinition : même signature dans une sous-classe, résolue à l'exécution (polymorphisme) ; `@Override` protège contre les fautes de frappe ; contraintes : visibilité non réduite, type de retour covariant, exceptions checked non élargies. Les méthodes `static`, `private` et `final` ne se redéfinissent pas.

### 106. Qu'est-ce que `final`, `finally` et `finalize` ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** `final` : variable non réassignable, méthode non redéfinissable, classe non héritable. `finally` : bloc exécuté après `try`/`catch` (nettoyage), remplacé le plus souvent par try-with-resources. `finalize()` : méthode appelée avant la collecte d'un objet, dépréciée pour suppression (imprévisible, coûteuse) ; utiliser `Cleaner` ou `AutoCloseable`.

### 107. Comment fonctionne try-with-resources ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** Toute ressource `AutoCloseable` déclarée dans `try (var in = ...)` est fermée automatiquement en ordre inverse, même en cas d'exception ; les exceptions de fermeture sont attachées en « suppressed ». Depuis Java 9, on peut utiliser une variable effectivement finale existante. Il élimine les fuites de fichiers, connexions et sockets.

### 108. Différence entre `throw` et `throws`, et comment créer une exception personnalisée ?
`🟢 Débutant` · Sujet : **Java**

**Réponse :** `throw` lève une exception ; `throws` déclare qu'une méthode peut en propager une (obligatoire pour les checked). Exception personnalisée : étendre `RuntimeException` (unchecked, recommandé pour les erreurs métier), fournir message et cause (chaînage), éventuellement un code d'erreur ; ne pas multiplier les hiérarchies, et documenter quand elle est levée.

### 109. Qu'est-ce que le chaînage d'exceptions et pourquoi ne jamais perdre la cause ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `new ServiceException("Paiement refusé", cause)` conserve la trace d'origine (`getCause()`, affichée « Caused by »). Avaler une exception (`catch (Exception e) {}`) ou relancer sans la cause supprime l'information de diagnostic. Attraper précisément, journaliser une seule fois au bon niveau, et convertir les exceptions techniques en exceptions métier à la frontière des couches.

### 110. Que sont les classes imbriquées, internes, anonymes et locales, et leurs différences ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Statique imbriquée : sans référence à l'instance externe (préférée). Interne (non statique) : capture `Outer.this`, peut provoquer des fuites mémoire si elle survit à l'objet externe. Locale : définie dans une méthode. Anonyme : implémentation en ligne, remplacée par les lambdas pour les interfaces fonctionnelles. Les records et enums imbriqués sont implicitement statiques.

### 111. Qu'est-ce qu'un `enum` en Java et quelles fonctionnalités avancées offre-t-il ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Une classe avec un nombre fixe d'instances : champs, constructeurs, méthodes, implémentation d'interfaces, méthodes abstraites par constante (stratégie), `EnumMap`/`EnumSet` très performants, `values()`, `valueOf`, `switch` exhaustif avec pattern matching. Un enum est thread-safe et sérialisable par nom ; ne pas dépendre de `ordinal()` pour la persistance.

### 112. Comment fonctionne le pattern matching pour `instanceof` et `switch` (Java 16-21) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `if (obj instanceof String s && s.length() > 3)` déclare et teste en une fois. `switch` accepte des patterns de type, des record patterns déconstruisant (`case Point(int x, int y)`), des gardes `when`, `null`, et impose l'exhaustivité sur les sealed types, sans `default` nécessaire : le compilateur signale les cas manquants lors d'une évolution du modèle.

### 113. Comment combiner `sealed`, `record` et `switch` pour modéliser un domaine ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `sealed interface Payment permits Card, Transfer, Cash` avec des records immuables pour chaque variante ; un `switch` exhaustif traite chaque cas de façon typée (somme de types algébriques). Cela remplace les hiérarchies avec `instanceof` en cascade et le pattern Visitor, rend les états illégaux non représentables et sécurise les évolutions.

### 114. Que sont les text blocks, `var`, et les switch expressions ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `var` (Java 10) : inférence de type local, lisibilité quand le type est évident. Text blocks (Java 15) : chaînes multi-lignes `"""` avec gestion de l'indentation (JSON, SQL). Switch expressions (Java 14) : `int n = switch (day) { case MON, TUE -> 1; default -> { yield 0; } };` sans fall-through ni `break`.

### 115. Qu'est-ce que le système de modules (JPMS) et est-il obligatoire ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `module-info.java` déclare `requires`, `exports`, `opens`, `provides/uses` pour encapsuler fortement les packages et expliciter les dépendances. Il n'est pas obligatoire (classpath classique fonctionne), mais il permet `jlink` (runtime minimal) et une meilleure encapsulation. Les frameworks à réflexion nécessitent `opens` ; beaucoup d'applications restent sur le classpath avec des jars « automatiques ».

### 116. Qu'est-ce que la réflexion, ses usages et ses coûts ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Class`, `Method`, `Field` permettent d'inspecter et invoquer dynamiquement (frameworks DI, sérialisation, tests). Coûts : plus lent que l'appel direct (mitigé par `MethodHandle`), contourne l'encapsulation (`setAccessible`, bloqué par les modules), incompatible avec Native Image sans hints. Alternatives : génération de code à la compilation (annotation processors, records), `MethodHandles`, ou la configuration explicite.

### 117. Comment fonctionne la sérialisation Java native et pourquoi l'éviter ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Serializable` + `ObjectOutputStream` écrit le graphe d'objets en binaire propriétaire. Problèmes : failles de désérialisation (exécution de code via gadget chains), fragilité aux changements de classe (`serialVersionUID`), non interopérable. Préférer JSON/Protobuf/Avro ; si nécessaire, filtrer avec `ObjectInputFilter` (JEP 290). Les records sont sérialisables de façon plus sûre (constructeur canonique).

### 118. Que sont `equals`/`hashCode`/`compareTo` cohérents et pourquoi les records les génèrent-ils ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `equals` doit être réflexif, symétrique, transitif, cohérent avec `hashCode` (objets égaux → même hash) ; `compareTo` idéalement cohérent avec `equals`. Les erreurs cassent `HashMap`, `HashSet`, `TreeMap`. Les records génèrent ces méthodes sur tous les composants ; pour les entités JPA, baser sur un identifiant métier ou l'id une fois assigné, jamais sur des collections lazy.

### 119. Comment fonctionnent les collections immuables (`List.of`, `Collections.unmodifiableList`, `Stream.toList`) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `List.of`/`Map.of` (Java 9) créent des collections réellement immuables, compactes, refusant `null` et les modifications (`UnsupportedOperationException`). `Collections.unmodifiableList` est une vue en lecture seule sur une liste qui peut encore changer par ailleurs. `List.copyOf` et `Stream.toList()` copient en immuable. Retourner des collections immuables protège les invariants des objets.

### 120. Qu'est-ce que le fail-fast et `ConcurrentModificationException` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Les itérateurs des collections standard détectent une modification structurelle pendant l'itération (compteur `modCount`) et lèvent `ConcurrentModificationException`, même en mono-thread (supprimer dans un `for-each`). Solutions : `iterator.remove()`, `removeIf`, itérer sur une copie, ou collections concurrentes (weakly consistent) en multi-thread.

### 121. Comment choisir entre `HashMap`, `ConcurrentHashMap`, `TreeMap`, `EnumMap`, `WeakHashMap` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `HashMap` : usage général mono-thread, O(1). `ConcurrentHashMap` : partagé entre threads, opérations atomiques `compute`/`merge`. `TreeMap` : ordre trié, requêtes par plage (`headMap`, `ceilingKey`), O(log n). `EnumMap` : clés enum, tableau interne très rapide. `WeakHashMap` : clés référencées faiblement, caches de métadonnées libérables par le GC. `LinkedHashMap` avec `removeEldestEntry` : LRU simple.

### 122. Que sont les références faibles, douces et fantômes ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `SoftReference` : libérée seulement sous pression mémoire (caches). `WeakReference` : libérée à la prochaine collecte dès qu'aucune référence forte n'existe (`WeakHashMap`, listeners). `PhantomReference` + `ReferenceQueue` : notification après finalisation pour nettoyage de ressources natives (`Cleaner`). En pratique, préférer Caffeine aux caches maison à références douces.

### 123. Comment fonctionne l'API `java.nio.file` (Files, Path) et pourquoi préférer NIO à `java.io.File` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Path`/`Files` offrent des opérations atomiques et explicites (`Files.readString`, `writeString`, `walk`, `lines` en stream, `createTempFile`, `move` avec `ATOMIC_MOVE`), des exceptions précises (`NoSuchFileException`), les attributs et les liens symboliques, et `WatchService`. `File` renvoie souvent `false` sans expliquer l'échec. Toujours fermer les streams de `Files.lines`/`walk` (try-with-resources).

### 124. Qu'est-ce que le `HttpClient` standard (Java 11+) et comment l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Client HTTP/1.1 et HTTP/2 intégré, synchrone (`send`) ou asynchrone (`sendAsync` → `CompletableFuture`), avec `BodyHandlers` (string, file, stream), timeouts, redirections, authentification, WebSocket. Un client par application (réutilisation des connexions), timeouts obligatoires, et il sert de connecteur à `RestClient` Spring. Il remplace `HttpURLConnection`.

### 125. Comment fonctionnent les annotations et les annotation processors ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Une annotation est une métadonnée (`@Retention` SOURCE/CLASS/RUNTIME, `@Target`) lue par réflexion (frameworks) ou par un processor à la compilation (`javax.annotation.processing`) qui génère du code : Lombok (modifie l'AST, controversé), MapStruct (mappers), Immutables, Dagger, les Q-classes Querydsl, la métadonnée Spring Boot. La génération à la compilation évite le coût de la réflexion à l'exécution.

### 126. Qu'est-ce que `Optional` dans la conception d'API et les alternatives pour les erreurs ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Optional` exprime l'absence, pas l'échec. Pour les résultats pouvant échouer avec une raison, utiliser des exceptions (cas exceptionnels), un type résultat (`sealed interface Result permits Ok, Err`), ou Vavr `Either`/`Try`. Une API cohérente : `Optional` pour les recherches par identifiant, exceptions pour les violations d'invariants, `Result` pour les validations métier multiples.

### 127. Comment concevoir une classe immuable et pourquoi ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Champs `private final`, pas de setters, initialisation complète dans le constructeur avec validation, copies défensives des entrées/sorties mutables (dates, collections → `List.copyOf`), classe `final` ou record. Bénéfices : thread-safety gratuite, simplicité de raisonnement, clés de map sûres, partage sans copie. Les records sont la forme idiomatique depuis Java 16.

### 128. Qu'est-ce que le principe « composition over inheritance » en Java ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Privilégier la délégation à des objets composants plutôt que l'héritage, qui couple fortement, expose les détails de la superclasse (fragile base class) et n'est pas multiple. Utiliser des interfaces (avec méthodes `default` si besoin), des records composant d'autres records, le pattern Decorator. Réserver l'héritage aux vraies relations « est-un » avec classes conçues pour l'extension (ou `sealed`).

### 129. Comment fonctionne `Comparable` vs `Comparator` et les pièges du tri ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Comparable` définit l'ordre naturel dans la classe (une seule façon) ; `Comparator` définit des ordres externes multiples. Pièges : `compareTo` incohérent avec `equals` (TreeSet supprime des éléments), soustraction d'entiers pour comparer (overflow : utiliser `Integer.compare`), non-transitivité, `null` non géré (`Comparator.nullsLast`). `List.sort` est stable (TimSort).

### 130. Comment fonctionne le boxing et quels pièges avec `Integer` ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Integer a = 127, b = 127; a == b` est vrai (cache -128..127) mais faux pour 128 : toujours `equals` ou `intValue`. `Integer` nul déballé → `NullPointerException` ; boxing dans les boucles alloue et ralentit (préférer `int`, `IntStream`, `mapToInt`). `Long` et `Integer` ne sont pas égaux même pour la même valeur numérique.

### 131. Qu'est-ce que `BigDecimal` et pourquoi ne jamais utiliser `double` pour l'argent ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `double` est binaire flottant : 0.1 + 0.2 ≠ 0.3, arrondis cumulatifs. `BigDecimal` représente exactement les décimaux avec échelle et arrondi contrôlés (`setScale(2, RoundingMode.HALF_EVEN)`), à construire depuis une chaîne ou `valueOf` (jamais `new BigDecimal(0.1)`), comparé avec `compareTo` (pas `equals`, qui tient compte de l'échelle). Stocker en `NUMERIC`/`DECIMAL` en base.

### 132. Comment gérer les nombres aléatoires et la cryptographie de base en Java ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `ThreadLocalRandom`/`RandomGenerator` (Java 17, algorithmes sélectionnables) pour le non sécurisé ; `SecureRandom` pour les jetons, sels, identifiants sensibles. Hachage de mots de passe via Argon2/bcrypt (bibliothèques), `MessageDigest` (SHA-256) pour l'intégrité, `Mac` (HMAC), `Cipher` AES-GCM avec IV unique pour le chiffrement, `KeyStore` pour les clés. Ne jamais inventer sa cryptographie.

### 133. Comment lire et manipuler du JSON en Java (Jackson, Gson, JSON-B) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Jackson (standard Spring) : `ObjectMapper` unique, `readValue`/`writeValueAsString`, annotations `@JsonProperty`, `@JsonIgnore`, `@JsonCreator` pour les records/immuables, modules `JavaTimeModule`, `TypeReference` pour les génériques, streaming `JsonParser` pour les gros documents, `JsonNode` pour l'arbre. Jackson 3 (2025) change le package (`tools.jackson`) et les défauts (dates ISO).

### 134. Qu'est-ce que Lombok, ses avantages et ses inconvénients ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Il génère getters, setters, constructeurs, `equals`/`hashCode`, builders, logs via annotations. Avantages : moins de code. Inconvénients : magie sur l'AST (dépendance à la version du compilateur), `@Data` sur des entités JPA (equals/hashCode dangereux), `@Builder` masquant les invariants, lisibilité pour les nouveaux. Depuis les records et `var`, son intérêt diminue ; beaucoup d'équipes le limitent à `@Builder`/`@Slf4j` ou l'abandonnent.

### 135. Comment fonctionne la journalisation en Java (SLF4J, Logback, Log4j2) et les bonnes pratiques ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** SLF4J est la façade ; Logback (défaut Spring Boot) ou Log4j2 l'implémentation. Bonnes pratiques : paramètres `{}` (pas de concaténation), niveaux cohérents, logs structurés JSON en production, MDC pour le contexte (traceId, tenant), pas de données sensibles, appenders asynchrones, exclure les doubles bindings. Éviter `System.out` et `e.printStackTrace()`.

### 136. Comment écrire de bons tests unitaires en Java (JUnit 5, Mockito, AssertJ) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** JUnit 5 : `@Test`, `@ParameterizedTest` (`@CsvSource`, `@MethodSource`), `@Nested` pour structurer, `@DisplayName`, extensions. Mockito : mocks des dépendances (`when`/`verify`), `@ExtendWith(MockitoExtension.class)`, ne pas mocker les types qu'on ne possède pas ni les valeurs. AssertJ : assertions fluides et lisibles. Un test = un comportement, nommage explicite, données minimales, pas de logique dans les tests.

### 137. Qu'est-ce que le mutation testing (PIT) et que révèle-t-il ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** PIT modifie le code (inversion de conditions, suppression d'appels, changement de constantes) et vérifie qu'un test échoue ; un mutant survivant indique un test insuffisant malgré une couverture élevée. Il mesure la qualité réelle des tests, au prix d'un temps d'exécution long : à lancer sur les modules critiques ou en nightly.

### 138. Comment fonctionnent Maven et Gradle et quelles différences ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Maven : XML déclaratif, cycle de vie fixe (validate → compile → test → package → verify → install → deploy), conventions fortes, plugins ; simple et prévisible. Gradle : DSL Kotlin/Groovy, graphe de tâches, builds incrémentaux et cache, très rapide sur les gros projets multi-modules, plus de flexibilité (et de complexité). Les deux gèrent les BOM, profils/variants et la reproductibilité (versions fixées, lockfiles).

### 139. Comment gérer les conflits de dépendances (dependency hell) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Maven résout par « nearest wins » (la version la plus proche dans l'arbre) ; `mvn dependency:tree` et `-Dverbose` montrent les évictions ; imposer via `dependencyManagement`/BOM, exclure les transitives problématiques, `maven-enforcer-plugin` (`dependencyConvergence`, bannir les doublons de logging). Gradle choisit la version la plus haute et offre `constraints`, `resolutionStrategy` et les lockfiles.

### 140. Qu'est-ce que la compatibilité binaire vs source, et comment faire évoluer une bibliothèque ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Compatibilité source : le code client recompile ; binaire : le code compilé continue de fonctionner sans recompiler (une signature changée, une constante inlinée ou une méthode d'interface ajoutée sans `default` peuvent casser). Outils : japicmp/revapi en CI, SemVer, dépréciation avec `@Deprecated(forRemoval, since)` sur au moins une version majeure avant suppression.

### 141. Comment fonctionne `java.util.concurrent.Flow` et l'API Reactive Streams ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Flow.Publisher`, `Subscriber`, `Subscription`, `Processor` (Java 9) définissent le contrat Reactive Streams avec backpressure (`request(n)`) sans implémentation complète (hors `SubmissionPublisher`). Reactor, RxJava, Mutiny et le `HttpClient` (`BodyHandlers.ofPublisher`) l'implémentent, garantissant l'interopérabilité. Utile pour comprendre WebFlux et le streaming.

### 142. Qu'est-ce que le Foreign Function & Memory API (finalisé en Java 22) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Un remplacement de JNI pour appeler du code natif (`Linker`, `SymbolLookup`, `FunctionDescriptor`) et manipuler de la mémoire hors heap (`Arena`, `MemorySegment`, `MemoryLayout`) de manière sûre, avec libération déterministe. `jextract` génère les bindings depuis des headers C. Utile pour les bibliothèques natives (compression, ML) sans écrire de C.

### 143. Que sont les Vector API et les autres APIs incubatrices/preview récentes ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Vector API (incubateur) : calculs SIMD explicites portables. Preview/récents : Structured Concurrency et Scoped Values (finalisés Java 25), Stream Gatherers (`Stream.gather`, Java 24, opérations intermédiaires personnalisées), Primitive Types in Patterns, Flexible Constructor Bodies (instructions avant `super()`), Module Import Declarations, Compact Source Files (`void main()`). Suivre les JEP et ne pas déployer de preview en production.

### 144. Qu'est-ce que le cycle de release Java et les versions LTS ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Une version tous les six mois (mars, septembre), avec LTS tous les deux ans : 8, 11, 17, 21, 25 (septembre 2025). Les entreprises ciblent les LTS ; les versions intermédiaires servent à tester les nouveautés. Vérifier le support des frameworks (Spring Boot 3 : 17+, Boot 4 : 17+/21 recommandé) et des distributions (Temurin, Corretto) pour les mises à jour de sécurité.

### 145. Comment migrer une application de Java 8 vers 17/21 ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Mettre à jour le build et les plugins, remplacer les APIs supprimées (JAXB, JAX-WS, CORBA → dépendances externes), gérer l'encapsulation forte des internes (`--add-opens` temporaire, puis corriger), mettre à jour les bibliothèques (Lombok, ASM, Mockito), vérifier les changements de GC par défaut (G1) et de `Locale`/dates (CLDR), tester avec `jdeps`/`jdeprscan`, puis adopter progressivement records, `var`, switch, virtual threads.

### 146. Qu'est-ce que `jlink`, `jpackage` et comment créer un runtime minimal ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `jlink` assemble un runtime contenant uniquement les modules nécessaires (`jdeps` pour les lister), réduisant la taille de l'image Docker et la surface d'attaque. `jpackage` crée des installeurs natifs (msi, dmg, deb) avec runtime embarqué pour les applications de bureau. Les images Docker « distroless »/`jlink` sont une alternative à Native Image quand le démarrage n'est pas critique.

### 147. Comment écrire un `main` moderne et des scripts Java (JEP 330, 445, 458) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `java Hello.java` exécute un fichier source directement (Java 11) ; Java 22+ permet plusieurs fichiers et Java 25 finalise les « compact source files » : `void main() { IO.println("Hi"); }` sans classe ni `public static`. Avec `jshell` pour l'exploration. Pratique pour scripts, outils et enseignement, sans passer par Maven.

### 148. Quelles sont les vulnérabilités Java courantes et comment les prévenir ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Désérialisation non sûre, injection (SQL, commande, LDAP, expression), XXE dans les parseurs XML (désactiver les entités externes), traversée de chemin, `Random` pour des secrets, dépendances vulnérables (Log4Shell), fuites via `toString` dans les logs, `Runtime.exec` avec entrées utilisateur. Outils : Dependency-Check/Snyk, SpotBugs avec find-sec-bugs, SonarQube, revues ciblées.

### 149. Comment gérer proprement la fermeture des ressources et l'arrêt d'une application (shutdown hooks) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** `Runtime.getRuntime().addShutdownHook(thread)` exécute du code à SIGTERM/`System.exit` (fermeture des pools, flush des logs, désinscription d'un registre) ; garder les hooks rapides et indépendants, sans dépendre d'autres hooks. Les frameworks (Spring) gèrent déjà la fermeture ordonnée des beans ; en Kubernetes, prévoir `terminationGracePeriodSeconds` en conséquence.

### 150. Comment lire et interpréter une stack trace Java efficacement ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Lire de haut en bas la première exception (type, message), repérer la première ligne appartenant à votre code (paquet de l'application) après les frames de frameworks, puis descendre vers les « Caused by » (la cause racine est la dernière). Les lignes « ... 42 more » sont des frames communes omises. Les exceptions dans des lambdas/streams montrent des frames synthétiques ; `-XX:-OmitStackTraceInFastThrow` évite les traces vides sur les exceptions répétées.

### 151. Quelles bonnes pratiques pour concevoir une API publique en Java (bibliothèque) ?
`🟠 Intermédiaire` · Sujet : **Java**

**Réponse :** Minimiser la surface (packages internes non exportés, `sealed`), types immuables, `Optional` en retour uniquement, éviter les booléens en paramètres (enums), exceptions documentées, pas de dépendances lourdes transitives, `@Deprecated` avec chemin de migration, Javadoc avec exemples, compatibilité vérifiée par japicmp, tests de non-régression et SemVer. Ne pas exposer de types de bibliothèques tierces dans les signatures.

### 152. Comment fonctionne `HashMap` en interne (buckets, hash, treeification, redimensionnement) ?
`🟢 Débutant` · Sujet : **Collections**

**Réponse :** Un tableau de buckets indexé par `hash(key) & (n-1)` ; les collisions forment une liste chaînée, convertie en arbre rouge-noir au-delà de 8 entrées (Java 8) pour garantir O(log n) en cas de mauvais `hashCode` ; redimensionnement ×2 quand le nombre d'entrées dépasse `capacité × loadFactor (0,75)`, avec redistribution. D'où l'importance d'un `hashCode` bien réparti et d'une capacité initiale adaptée.

### 153. Différence entre `ArrayList`, `LinkedList`, `ArrayDeque` et quand utiliser chacun ?
`🟢 Débutant` · Sujet : **Collections**

**Réponse :** `ArrayList` : accès indexé O(1), ajout en fin amorti O(1), insertion au milieu O(n), cache-friendly : le choix par défaut. `LinkedList` : insertions/suppressions O(1) via itérateur mais surcoût mémoire et accès O(n) : quasiment jamais le bon choix. `ArrayDeque` : pile et file à double extrémité très rapide, préférable à `Stack` et `LinkedList` pour LIFO/FIFO.

### 154. Comment fonctionnent `TreeMap`/`TreeSet` et les vues `NavigableMap` ?
`🟢 Débutant` · Sujet : **Collections**

**Réponse :** Arbre rouge-noir trié par ordre naturel ou `Comparator` (O(log n)), avec des vues de plage (`subMap`, `headMap`, `tailMap`), navigation (`floorKey`, `ceilingKey`, `firstEntry`, `pollFirst`), et itération ordonnée. Utile pour les intervalles, les planifications, les top-N évolutifs. Le comparateur doit être cohérent avec `equals` sinon des éléments « égaux » sont fusionnés.

### 155. Qu'est-ce que `PriorityQueue` et comment implémenter un top-K ou un scheduler simple ?
`🟢 Débutant` · Sujet : **Collections**

**Réponse :** Un tas binaire (min-heap par défaut) avec `offer`/`poll` en O(log n) et `peek` en O(1), sans ordre d'itération garanti. Top-K : garder une `PriorityQueue` de taille K (min-heap) et rejeter le minimum quand on dépasse. Scheduler : file ordonnée par échéance ; `DelayQueue`/`ScheduledExecutorService` pour la version concurrente.

### 156. Différence entre `Iterable`, `Iterator`, `ListIterator` et `Spliterator`, et comment rendre une classe itérable ?
`🟢 Débutant` · Sujet : **Collections**

**Réponse :** `Iterable<T>` expose `iterator()` (utilisable dans `for-each`, `forEach`, `spliterator()` par défaut) ; `Iterator` parcourt (`hasNext`, `next`, `remove` optionnel) ; `ListIterator` permet le parcours bidirectionnel et la modification ; `Spliterator` découpe pour les streams parallèles. Implémenter `Iterable` avec un itérateur paresseux évite de matérialiser une collection (pagination, génération).

### 157. Comment fonctionnent les collections synchronisées, concurrentes et « weakly consistent » ?
`🟠 Intermédiaire` · Sujet : **Collections**

**Réponse :** `Collections.synchronizedX` verrouille chaque opération (itération à synchroniser manuellement, `ConcurrentModificationException` possible). Les collections `java.util.concurrent` (`ConcurrentHashMap`, `CopyOnWriteArrayList`, `ConcurrentLinkedQueue`) offrent des itérateurs weakly consistent : pas d'exception, reflètent un état approximatif. `ConcurrentHashMap.size()` et les vues sont des estimations sous forte concurrence.

### 158. Comment fonctionnent `Arrays.asList`, `List.of`, `Collections.emptyList` et leurs pièges ?
`🟠 Intermédiaire` · Sujet : **Collections**

**Réponse :** `Arrays.asList` retourne une vue de taille fixe sur le tableau (`set` OK, `add` interdit, modifications reflétées dans le tableau, un `int[]` donne une liste d'un seul élément). `List.of` : immuable, refuse `null`. `Collections.emptyList()` : singleton immuable. `new ArrayList<>(Arrays.asList(...))` pour une copie modifiable. Connaître ces sémantiques évite les `UnsupportedOperationException` en production.

### 159. Comment choisir la capacité initiale et éviter les redimensionnements coûteux ?
`🟠 Intermédiaire` · Sujet : **Collections**

**Réponse :** `new ArrayList<>(n)` et `HashMap.newHashMap(n)` (Java 19, calcule la capacité pour n entrées sans rehash ; sinon `n / 0.75 + 1`), `StringBuilder(n)`. Utile pour les collections construites en boucle à taille connue ; les collecteurs `toList()`/`toMap` gèrent leur croissance. Ne pas surdimensionner par défaut : mémoire gaspillée sur des millions de petites collections.

### 160. Quelles bibliothèques de collections tierces valent la peine (Guava, Eclipse Collections, Vavr) ?
`🟠 Intermédiaire` · Sujet : **Collections**

**Réponse :** Guava : `ImmutableList/Map`, `Multimap`, `Table`, `BiMap`, `Cache` (préférer Caffeine), utilitaires. Eclipse Collections : collections primitives (`IntList`, `LongIntMap`) très efficaces en mémoire, API riche. Vavr : collections persistantes (immuables avec partage structurel) et types fonctionnels (`Option`, `Try`, `Either`). À évaluer contre les APIs standard modernes (records, `List.of`, streams) avant d'ajouter une dépendance.

### 161. Comment implémenter un cache LRU/LFU en Java pur et pourquoi préférer Caffeine ?
`🟠 Intermédiaire` · Sujet : **Collections**

**Réponse :** LRU : `LinkedHashMap(capacity, 0.75f, true)` avec `removeEldestEntry` (accès-ordonné) ; thread-safe via synchronisation externe. LFU exige une structure plus complexe (compteurs + buckets). Caffeine offre W-TinyLFU (meilleur taux de hit), concurrence lock-free, expiration, poids, refresh asynchrone, statistiques et intégration Spring Cache : réimplémenter n'a de sens qu'en exercice d'entretien.

### 162. Comment écrire une méthode générique avec bornes multiples et jokers, et quelles limites ?
`🟠 Intermédiaire` · Sujet : **Generics**

**Réponse :** `<T extends Comparable<? super T> & Serializable> T max(Collection<? extends T> c)` : bornes multiples (une classe max, en premier), joker `? super T` pour accepter les comparateurs de supertypes. Limites : pas de bornes inférieures sur les paramètres de type (`T super X` interdit), pas de génériques primitifs (boxing, ou spécialisations `IntStream`), pas d'`instanceof` paramétré, tableaux génériques impossibles (`(T[]) new Object[n]` avec avertissement).

### 163. Qu'est-ce qu'un type récursif (`Enum<E extends Enum<E>>`, `Comparable<T>`) et le pattern « self-type » ?
`🟠 Intermédiaire` · Sujet : **Generics**

**Réponse :** `class Builder<B extends Builder<B>>` permet de retourner `B` (le sous-type concret) dans les méthodes chaînables d'une hiérarchie de builders (CRTP). `Enum<E extends Enum<E>>` garantit que `compareTo` ne compare que des constantes du même enum. Puissant mais verbeux ; les records et les builders générés (Lombok, Immutables) le rendent rarement nécessaire.

### 164. Comment fonctionne l'inférence de type (diamant, lambdas, `var`) et ses limites ?
`🟠 Intermédiaire` · Sujet : **Generics**

**Réponse :** Le compilateur infère les arguments de type depuis le contexte cible (`List<String> l = new ArrayList<>()`, `List.of()`, lambdas typées par l'interface attendue). Limites : classes anonymes avec diamant (Java 9+ OK), chaînes d'appels où le type cible est perdu (`Collections.emptyList().add(...)`), surcharges ambiguës avec lambdas (`submit(Runnable)` vs `submit(Callable)`), et `var` interdit sans initialiseur ou avec `null`/lambda.

### 165. Comment capturer un type générique à l'exécution (`TypeReference`, `ParameterizedType`, super type token) ?
`🟠 Intermédiaire` · Sujet : **Generics**

**Réponse :** Les types génériques des superclasses/champs/méthodes restent dans les métadonnées de classe : `new TypeReference<List<User>>(){}` (Jackson) crée une sous-classe anonyme dont `getGenericSuperclass()` expose `ParameterizedType`. Alternatives : passer `Class<T>` en paramètre, ou `Class<T>[]` ; Spring `ResolvableType`. Nécessaire pour la désérialisation de collections typées.

### 166. Qu'est-ce que le principe de substitution de Liskov et un exemple de violation en Java ?
`🟠 Intermédiaire` · Sujet : **OOP**

**Réponse :** Un sous-type doit pouvoir remplacer son supertype sans casser le programme (préconditions non renforcées, postconditions non affaiblies, invariants conservés). Violations classiques : `Square extends Rectangle` avec `setWidth` modifiant la hauteur, une sous-classe levant `UnsupportedOperationException` sur une méthode héritée (`Collections.unmodifiableList`), ou `equals` non symétrique entre classe et sous-classe (utiliser `getClass()` ou `sealed`).

### 167. Comment concevoir une hiérarchie extensible et sûre : `sealed` vs `abstract`, `final` par défaut, `protected` ?
`🟠 Intermédiaire` · Sujet : **OOP**

**Réponse :** Déclarer les classes `final` par défaut (ou `sealed` avec les sous-types connus) sauf conception explicite pour l'extension ; documenter les méthodes redéfinissables (`protected`, non appelées depuis le constructeur), privilégier les interfaces avec méthodes `default` pour l'évolution, et la composition pour la réutilisation. `sealed` + records donne des sommes de types exhaustives ; `abstract` reste pour le code partagé (template method).

### 168. Qu'est-ce que le pattern Template Method vs Strategy vs lambdas en Java moderne ?
`🟠 Intermédiaire` · Sujet : **OOP**

**Réponse :** Template Method : classe abstraite fixant l'algorithme et déléguant des étapes à des méthodes abstraites (héritage, rigide). Strategy : l'algorithme est injecté via une interface (composition, testable). En Java moderne, une `Function`/`BiFunction`/interface fonctionnelle passée en paramètre ou en `Map<Type, Strategy>` remplace la plupart des Template Methods, et les enums avec méthodes abstraites offrent des stratégies fermées.

### 169. Comment gérer l'égalité et l'identité des entités et des value objects ?
`🟠 Intermédiaire` · Sujet : **OOP**

**Réponse :** Value objects (records) : égalité structurelle sur tous les champs, immuables, interchangeables. Entités : identité par identifiant (`equals` sur l'id une fois assigné, `hashCode` constant ou basé sur une clé métier stable pour rester valide dans les `HashSet` avant persistance). Ne jamais baser `equals` d'une entité sur des champs mutables ; et documenter le choix.

### 170. Qu'est-ce que le pattern Null Object, `Optional` et comment éliminer les `null` d'une API ?
`🟠 Intermédiaire` · Sujet : **OOP**

**Réponse :** Retourner des collections vides plutôt que `null`, `Optional` pour un résultat absent, des Null Objects (implémentation neutre : `NoOpLogger`) pour éviter les vérifications, valeurs par défaut explicites, `Objects.requireNonNull` en préconditions, annotations de nullabilité (JSpecify `@Nullable`, NullAway/Error Prone pour vérifier), et records avec validation dans le constructeur compact. Le `null` reste acceptable en interne, jamais dans un contrat public sans annotation.

### 171. Comment composer des fonctions et prédicats (`andThen`, `compose`, `Predicate.not`, currying) ?
`🟠 Intermédiaire` · Sujet : **Fonctionnel**

**Réponse :** `f.andThen(g)` (g après f), `f.compose(g)` (g avant f), `Predicate.and/or/negate` et `Predicate.not(String::isBlank)`, `Comparator.comparing().thenComparing()`, `UnaryOperator.identity()`. Currying par lambdas imbriquées (`Function<A, Function<B, C>>`) reste verbeux en Java ; les pipelines de fonctions clarifient les validations et transformations sans classes dédiées.

### 172. Qu'est-ce que la mémoïsation et comment l'implémenter en Java ?
`🟠 Intermédiaire` · Sujet : **Fonctionnel**

**Réponse :** Mettre en cache les résultats d'une fonction pure par argument : `ConcurrentHashMap.computeIfAbsent(arg, f)` (attention : `computeIfAbsent` récursif sur la même map lève une exception depuis Java 9), ou Caffeine `LoadingCache` avec taille/expiration, ou `Suppliers.memoize` (Guava) pour une valeur unique paresseuse. Pour la récursion (Fibonacci, programmation dynamique), passer par une map externe ou une itération.

### 173. Comment gérer les effets de bord et l'immuabilité dans un style fonctionnel en Java ?
`🟠 Intermédiaire` · Sujet : **Fonctionnel**

**Réponse :** Fonctions pures pour la logique (entrées → sorties, testables sans mock), effets (I/O, base) isolés aux frontières (« functional core, imperative shell »), données immuables (records, `List.copyOf`, `with`-ers), pas de mutation dans les streams (`forEach` avec état partagé), et retour de nouvelles valeurs plutôt que modification. Les `Result`/`Either` rendent les erreurs explicites sans exceptions pour le flux de contrôle.

### 174. Que sont les Stream Gatherers (Java 24) et quels problèmes résolvent-ils ?
`🟠 Intermédiaire` · Sujet : **Fonctionnel**

**Réponse :** `Stream.gather(Gatherer)` ajoute des opérations intermédiaires personnalisées avec état, ce que `map`/`filter`/`flatMap` ne permettaient pas : fenêtres (`Gatherers.windowFixed(3)`, `windowSliding`), `fold`, `scan` (préfixes cumulés), `mapConcurrent` (parallélisme borné sur virtual threads, ordre conservé), et gatherers maison (`Gatherer.ofSequential(initializer, integrator, finisher)`). Ils évitent de casser le pipeline pour des besoins comme « regrouper par paquets ».

### 175. Comment implémenter des opérations « batch par N » et « distinct par clé » sur des streams ?
`🟠 Intermédiaire` · Sujet : **Fonctionnel**

**Réponse :** Batch : `Gatherers.windowFixed(n)` (Java 24) ; avant : `IntStream.range(0, (size+n-1)/n).mapToObj(i -> list.subList(i*n, Math.min(size,(i+1)*n)))` sur une liste, ou un `Collector` personnalisé. Distinct par clé : `collect(toMap(keyFn, identity(), (a, b) -> a, LinkedHashMap::new)).values()` ou `filter` avec un `Set` concurrent (`ConcurrentHashMap.newKeySet()`) via `seen.add(key(x))` — acceptable si documenté, mais impur.

### 176. Comment écrire un `Collector` personnalisé ?
`🟠 Intermédiaire` · Sujet : **Fonctionnel**

**Réponse :** `Collector.of(supplier, accumulator, combiner, finisher, characteristics)` : par exemple un collecteur vers une `ImmutableList` Guava, une statistique métier (min/max/moyenne pondérée), ou une `String` tronquée. Les `characteristics` (`CONCURRENT`, `UNORDERED`, `IDENTITY_FINISH`) optimisent le parallélisme. `Collectors.teeing` et `collectingAndThen` couvrent souvent le besoin sans collecteur maison.

### 177. Comment concevoir une hiérarchie d'exceptions applicatives et une stratégie de gestion par couche ?
`🟠 Intermédiaire` · Sujet : **Exceptions**

**Réponse :** Une exception racine `AppException` (unchecked) avec code d'erreur et données structurées, des sous-types par catégorie (`NotFound`, `Conflict`, `ValidationFailed`, `ExternalServiceFailure`), les exceptions techniques (SQL, HTTP) traduites aux frontières (adaptateurs), la couche web les mappe en réponses (`ProblemDetail`), et un `catch-all` global pour l'inattendu (500 + log). Ne pas capturer là où on ne peut rien faire.

### 178. Qu'est-ce que `try`/`finally` avec `return` et les exceptions masquées (suppressed) ?
`🟠 Intermédiaire` · Sujet : **Exceptions**

**Réponse :** Un `return` ou `throw` dans `finally` écrase le résultat ou l'exception du `try` (à proscrire). Try-with-resources gère correctement : l'exception principale est conservée et celles de `close()` deviennent des `suppressed` (`getSuppressed()`) ; un `finally` manuel qui lève perd l'exception d'origine. Toujours logger les `suppressed` ou utiliser try-with-resources.

### 179. Comment gérer les exceptions dans les `CompletableFuture`, executors et streams parallèles ?
`🟠 Intermédiaire` · Sujet : **Exceptions**

**Réponse :** `CompletableFuture` : `exceptionally`, `handle`, `whenComplete` ; une exception est encapsulée en `CompletionException` (`getCause()`). `ExecutorService.submit` stocke l'exception dans le `Future` (`get()` lève `ExecutionException`), `execute` la propage à l'`UncaughtExceptionHandler`. Streams parallèles : la première exception interrompt et est relancée ; les autres tâches peuvent continuer brièvement. Toujours consommer les futures ou définir des handlers.

### 180. Qu'est-ce que `StackWalker` et comment obtenir le contexte d'appel sans coût prohibitif ?
`🟠 Intermédiaire` · Sujet : **Exceptions**

**Réponse :** `StackWalker.getInstance().walk(frames -> ...)` parcourt paresseusement la pile (Java 9) sans construire tout un `StackTraceElement[]`, avec option `RETAIN_CLASS_REFERENCE` pour obtenir la classe appelante. Utile pour les loggers, l'audit ou les frameworks ; bien plus efficace que `Thread.currentThread().getStackTrace()` ou `new Throwable()`.

### 181. Comment concevoir des messages d'erreur et des codes exploitables (i18n, support, sécurité) ?
`🟠 Intermédiaire` · Sujet : **Exceptions**

**Réponse :** Message technique précis dans les logs (avec contexte : identifiants, paramètres non sensibles), message utilisateur localisé et générique dans la réponse, code d'erreur stable (`ORDER_NOT_FOUND`) documenté, identifiant de corrélation pour le support, pas de détails d'implémentation ni de données sensibles exposés, et niveaux de log adaptés (les erreurs attendues du client en `WARN` ou `INFO`, pas `ERROR`).

### 182. Différence entre I/O bloquant, NIO (non-blocking) et asynchrone (AIO) en Java ?
`🟠 Intermédiaire` · Sujet : **I/O**

**Réponse :** `java.io` : un thread par connexion bloqué sur `read` (simple ; viable avec les virtual threads). NIO (`Selector`, `Channel`, `ByteBuffer`) : un thread multiplexe de nombreuses connexions non bloquantes (Netty, Tomcat NIO). NIO.2 asynchrone (`AsynchronousSocketChannel`, `CompletionHandler`) rarement utilisé directement. Java 21 réhabilite le modèle bloquant simple grâce aux virtual threads ; Netty/Reactor restent pour les besoins extrêmes.

### 183. Comment fonctionne `ByteBuffer` (position, limit, flip, direct vs heap) ?
`🟠 Intermédiaire` · Sujet : **I/O**

**Réponse :** Un tampon avec `position`, `limit`, `capacity` ; on écrit puis `flip()` pour lire, `clear()`/`compact()` pour réutiliser. Heap buffers vivent dans le tas (copie lors des I/O natifs) ; direct buffers (`allocateDirect`) sont hors tas, plus rapides pour les I/O mais coûteux à allouer et limités par `MaxDirectMemorySize` (fuites possibles si mal libérés). Le FFM API `MemorySegment` modernise cette gestion.

### 184. Comment lire et écrire des fichiers volumineux efficacement (streaming, memory-mapped, buffers) ?
`🟠 Intermédiaire` · Sujet : **I/O**

**Réponse :** `Files.newBufferedReader`/`lines()` en streaming (jamais `readAllLines` sur des Go), `BufferedInputStream` avec buffer de 64 Ko+, `FileChannel.transferTo` pour les copies (zero-copy), `MappedByteBuffer` pour l'accès aléatoire à de gros fichiers (attention à l'`unmap` non déterministe), `RandomAccessFile` pour les positions, et compression à la volée (`GZIPInputStream`). Mesurer : le disque est souvent le goulot.

### 185. Comment gérer les encodages de caractères correctement (UTF-8, BOM, `Charset` par défaut) ?
`🟠 Intermédiaire` · Sujet : **I/O**

**Réponse :** Toujours spécifier `StandardCharsets.UTF_8` dans les readers/writers/`getBytes`/`new String` ; depuis Java 18 (JEP 400) le charset par défaut est UTF-8 partout, mais les JDK plus anciens dépendaient de l'OS (bugs Windows cp1252). Détecter/retirer le BOM sur les fichiers tiers, normaliser Unicode (`Normalizer.normalize`, NFC) pour les comparaisons, et déclarer le charset dans les `Content-Type`.

### 186. Comment fonctionne `ProcessBuilder` et comment exécuter des commandes externes sans deadlock ?
`🟠 Intermédiaire` · Sujet : **I/O**

**Réponse :** `new ProcessBuilder(cmd, args).redirectErrorStream(true).start()`, lire la sortie (`inputStream`) dans un thread ou via `inheritIO`/`redirectOutput` avant `waitFor` (sinon le buffer se remplit et le processus bloque), timeout `waitFor(30, SECONDS)` + `destroyForcibly`, arguments en liste (pas de shell, évite l'injection), et `ProcessHandle` pour la supervision. Éviter d'appeler des commandes externes quand une bibliothèque Java existe.

### 187. Comment implémenter un client et un serveur HTTP minimalistes en Java standard et quand le faire ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Client : `java.net.http.HttpClient` (HTTP/2, async). Serveur : `com.sun.net.httpserver.HttpServer` (ou `jwebserver` Java 18 pour du statique) suffit pour des outils internes, health endpoints d'un job ou des tests ; pour une vraie application, Spring Boot/Helidon/Javalin/Vert.x apportent routage, sécurité, observabilité. Comprendre le protocole (headers, keep-alive, chunked) aide au débogage.

### 188. Comment gérer les timeouts, keep-alive et pools de connexions dans les clients HTTP Java ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Toujours fixer connect/read/response timeouts (`HttpClient.newBuilder().connectTimeout`, `HttpRequest.timeout`), réutiliser une instance de client (pool interne), HTTP/2 pour le multiplexage, limiter les connexions par hôte (Apache HttpClient `PoolingHttpClientConnectionManager`), fermer les corps de réponse (fuites de connexions), et gérer les erreurs de connexions réinitialisées par des load balancers avec un `maxLifetime` inférieur à leur timeout d'inactivité.

### 189. Comment sérialiser efficacement entre services Java (JSON vs Protobuf vs Avro vs Kryo/FST) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** JSON (Jackson) : lisible, universel, plus lent et volumineux. Protobuf/gRPC : compact, typé, multi-langage, idéal pour l'interne. Avro : évolution de schéma et écosystème Kafka. Kryo/FST : très rapides mais Java-only et fragiles aux versions (cache, sessions). MessagePack/CBOR : JSON binaire. Choisir selon interopérabilité, évolution de schéma et coût ; toujours versionner les contrats.

### 190. Comment implémenter des retries, timeouts et circuit breakers en Java pur (Resilience4j, Failsafe) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Resilience4j : décorateurs `Retry`, `CircuitBreaker`, `RateLimiter`, `Bulkhead`, `TimeLimiter` composables (`Decorators.ofSupplier(...).withRetry().withCircuitBreaker()`), configurations par nom, métriques Micrometer et événements. Failsafe : API fluide similaire. Règles : retries uniquement sur erreurs transitoires et opérations idempotentes, backoff avec jitter, timeouts globaux, et tests des états du circuit breaker.

### 191. Comment sécuriser un client TLS en Java (validation, pinning, mTLS, TLS 1.3) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Laisser la validation par défaut (truststore, hostname verification) ; ne jamais désactiver (`TrustAll`) même en test ; ajouter des CA privées au truststore ; mTLS via `SSLContext` avec `KeyManager` ; TLS 1.3 par défaut (Java 11+), désactiver les protocoles/ciphers faibles via `jdk.tls.disabledAlgorithms` ; pinning de certificat uniquement avec rotation planifiée. Diagnostiquer avec `-Djavax.net.debug=ssl:handshake`.

### 192. Comment gérer les règles de fuseaux, l'heure d'été et les calculs de durée sans bugs ?
`🟠 Intermédiaire` · Sujet : **Dates**

**Réponse :** `ZonedDateTime` pour les rendez-vous locaux (« 9h à Paris »), `Instant` pour les événements, `Duration` (temps machine) vs `Period` (calendrier) ; `plusDays(1)` sur un `ZonedDateTime` conserve l'heure locale même lors d'un changement d'heure, alors que `plus(Duration.ofHours(24))` la décale ; mettre à jour la base tzdata (`tzupdater`, mises à jour JDK) ; tester les dates autour des transitions et des fins de mois.

### 193. Comment formater et parser des dates de manière robuste et localisée ?
`🟠 Intermédiaire` · Sujet : **Dates**

**Réponse :** `DateTimeFormatter.ISO_INSTANT`/`ISO_OFFSET_DATE_TIME` pour les échanges machine, `ofPattern("dd MMM yyyy", locale)` pour l'affichage, `ofLocalizedDate(FormatStyle.MEDIUM)`, gestion des `DateTimeParseException` ; les formatters sont immuables et thread-safe (contrairement à `SimpleDateFormat`). Ne jamais parser des dates utilisateur sans locale explicite, ni utiliser `yyyy` vs `YYYY` (année ISO de semaine) par erreur.

### 194. Comment tester du code dépendant du temps (`Clock`, `InstantSource`, horloges fixes) ?
`🟠 Intermédiaire` · Sujet : **Dates**

**Réponse :** Injecter un `Clock` (`Clock.systemUTC()` en production, `Clock.fixed`/`Clock.offset` en test) ou `InstantSource` (Java 17) et appeler `Instant.now(clock)`/`LocalDate.now(clock)` ; jamais `Instant.now()` direct dans la logique métier. Pour les timers et délais, abstraire le scheduler ou utiliser des horloges virtuelles (Reactor `VirtualTimeScheduler`, `awaitility` pour les attentes asynchrones).

### 195. Comment manipuler efficacement les chaînes : `String.format`, `MessageFormat`, `StringJoiner`, `repeat`, `strip`, `formatted` ?
`🟠 Intermédiaire` · Sujet : **Texte**

**Réponse :** `"%s".formatted(x)` (Java 15), `String.join`/`StringJoiner`, `repeat`, `strip`/`isBlank`/`lines` (Java 11), `chars()`, `indent`, text blocks. `String.format` est lent en boucle chaude (parsing du pattern) : préférer `StringBuilder` ou `MessageFormat` précompilé ; `intern()` avec parcimonie. Pour les gros volumes, `CharSequence`/`StringBuilder` évitent les copies.

### 196. Comment utiliser les regex efficacement et éviter les catastrophic backtracking ?
`🟠 Intermédiaire` · Sujet : **Texte**

**Réponse :** Précompiler `Pattern` (thread-safe) et réutiliser ; `Matcher` par usage ; groupes nommés ; `find` vs `matches` ; éviter les quantificateurs imbriqués ambigus (`(a+)+`) sur des entrées non fiables (ReDoS) ; borner la taille des entrées ; préférer des parseurs dédiés pour les formats structurés (e-mail, URL, JSON). Tester avec des entrées adverses et un timeout si la regex vient de l'utilisateur.

### 197. Comment parser et générer du CSV, XML et YAML en Java de façon sûre ?
`🟠 Intermédiaire` · Sujet : **Texte**

**Réponse :** CSV : Jackson CSV, OpenCSV ou univocity (guillemets, séparateurs, encodages ; ne jamais `split(",")`). XML : StAX/SAX pour le streaming, JAXB/Jackson XML pour le mapping, désactiver DTD et entités externes (XXE) sur tous les parseurs (`XMLInputFactory.SUPPORT_DTD=false`). YAML : SnakeYAML avec `SafeConstructor`/Jackson YAML, jamais de désérialisation de types arbitraires. Valider contre un schéma quand il existe.

### 198. Comment gérer Unicode correctement (code points, graphèmes, tri, comparaison) ?
`🟠 Intermédiaire` · Sujet : **Texte**

**Réponse :** `String.length()` compte les unités UTF-16, pas les caractères : utiliser `codePointCount`/`codePoints()` et `BreakIterator` pour les graphèmes (emoji composés) ; comparaison et tri par `Collator` pour respecter les règles de langue (accents, casse) ; normalisation NFC/NFKC avant comparaison ; `toLowerCase(Locale.ROOT)` pour les identifiants (le turc `I` piège). Tester avec des caractères hors BMP.

### 199. Comment valider et assainir des entrées en Java (injection, chemins, tailles, types) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Valider en allow-list (regex simples, enums, plages), typer tôt (records/value objects), limiter les tailles, normaliser et vérifier les chemins (`Path.normalize().startsWith(base)`), requêtes préparées, encoder à la sortie selon le contexte (HTML, URL, JSON via bibliothèques), rejeter plutôt que « nettoyer » les entrées suspectes, et centraliser dans des validateurs testés. Bean Validation aux frontières, invariants dans le domaine.

### 200. Comment stocker et manipuler des secrets en mémoire et dans le code (char[], Vault, variables d'environnement) ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Pas de secrets dans le code ni les images ; injection par gestionnaire de secrets (Vault, AWS Secrets Manager) ou fichiers montés ; `char[]` effaçable plutôt que `String` pour les mots de passe saisis (limité en pratique par les bibliothèques) ; ne jamais logger ni sérialiser (`@JsonIgnore`, `toString` masqué) ; rotation régulière ; et scan de secrets en CI (gitleaks). Les heap dumps contiennent les secrets : les protéger.

### 201. Comment implémenter le hachage, le chiffrement et la signature correctement avec les APIs Java ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Mots de passe : Argon2id/bcrypt (bibliothèques). Intégrité : `MessageDigest` SHA-256, HMAC (`Mac`) pour l'authentification. Chiffrement symétrique : `Cipher.getInstance("AES/GCM/NoPadding")` avec IV aléatoire unique de 12 octets et tag 128 bits, clés depuis un KMS/KeyStore. Asymétrique/signature : RSA-PSS ou Ed25519 (Java 15+), `Signature`. `SecureRandom` pour tout aléa ; jamais ECB, ni MD5/SHA-1 pour la sécurité.

### 202. Comment mettre à jour et surveiller les vulnérabilités du JDK et des dépendances ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Suivre les Critical Patch Updates trimestriels et appliquer via des images de base à jour (Temurin), rester sur une LTS supportée, scanner les dépendances (OWASP Dependency-Check, Snyk, Trivy sur l'image), SBOM, `jdeprscan` et `jdeps` pour les APIs internes, et un processus de réponse aux CVE critiques (Log4Shell) avec inventaire des versions déployées par service.

### 203. Comment fonctionne le JIT en détail (interpréteur, C1, C2, profiling, déoptimisation) et comment l'observer ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Le bytecode est interprété, profilé, compilé par C1 (rapide, niveaux 1-3) puis C2 (optimisations agressives : inlining, escape analysis, vectorisation) après des milliers d'invocations ; des hypothèses invalidées (nouvelle classe chargée, branche jamais prise) déclenchent une déoptimisation vers l'interpréteur. Observer avec `-XX:+PrintCompilation`, JITWatch, JFR (compilation events) ; `-XX:CompileThreshold` et `TieredStopAtLevel` pour expérimenter.

### 204. Qu'est-ce que l'inlining et les appels mono/bi/mégamorphiques ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Le JIT inline les petites méthodes chaudes (`-XX:MaxInlineSize`, `FreqInlineSize`) et dévirtualise les sites d'appel monomorphiques (une seule classe vue) ou bimorphiques via des gardes de type ; un site mégamorphique (3+ types) passe par une table virtuelle, plus lent et non inlinable. D'où l'intérêt de limiter la diversité des implémentations dans les boucles chaudes (ou de spécialiser), sans sacrifier la conception ailleurs.

### 205. Comment fonctionne la mémoire de la JVM en dehors du heap (metaspace, code cache, threads, GC, direct, natif) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Metaspace (métadonnées de classes, à borner), code cache (code JIT, `ReservedCodeCacheSize`), piles de threads (`-Xss` × threads), structures GC (G1 remembered sets, cartes), buffers directs (`MaxDirectMemorySize`), mémoire native des bibliothèques (compression, TLS) et malloc arenas (glibc : `MALLOC_ARENA_MAX`). `NativeMemoryTracking` (`-XX:NativeMemoryTracking=summary` + `jcmd VM.native_memory`) détaille l'usage ; indispensable pour expliquer un RSS bien supérieur à `-Xmx`.

### 206. Comment fonctionne G1 en détail (régions, young/mixed collections, remembered sets, humongous, pauses) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Heap découpé en régions (eden, survivor, old, humongous pour les gros objets > demi-région) ; collectes young fréquentes avec évacuation par copie, marquage concurrent de l'old puis collectes « mixed » ciblant les régions les plus vides ; remembered sets suivent les références entre régions. Réglages utiles : `MaxGCPauseMillis`, `G1HeapRegionSize` (objets humongous), `InitiatingHeapOccupancyPercent`. Les allocations humongous fréquentes (gros tableaux) sont un piège de performance.

### 207. Comment fonctionne ZGC générationnel et quels sont ses compromis ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Marquage et relocation concurrents (pauses < 1 ms indépendantes de la taille du heap) grâce aux colored pointers et load barriers ; la version générationnelle (défaut depuis Java 23) collecte séparément les jeunes objets, réduisant le CPU et permettant des taux d'allocation élevés. Compromis : surcoût CPU et mémoire (headroom nécessaire, `SoftMaxHeapSize`), débit légèrement inférieur à Parallel ; idéal pour les services sensibles à la latence avec de gros heaps.

### 208. Que sont les safepoints et pourquoi peuvent-ils provoquer des pauses hors GC ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Un safepoint est un état où tous les threads Java sont arrêtés à des points connus (pour le GC, les déoptimisations, les thread dumps, la révocation de biased locking, JFR). Un thread dans une longue boucle comptée sans safepoint poll (`-XX:+UseCountedLoopSafepoints`) retarde tout le monde (« time to safepoint »). Diagnostiquer avec `-Xlog:safepoint` ; des pauses inexpliquées viennent souvent de là ou de swapping/CPU throttling.

### 209. Comment analyser un thread dump efficacement (états, verrous, patterns) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Prendre 3-5 dumps espacés de quelques secondes (`jcmd <pid> Thread.print`, `jstack`), regrouper les threads par pile identique (fastthread.io, `jstack` analyzers), repérer : nombreux `BLOCKED` sur le même moniteur (contention), `WAITING` sur un pool vide (pas de travail) ou sur une `Condition` de pool de connexions (base saturée), threads `RUNNABLE` bloqués en socket read (dépendance lente), deadlocks signalés en fin de dump. Corréler avec les métriques.

### 210. Comment analyser un heap dump avec Eclipse MAT ou VisualVM (dominator tree, leak suspects, OQL) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Ouvrir le dump (peut nécessiter autant de RAM que le dump), lire « Leak Suspects », le dominator tree (objets retenant le plus de mémoire), les chemins vers les GC roots (« Path to GC Roots » en excluant les références faibles) pour comprendre qui retient, les histogrammes par classe, et OQL pour requêter (`SELECT * FROM java.util.HashMap WHERE size > 100000`). Comparer deux dumps montre la croissance.

### 211. Qu'est-ce que l'`-XX:+UseStringDeduplication`, les compact strings et autres optimisations mémoire ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Compact strings (Java 9) stockent les chaînes Latin-1 sur un octet par caractère ; `UseStringDeduplication` (G1/ZGC/Shenandoah) fusionne les tableaux de chaînes identiques pendant le GC (utile pour les caches de texte dupliqué) ; compressed oops (références 32 bits sous 32 Go de heap, `-XX:+UseCompressedOops` par défaut) ; compressed class pointers ; Project Lilliput (Java 24+ expérimental) réduit les en-têtes d'objets à 8 octets.

### 212. Comment fonctionne le class loading personnalisé et quels problèmes provoque-t-il (leaks, `ClassCastException` entre loaders) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Un `ClassLoader` personnalisé (plugins, hot reload, isolation) charge des classes avec délégation au parent ; une même classe chargée par deux loaders est deux types différents (`ClassCastException` « X cannot be cast to X »). Fuites : un loader reste vivant tant qu'une de ses classes est référencée (threads, `ThreadLocal`, caches statiques, drivers JDBC enregistrés), classique dans les redéploiements de serveurs d'applications. Préférer des processus séparés au chargement dynamique.

### 213. Qu'est-ce que `invokedynamic` et à quoi sert-il (lambdas, concaténation, langages dynamiques) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Une instruction de bytecode dont la cible est résolue à l'exécution par un bootstrap method (`MethodHandle`) puis liée définitivement (call site) : utilisée pour les lambdas (`LambdaMetafactory` génère des classes cachées), la concaténation de chaînes (`StringConcatFactory`), les records (`ObjectMethods`), les patterns switch, et les langages dynamiques sur la JVM (Groovy, Kotlin partiellement). Il rend ces constructions rapides et optimisables par le JIT.

### 214. Comment fonctionnent `MethodHandle` et `VarHandle` et quand les utiliser à la place de la réflexion ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** `MethodHandles.lookup().findVirtual(...)` produit un handle invocable (`invokeExact`) que le JIT peut inliner, bien plus rapide que `Method.invoke` après warm-up ; `VarHandle` (Java 9) offre des accès atomiques et des modes mémoire (`getAcquire`, `compareAndSet`) sur les champs, remplaçant `Unsafe` et `AtomicXFieldUpdater`. Réservés aux frameworks et aux structures concurrentes de bas niveau.

### 215. Comment diagnostiquer une JVM qui consomme du CPU sans requêtes (GC, JIT, threads en boucle, timers) ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** `top -H -p <pid>` pour identifier le thread natif chaud, convertir son TID en hexadécimal et le retrouver dans un thread dump (« nid=0x... »), distinguer GC threads (`-Xlog:gc*`, heap trop petit → GC permanent), compilateur JIT (warm-up, ou déoptimisations en boucle), threads applicatifs en spin (boucle sans attente, `while(!done)`), planificateurs trop fréquents, et loggers/métriques mal configurés. async-profiler `-e cpu` confirme en une minute.

### 216. Comment démarrer une JVM plus vite et consommer moins : CDS, AOT cache (Java 24/25 Leyden), Native Image, jlink ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** AppCDS (Java 10+) et l'AOT cache de Project Leyden (JEP 483 Java 24, JEP 514/515 Java 25 : `-XX:AOTCache` enregistrant classes chargées, liées et profils de méthodes) réduisent le démarrage de 40 % ou plus sans changer le code ; GraalVM Native Image supprime le JIT (démarrage instantané, mémoire minimale, build lent, réflexion à déclarer) ; `jlink` réduit la taille ; CRaC (Coordinated Restore at Checkpoint) restaure une JVM déjà chauffée (Lambda SnapStart en est dérivé).

### 217. Qu'est-ce que CRaC et comment l'utiliser avec Spring Boot ?
`🟠 Intermédiaire` · Sujet : **JVM**

**Réponse :** Coordinated Restore at Checkpoint (JDK Azul/OpenJDK builds) prend un snapshot d'un processus JVM chauffé (`jcmd JDK.checkpoint`) et le restaure en millisecondes ; l'application doit fermer/rouvrir ses ressources (sockets, connexions) via les callbacks `Resource.beforeCheckpoint/afterRestore`, ce que Spring Boot 3.2+ supporte (`spring-boot-starter` + `-Dspring.context.checkpoint=onRefresh`). Contraintes : Linux, image contenant le snapshot, secrets à réinjecter après restauration.

### 218. Comment fonctionne le `ForkJoinPool` (work stealing, `commonPool`, parallélisme, `ManagedBlocker`) ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Chaque worker a une deque de tâches et vole aux autres quand la sienne est vide (work stealing) ; `RecursiveTask`/`RecursiveAction` découpent récursivement (fork) et joignent. Le `commonPool` (parallélisme = cœurs − 1) est partagé par les parallel streams et `CompletableFuture.*Async` sans executor : les tâches bloquantes le saturent (`ManagedBlocker` peut compenser). Utiliser un pool dédié pour les traitements CPU longs.

### 219. Qu'est-ce que la Structured Concurrency (`StructuredTaskScope`) et comment l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Java 21 preview / finalisée en 25 : `try (var scope = StructuredTaskScope.open()) { var a = scope.fork(() -> ...); var b = scope.fork(() -> ...); scope.join(); return combine(a.get(), b.get()); }` : les sous-tâches (virtual threads) vivent dans la portée du bloc, l'échec d'une annule les autres (`ShutdownOnFailure`/joiners), les annulations se propagent, et les traces d'observabilité restent hiérarchiques. Elle remplace les `CompletableFuture` enchevêtrés pour le fan-out/fan-in.

### 220. Comment fonctionne `Phaser`, `Exchanger` et quand ces outils sont-ils pertinents ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** `Phaser` : barrière réutilisable avec nombre de participants dynamique et phases numérotées (simulations, pipelines par étapes). `Exchanger` : deux threads échangent des objets à un point de rendez-vous (double buffering producteur/consommateur). Rarement nécessaires dans le code applicatif ; les connaître montre la maîtrise de `java.util.concurrent`, mais les executors, `CompletableFuture` et les files couvrent la plupart des cas.

### 221. Comment concevoir un pipeline producteur-consommateur robuste (files bornées, poison pill, arrêt, backpressure) ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** `ArrayBlockingQueue`/`LinkedBlockingQueue` bornées (backpressure naturelle : `put` bloque), plusieurs consommateurs dans un `ExecutorService`, arrêt propre par signal (`poison pill` par consommateur, ou flag + `poll(timeout)` + interruption), gestion des exceptions par tâche (ne pas tuer le consommateur), métriques de taille de file et de latence, et idempotence si les éléments peuvent être rejoués. Avec les virtual threads, un thread par élément peut remplacer le pool.

### 222. Comment implémenter un rate limiter ou un token bucket thread-safe en Java ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Un compteur de jetons avec horodatage, rempli à la demande (`tokens = min(capacity, tokens + elapsed × rate)`) protégé par `synchronized`/`ReentrantLock` (contention faible) ou via `AtomicLong` + CAS sur une valeur encodée ; `tryAcquire()` retourne faux si vide. Pour le distribué, Redis + Lua ou Bucket4j ; Resilience4j `RateLimiter` fournit une version prête avec métriques.

### 223. Comment éviter et détecter les fuites de threads et les executors non fermés ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Nommer les threads (`ThreadFactory`), utiliser des daemon threads ou fermer les executors dans un `@PreDestroy`/shutdown hook (`shutdown` + `awaitTermination` + `shutdownNow`), ne pas créer d'executor par requête, surveiller `jvm.threads.live`/`thread dumps` (croissance de threads `pool-N-thread-M`), et `ExecutorService` avec try-with-resources (Java 19+ : `AutoCloseable`). Les threads non-daemon empêchent l'arrêt de la JVM.

### 224. Comment fonctionne `ThreadLocal` en interne et pourquoi peut-il fuir ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Chaque `Thread` porte une `ThreadLocalMap` (clés à références faibles vers le `ThreadLocal`, valeurs fortes) ; avec un pool de threads, la valeur survit à la tâche si `remove()` n'est pas appelé, causant fuites mémoire et fuites de contexte entre requêtes (données d'un utilisateur vues par un autre). Toujours `remove()` en `finally`, préférer `ScopedValue` ou le passage explicite, et éviter les `ThreadLocal` avec les virtual threads en masse.

### 225. Comment fonctionne `synchronized` en interne (moniteurs, lightweight/heavyweight locks, lock elision) ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Chaque objet possède un moniteur ; `synchronized` acquiert un lightweight lock (CAS dans l'en-tête, pas de contention) ou gonfle en heavyweight lock (mutex OS, file d'attente) en cas de contention ; le biased locking a été retiré (Java 15). L'escape analysis élimine les verrous sur des objets non partagés (lock elision) et fusionne les sections adjacentes (coarsening). `synchronized` reste correct et rapide sans contention ; `ReentrantLock` apporte timeouts, équité, conditions multiples, et évite le pinning des virtual threads avant Java 24.

### 226. Quelles garanties offrent `final` et les constructeurs pour la publication sûre d'objets ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** Les champs `final` correctement initialisés dans le constructeur sont visibles par tous les threads après construction, même sans synchronisation (garantie du JMM), à condition que `this` ne s'échappe pas pendant le constructeur (pas d'enregistrement de listener, pas de démarrage de thread dans le constructeur). Les champs non-`final` exigent une publication via `volatile`, verrou, collection concurrente ou initialisation statique. Les records et objets immuables sont donc trivialement thread-safe.

### 227. Comment tester et prouver l'absence de data races (jcstress, Lincheck, tests de stress) ?
`🟠 Intermédiaire` · Sujet : **Concurrence**

**Réponse :** jcstress (OpenJDK) exécute des tests de concurrence sur des millions d'entrelacements et rapporte les résultats observés vs acceptables selon le JMM ; Lincheck (Kotlin/JetBrains, utilisable en Java) génère des scénarios concurrents et vérifie la linéarisabilité d'une structure de données ; tests de stress avec `ExecutorService` et compteurs pour détecter les pertes de mises à jour. Les revues de code restent indispensables : les races sont probabilistes.

### 228. Comment structurer les tests unitaires d'une classe complexe (AAA, builders, paramétrés, propriétés) ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Arrange-Act-Assert avec un seul comportement par test, builders/factories pour les données (`anOrder().withStatus(PAID).build()`), tests paramétrés pour les cas limites, tests de propriétés (jqwik) pour les invariants (« le tri est idempotent »), nommage explicite (`shouldRejectNegativeQuantity`), assertions AssertJ ciblées, et pas de logique conditionnelle dans les tests. Un test difficile à écrire signale souvent une classe à découper.

### 229. Quelles bonnes pratiques et anti-patterns avec Mockito (mocks vs fakes, `verify`, `ArgumentCaptor`, `spy`) ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Mocker les frontières (dépendances externes lentes ou non déterministes), pas les objets de valeur ni les collaborateurs simples (fakes en mémoire plus lisibles) ; vérifier les interactions seulement quand elles sont l'effet attendu (envoi d'un événement) ; `ArgumentCaptor` pour asserter sur les objets envoyés ; éviter `spy` sur la classe testée et les `when(...).thenReturn` en cascade qui répliquent l'implémentation ; strict stubs pour détecter les stubs inutilisés.

### 230. Comment tester du code utilisant le temps, l'aléatoire, le système de fichiers et le réseau ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Injecter `Clock`, `RandomGenerator` (ou une graine fixe), `FileSystem` (Jimfs en mémoire) ou `@TempDir` JUnit 5, `HttpClient` derrière une interface (WireMock/MockWebServer pour l'intégration), et `Awaitility` pour les assertions asynchrones sans `Thread.sleep`. Ces dépendances rendues explicites améliorent aussi la conception (ports/adaptateurs).

### 231. Comment organiser tests unitaires, d'intégration et E2E dans un build Maven/Gradle et en CI ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Surefire (unit, rapides, à chaque commit) vs Failsafe (`*IT`, Testcontainers, phase `verify`) ; profils pour les tests longs (nightly), parallélisation (JUnit 5 `junit.jupiter.execution.parallel`, forks Maven), rapports agrégés (JaCoCo avec seuils raisonnables par module), tests flaky mis en quarantaine et corrigés, et ordonnancement CI (unit → intégration → E2E → déploiement). Les tests doivent rester déterministes et indépendants de l'ordre.

### 232. Qu'est-ce que le testing par approbation (Approval/Snapshot tests) et quand l'utiliser en Java ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Comparer la sortie d'un traitement (JSON, rapport, rendu) à une version approuvée stockée dans le dépôt (ApprovalTests, `JsonAssert`), avec diff lisible à la modification ; utile pour les objets complexes, les migrations de code legacy (tests de caractérisation) et les formats de sortie. Risque : approbations aveugles lors des mises à jour ; à combiner avec des tests d'intention ciblés.

### 233. Comment mesurer et utiliser la couverture de code intelligemment (JaCoCo, seuils, branches) ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** JaCoCo instrumente et rapporte lignes/branches/instructions ; fixer des seuils par module sur les branches plutôt qu'un global de lignes, exclure le code généré, viser la couverture des chemins critiques plutôt que 100 %, et croiser avec le mutation testing pour la qualité. Une couverture élevée sans assertions pertinentes ne prouve rien ; une couverture faible sur le domaine est un signal réel.

### 234. Comment structurer un projet Maven multi-modules et optimiser le build (BOM, profils, cache, parallélisme) ?
`🟠 Intermédiaire` · Sujet : **Build**

**Réponse :** Parent avec `dependencyManagement` et `pluginManagement`, modules par domaine/couche, `-T 1C` pour le build parallèle, `mvn -pl module -am` pour les builds partiels, Maven Build Cache Extension, profils pour les tests longs et les environnements, wrapper `mvnw`, versions fixées (`versions:lock-snapshots`), enforcer (Java version, convergence), reproducible builds (`project.build.outputTimestamp`), et CI avec cache du dépôt local.

### 235. Comment fonctionne Gradle (tâches, configuration cache, build cache, version catalogs, convention plugins) ?
`🟠 Intermédiaire` · Sujet : **Build**

**Réponse :** Graphe de tâches avec entrées/sorties déclarées permettant l'incrémentalité et le build cache (local/distant) ; configuration cache pour accélérer le démarrage ; `libs.versions.toml` (version catalog) centralise les dépendances ; convention plugins (`buildSrc`/`build-logic`) partagent la configuration entre modules sans duplication ; `gradle --scan` pour analyser. Les DSL Kotlin apportent typage et complétion.

### 236. Comment gérer les versions et releases d'une application/bibliothèque Java (SemVer, CalVer, release plugins, tags) ?
`🟠 Intermédiaire` · Sujet : **Build**

**Réponse :** Applications déployées en continu : version calendaire ou SHA + numéro de build, tags Git par déploiement. Bibliothèques : SemVer strict, `maven-release-plugin` ou `jreleaser`/`semantic-release` avec Conventional Commits, publication sur Maven Central (signature GPG, Sonatype) ou un dépôt interne, changelog généré, et vérification de compatibilité binaire (japicmp) avant chaque version mineure.

### 237. Comment créer une image Docker optimale pour une application Java (couches, JRE minimal, non-root, cache) ?
`🟠 Intermédiaire` · Sujet : **Build**

**Réponse :** Multi-stage : build avec JDK (cache des dépendances Maven/Gradle en couche séparée), runtime avec JRE minimal (`eclipse-temurin:21-jre-alpine`/distroless ou `jlink`), extraction des couches Boot (`layertools`/`jarmode=tools`), utilisateur non-root, `ENTRYPOINT ["java", ...]` en forme exec (signaux), `JAVA_TOOL_OPTIONS` pour les flags, `MaxRAMPercentage`, AppCDS/AOT cache généré au build, pas de secrets ni d'outils inutiles, scan de vulnérabilités, et tags immuables.

### 238. Qu'est-ce que Jib, Buildpacks (Paketo) et comment se comparent-ils au Dockerfile ?
`🟠 Intermédiaire` · Sujet : **Build**

**Réponse :** Jib (Google) construit des images optimisées directement depuis Maven/Gradle sans Docker ni Dockerfile (couches dépendances/ressources/classes, reproductibles). Buildpacks Paketo (`spring-boot:build-image`) détectent le projet et produisent des images sécurisées et à jour (base, JVM, mémoire calculée) sans Dockerfile, avec rebase rapide des couches de base. Le Dockerfile reste le plus flexible et transparent ; Jib/Buildpacks réduisent la maintenance.

### 239. Comment choisir entre Spring Boot, Quarkus, Micronaut, Helidon et Vert.x pour un nouveau service ?
`🟠 Intermédiaire` · Sujet : **Écosystème**

**Réponse :** Spring Boot : écosystème et communauté les plus larges, standard en entreprise, natif possible. Quarkus : orienté Kubernetes/natif (build-time), dev mode remarquable, démarrage rapide, extensions curées. Micronaut : DI à la compilation, faible mémoire, proche de Spring en style. Helidon : Oracle, MicroProfile ou Níma sur virtual threads. Vert.x : toolkit réactif événementiel très performant. Choisir selon les compétences de l'équipe, le besoin natif/serverless et l'écosystème requis.

### 240. Qu'est-ce que Jakarta EE et MicroProfile aujourd'hui, et comment se positionnent-ils face à Spring ?
`🟠 Intermédiaire` · Sujet : **Écosystème**

**Réponse :** Jakarta EE (ex Java EE, Eclipse Foundation) : spécifications (Servlet, Persistence, CDI, REST, Bean Validation) implémentées par les serveurs (WildFly, Open Liberty, Payara, GlassFish) ; MicroProfile ajoute config, health, metrics, fault tolerance, OpenAPI, JWT pour les microservices. Spring réutilise plusieurs spécifications Jakarta (Servlet, Persistence, Validation) tout en offrant son propre modèle. Le choix dépend de l'écosystème d'entreprise existant.

### 241. Comment fonctionne le passage à Kotlin dans un projet Java et quelles interopérabilités surveiller ?
`🟠 Intermédiaire` · Sujet : **Écosystème**

**Réponse :** Kotlin compile en bytecode JVM et coexiste fichier par fichier avec Java (même module) ; interop : nullabilité (annotations JSpecify/Jetbrains côté Java pour éviter les platform types), `@JvmStatic`/`@JvmOverloads`/`@JvmField` pour l'API Java, data classes vs records, coroutines vs virtual threads/CompletableFuture, Lombok incompatible avec Kotlin dans le même module. Spring supporte Kotlin nativement ; migrer par les tests ou les nouveaux modules d'abord.

### 242. Quels outils de qualité de code adopter (Error Prone, NullAway, SpotBugs, PMD, Checkstyle, Sonar) et comment les intégrer sans friction ?
`🟠 Intermédiaire` · Sujet : **Écosystème**

**Réponse :** Formatage automatique (Spotless + google-java-format/palantir), Error Prone (bugs à la compilation) + NullAway (null-safety), SpotBugs avec find-sec-bugs, PMD/Checkstyle pour le style résiduel, SonarQube/SonarCloud pour le suivi et les quality gates sur le nouveau code uniquement (ne pas bloquer sur le legacy). Introduire progressivement (warnings → erreurs), et faire échouer la CI sur les nouvelles violations seulement.

### 243. Qu'est-ce qu'OpenRewrite et comment automatiser les migrations (Java, Spring Boot, dépendances) ?
`🟠 Intermédiaire` · Sujet : **Écosystème**

**Réponse :** Un moteur de refactoring à grande échelle basé sur un AST sémantique (LST) avec des recettes composables : migration Java 8 → 21, `javax` → `jakarta`, Spring Boot 2 → 3 → 4, JUnit 4 → 5, remplacement de bibliothèques, corrections de sécurité ; exécuté via plugin Maven/Gradle ou Moderne à l'échelle d'une organisation. Vérifier les diffs et les tests après chaque recette ; combiner avec les migrations manuelles restantes.

### 244. Comment tirer parti des assistants IA pour Java (génération, tests, migration) tout en maintenant la qualité ?
`🟠 Intermédiaire` · Sujet : **Écosystème**

**Réponse :** Fournir le contexte (conventions, versions de Java/Spring, architecture) dans un fichier d'instructions, demander du code moderne (records, virtual threads, `RestClient`) explicitement car les modèles privilégient souvent des APIs anciennes, faire générer et exécuter les tests, relire comme une PR (sécurité, exceptions avalées, dépendances inventées), utiliser OpenRewrite pour les migrations mécaniques et l'IA pour les cas restants, et garder les décisions d'architecture humaines.

### 245. Comment concevoir des value objects typés (identifiants, montants, e-mails) sans surcoût ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Records à un composant avec validation dans le constructeur compact (`record Email(String value) { Email { require(valid(value)); } }`), `toString` utile, conversions explicites (`static Email of(String)`), et intégration : `AttributeConverter` JPA, `@JsonValue`/`@JsonCreator` Jackson, `Converter` Spring pour les paramètres de requête. Le JIT élimine souvent l'allocation (escape analysis) ; Valhalla (value classes, en preview) supprimera le reste.

### 246. Comment modéliser des états et transitions (machines à états) proprement en Java ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** `enum State` avec les transitions autorisées (`canTransitionTo`) ou `sealed interface State permits Draft, Submitted, Approved` avec records portant les données propres à chaque état et des méthodes de transition retournant un nouvel état (immuabilité, exhaustivité du `switch`), validations dans l'agrégat, persistance du nom d'état + colonnes, événements de domaine émis aux transitions, et tests exhaustifs des transitions interdites. Spring Statemachine pour les cas très complexes.

### 247. Comment implémenter un Builder, un Factory et un Registry sans classes Lombok ni frameworks ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Builder : classe imbriquée statique avec méthodes chaînées retournant `this`, validation dans `build()`, ou records + `with`-ers pour les objets simples. Factory : méthodes statiques nommées (`Order.draft(customer)`) ou une classe injectant les dépendances nécessaires à la création. Registry : `Map<Key, Handler>` construit à partir d'une `List<Handler>` injectée (`handler.supports(key)`), immuable après construction. Rester simple : chaque pattern doit résoudre un problème réel.

### 248. Comment concevoir une API fluide et un DSL interne en Java (chaînage, types de phases, lambdas) ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Interfaces représentant les étapes (`From → Where → Select`) pour guider l'ordre des appels par le typage, méthodes retournant l'étape suivante, lambdas pour les blocs (`query(q -> q.where(...))`), `Consumer<Builder>` pour la configuration imbriquée, immuabilité des objets intermédiaires, et messages d'erreur clairs. Exemples : `Stream`, `HttpRequest.newBuilder`, `Comparator`, Spring Security DSL.

### 249. Comment documenter du code Java efficacement (Javadoc, ADR, README, exemples exécutables) ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Javadoc sur les APIs publiques (contrat, préconditions, exceptions, exemples `{@snippet}` Java 18), pas de commentaires paraphrasant le code, noms explicites, ADR pour les décisions, README avec démarrage et architecture, diagrammes C4 générés (Structurizr) ou Modulith, tests lisibles comme documentation, et `package-info.java` pour la responsabilité d'un package. La documentation est versionnée et revue avec le code.

### 250. Quelles règles pour écrire du Java lisible et maintenable (taille, nommage, commentaires, immutabilité) ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Méthodes courtes avec un niveau d'abstraction, noms révélant l'intention, early return, pas de booléens en paramètres, `final`/records par défaut, éviter les `null`, exceptions ciblées, pas de commentaires obsolètes, formatage automatique, dépendances explicites par constructeur, petits packages cohérents, et suppression du code mort. Une revue se concentre sur la conception et la lisibilité, l'outillage sur le style.

### 251. Comment mener une revue de code Java : que vérifier en priorité ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Correction (cas limites, null, concurrence, transactions), sécurité (injections, secrets, validation, désérialisation), lisibilité et nommage, conception (responsabilités, couplage, duplication), tests (présence, pertinence, non-flaky), performance sur les chemins chauds (N+1, allocations en boucle), compatibilité (API, schéma, migrations), observabilité (logs/métriques pertinents), et documentation. Petites PR, commentaires bienveillants et actionnables, distinction bloquant/suggestion.

### 252. Comment aborder un code legacy Java sans tests avant de le modifier ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Comprendre par la lecture et les logs, écrire des tests de caractérisation (ApprovalTests, golden master) capturant le comportement actuel, isoler les dépendances par des « seams » (extraction d'interface, injection, sous-classage en test), refactorer par petits pas sûrs (extraction de méthodes, renommages avec l'IDE), ajouter des tests unitaires sur le code extrait, puis implémenter le changement. Ne jamais réécrire d'un bloc sans filet.

### 253. Comment préparer et réussir un entretien technique Java (approche, questions à poser, erreurs courantes) ?
`🟠 Intermédiaire` · Sujet : **Design**

**Réponse :** Réviser les fondamentaux (collections, concurrence, JVM, exceptions), le Java moderne (records, sealed, streams, virtual threads), l'écosystème (Spring, tests, build), et savoir expliquer ses projets (décisions, compromis, incidents). En live coding : clarifier le problème, penser à voix haute, écrire des tests, gérer les cas limites. Erreurs : réciter sans comprendre, ignorer la complexité, ne pas admettre une inconnue. Poser des questions sur l'équipe, le code, la dette et les pratiques.
