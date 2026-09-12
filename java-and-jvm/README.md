# ☕ Java & JVM

> Java 8-21, Virtual Threads, GC, JIT, concurrency, memory leaks, thread dumps

**50 questions**

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
