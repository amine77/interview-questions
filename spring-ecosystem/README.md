# 🌱 Spring Ecosystem

> Spring Core, Boot, Data, Batch, Cloud, Security, Actuator

**100 questions**

---

### 1. Qu'est-ce que l'auto-configuration dans Spring Boot ?
`🟢 Débutant` · Sujet : **Spring Boot**

**Réponse :** Mécanisme qui configure automatiquement les beans nécessaires en fonction des dépendances présentes dans le classpath (ex : si `spring-boot-starter-web` est présent, Tomcat et Spring MVC sont configurés automatiquement). Elle repose sur les annotations `@Conditional` et le fichier `AutoConfiguration.imports`.

### 2. Qu'est-ce qu'un `SecurityFilterChain` dans Spring Security ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Chaîne de filtres servlet qui traite les requêtes HTTP pour appliquer authentification, autorisation, protection CSRF, etc. Se configure via un bean `SecurityFilterChain` depuis Spring Security 5.7+.

### 3. Différence entre `CrudRepository`, `PagingAndSortingRepository` et `JpaRepository` ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `CrudRepository` fournit le CRUD de base. `PagingAndSortingRepository` ajoute pagination/tri. `JpaRepository` étend les deux et ajoute des méthodes spécifiques JPA (flush, batch delete).

### 4. Trois composants principaux d'un Job Spring Batch ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Un Job composé de Steps ; chaque Step suit le modèle ItemReader/ItemProcessor/ItemWriter, souvent chunk-oriented.

### 5. À quoi sert Spring Cloud Config ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Serveur de configuration centralisé gérant les propriétés de plusieurs microservices depuis un dépôt externe, avec rafraîchissement à chaud.

### 6. Différence entre `@Component`, `@Service`, `@Repository` ?
`🟢 Débutant` · Sujet : **Spring**

**Réponse :** Spécialisations de `@Component`. `@Service` = couche métier. `@Repository` = accès données + traduction d'exceptions persistance.

### 7. Différence authentification / autorisation ?
`🟢 Débutant` · Sujet : **Spring Sécurité**

**Réponse :** Authentification = vérifier l'identité. Autorisation = déterminer les droits d'accès.

### 8. Que fait `@Query` ?
`🟢 Débutant` · Sujet : **Spring Data**

**Réponse :** Définit une requête JPQL (ou SQL natif) personnalisée sur une méthode de repository.

### 9. Différence Tasklet / chunk-oriented ?
`🟢 Débutant` · Sujet : **Spring Batch**

**Réponse :** Tasklet = action unique atomique. Chunk-oriented = traitement par lots via Reader/Processor/Writer avec transactions par chunk.

### 10. À quoi sert un API Gateway ?
`🟢 Débutant` · Sujet : **Spring Cloud**

**Réponse :** Point d'entrée unique routant vers les microservices, centralisant authentification, rate limiting, logging.

### 11. Injection par constructeur vs par champ ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Constructeur = dépendances explicites, immuables, testables sans conteneur. Champ = concis mais implicite, tests plus difficiles.

### 12. Trois parties d'un JWT ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Header (algorithme), payload (claims), signature (intégrité), encodées en Base64.

### 13. N+1 select problem et solution ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Problème de performance : requête initiale + N requêtes supplémentaires pour relations lazy. Solution : JOIN FETCH, @EntityGraph.

### 14. À quoi sert Spring Boot Actuator ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Expose des endpoints de monitoring/gestion (/health, /metrics, /info) pour l'observabilité en production.

### 15. Pourquoi CSRF activé par défaut dans Spring Security ?
`🟢 Débutant` · Sujet : **Spring Sécurité**

**Réponse :** Protège les applications avec état de session, en générant un token à valider sur les requêtes modifiant l'état.

### 16. Qu'est-ce qu'un JobRepository ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Persiste les métadonnées d'exécution (jobs, steps, statuts), permettant suivi, reprise et audit.

### 17. Qu'est-ce que le service discovery (Eureka) ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Mécanisme permettant aux microservices de se localiser dynamiquement via un registre central.

### 18. À quoi sert `application.properties`/`application.yml` ?
`🟢 Débutant` · Sujet : **Spring Boot**

**Réponse :** Centralise la configuration externalisée (port, datasource, profils) sans recompiler le code.

### 19. Principe du moindre privilège ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** N'accorder que les permissions strictement nécessaires, réduisant la surface d'attaque.

### 20. Projection dans Spring Data JPA ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Récupère un sous-ensemble de champs (interface/DTO) plutôt que l'entité complète.

### 21. Qu'est-ce qu'un JobLauncher ?
`🟢 Débutant` · Sujet : **Spring Batch**

**Réponse :** Démarre l'exécution d'un Job avec des JobParameters donnés.

### 22. Spring Cloud Sleuth / Micrometer Tracing ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Ajoute trace ID/span ID aux requêtes distribuées, couplé à Zipkin pour visualisation.

### 23. Qu'est-ce qu'un BeanPostProcessor ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Intercepte/modifie les beans avant/après leur initialisation, utilisé pour l'AOP proxying.

### 24. Pourquoi BCryptPasswordEncoder ?
`🟢 Débutant` · Sujet : **Spring Sécurité**

**Réponse :** Intègre un salt aléatoire et un facteur de coût ajustable, rendant les attaques par force brute difficiles.

### 25. Différence `findById()` / `getReferenceById()` ?
`🟢 Débutant` · Sujet : **Spring Data**

**Réponse :** findById exécute une requête immédiate (Optional). getReferenceById retourne un proxy paresseux.

### 26. ItemProcessor composite ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Enchaîne plusieurs processeurs (CompositeItemProcessor), chacun transformant la sortie du précédent.

### 27. Qu'est-ce que Spring Cloud Bus ?
`🟢 Débutant` · Sujet : **Spring Cloud**

**Réponse :** Relie les instances via un bus de messages pour diffuser des événements (ex: refresh config).

### 28. Qu'est-ce qu'un profil Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Active des beans/configurations selon l'environnement (dev, test, prod).

### 29. OAuth2 et resource server ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** OAuth2 = autorisation déléguée. Resource server = héberge les ressources protégées et valide les tokens.

### 30. Specification pattern ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Construit des requêtes JPA dynamiques et composables via critères combinables (and/or).

### 31. Utilité de `@SpringBootApplication` ?
`🟢 Débutant` · Sujet : **Spring Boot**

**Réponse :** Combine `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`.

### 32. Qu'est-ce qu'un UserDetailsService ?
`🟢 Débutant` · Sujet : **Spring Sécurité**

**Réponse :** Interface avec `loadUserByUsername()` pour charger les informations utilisateur.

### 33. Qu'est-ce qu'un SkipPolicy ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Définit les conditions pour ignorer une erreur sur un item plutôt que faire échouer le step, avec un max configurable.

### 34. Client-Side Load Balancing (Spring Cloud LoadBalancer) ?
`🟢 Débutant` · Sujet : **Spring Cloud**

**Réponse :** Répartition de charge effectuée par le client entre instances découvertes dynamiquement.

### 35. Qu'est-ce que le pattern "12-Factor App" et son lien avec Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready Spring Boot**

**Réponse :** Ensemble de bonnes pratiques pour construire des applications cloud-native (configuration externalisée, stateless, logs en flux stdout, dépendances déclarées explicitement). Spring Boot facilite son application via les profils, les propriétés externalisées, et Actuator.

### 36. Comment sécuriser les endpoints Actuator en production ?
`🟢 Débutant` · Sujet : **Spring Actuator**

**Réponse :** En restreignant l'exposition des endpoints sensibles (`management.endpoints.web.exposure.include`), en les plaçant derrière une authentification dédiée (souvent un port de gestion séparé), et en désactivant les endpoints non nécessaires comme `/env` ou `/heapdump`.

### 37. Qu'est-ce qu'un "readiness probe" vs un "liveness probe" ?
`🟠 Intermédiaire` · Sujet : **Cloud-ready Spring Boot**

**Réponse :** Le liveness probe indique si l'application est vivante. Le readiness probe indique si elle est prête à recevoir du trafic. Spring Boot Actuator les expose via /actuator/health/liveness et /readiness.

### 38. Comment fonctionne `@Transactional` et quels sont ses pièges classiques ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Spring crée un proxy autour du bean : il ouvre une transaction avant la méthode, commit après, rollback sur `RuntimeException` (pas sur les checked par défaut). Pièges : appel interne `this.method()` qui contourne le proxy, méthode `private` ou `final` non interceptée, `rollbackFor` oublié pour les exceptions checked, et transaction trop longue englobant des appels réseau.

### 39. Quels sont les niveaux de propagation de transaction et à quoi sert `REQUIRES_NEW` ?
`🔴 Avancé` · Sujet : **Spring**

**Réponse :** `REQUIRED` (défaut) rejoint la transaction existante ou en crée une. `REQUIRES_NEW` suspend la transaction courante et en ouvre une indépendante, utile pour persister un log d'audit même si la transaction principale échoue. `SUPPORTS`, `MANDATORY`, `NOT_SUPPORTED`, `NEVER` et `NESTED` (savepoint) couvrent les autres cas.

### 40. Différence entre `@RestControllerAdvice` et un `@ExceptionHandler` local ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@ExceptionHandler` dans un contrôleur ne s'applique qu'à ce contrôleur. `@RestControllerAdvice` centralise la gestion des exceptions pour toute l'application et permet de renvoyer un format d'erreur uniforme, idéalement `ProblemDetail` (RFC 9457) supporté nativement par Spring 6.

### 41. Qu'est-ce que `@ConfigurationProperties` et pourquoi le préférer à `@Value` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@ConfigurationProperties` lie un préfixe de configuration à un POJO/record typé, avec validation (`@Validated`), métadonnées pour l'IDE et support des listes/maps. `@Value` reste pratique pour une valeur isolée mais disperse la configuration et ne se valide pas au démarrage.

### 42. Différence entre `FetchType.LAZY` et `EAGER`, et qu'est-ce que la `LazyInitializationException` ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `EAGER` charge la relation immédiatement, `LAZY` à la première utilisation via un proxy. La `LazyInitializationException` survient quand on accède à une relation lazy hors session Hibernate (transaction fermée, par exemple dans la sérialisation JSON). Solutions : `@EntityGraph`, `JOIN FETCH`, DTO/projection, ou charger les données dans la transaction (jamais `open-in-view=true` en production).

### 43. Comment gérer la pagination et le tri avec Spring Data ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** On passe un `Pageable` (`PageRequest.of(page, size, Sort.by("name"))`) au repository, qui renvoie un `Page<T>` (contenu + total + métadonnées) ou un `Slice<T>` (sans `COUNT`, plus léger). Côté web, Spring résout automatiquement `?page=0&size=20&sort=name,desc` en `Pageable`.

### 44. Comment implémenter le verrouillage optimiste avec JPA ?
`🔴 Avancé` · Sujet : **Spring Data**

**Réponse :** Ajouter un champ annoté `@Version` (entier ou timestamp). Hibernate inclut la version dans le `WHERE` de l'`UPDATE` et l'incrémente ; si aucune ligne n'est affectée, il lève `OptimisticLockException`. C'est la stratégie par défaut pour les conflits rares ; `@Lock(PESSIMISTIC_WRITE)` sert aux cas de forte contention.

### 45. Comment fonctionne la sécurité par méthode avec `@PreAuthorize` ?
`🔴 Avancé` · Sujet : **Spring Sécurité**

**Réponse :** Activée par `@EnableMethodSecurity`, elle évalue une expression SpEL avant l'appel (`hasRole('ADMIN')`, `#id == authentication.principal.id`). Elle repose sur un proxy AOP, donc mêmes limites que `@Transactional` (appels internes non interceptés). `@PostAuthorize` et `@PostFilter` permettent de filtrer sur le résultat.

### 46. Comment valider un JWT dans un Resource Server Spring Security ?
`🔴 Avancé` · Sujet : **Spring Sécurité**

**Réponse :** Avec `spring-boot-starter-oauth2-resource-server` et `spring.security.oauth2.resourceserver.jwt.issuer-uri`, Spring télécharge les clés publiques (JWKS) de l'issuer, vérifie signature, expiration, audience, et convertit les claims en `Authentication`. Un `JwtAuthenticationConverter` personnalisé permet de mapper les rôles/scopes en `GrantedAuthority`.

### 47. Qu'est-ce qu'un `starter` Spring Boot et comment créer le sien ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un starter est une dépendance regroupant les librairies et une auto-configuration cohérente (`spring-boot-starter-web`). Créer le sien : un module `xxx-autoconfigure` avec des classes `@AutoConfiguration` conditionnelles (`@ConditionalOnClass`, `@ConditionalOnMissingBean`) déclarées dans `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`, et un module `xxx-starter` qui l'agrège.

### 48. Différence entre `RestTemplate`, `WebClient` et le nouveau `RestClient` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `RestTemplate` : API synchrone historique, en maintenance. `WebClient` : réactif non bloquant (WebFlux), adapté aux flux et à la haute concurrence. `RestClient` (Spring 6.1) : API fluide moderne et synchrone, sans dépendance réactive, recommandé pour les nouvelles applications Spring MVC ; il peut être exposé via des interfaces déclaratives `@HttpExchange`.

### 49. Comment gérer les retries et timeouts avec Resilience4j dans Spring Boot ?
`🔴 Avancé` · Sujet : **Cloud-ready Spring Boot**

**Réponse :** Les annotations `@Retry`, `@TimeLimiter`, `@CircuitBreaker`, `@RateLimiter` et `@Bulkhead` se configurent dans `application.yml` par instance nommée (nombre de tentatives, backoff exponentiel, exceptions à ignorer). L'ordre d'application par défaut est Retry > CircuitBreaker > RateLimiter > TimeLimiter > Bulkhead, et les métriques sont exposées via Actuator/Micrometer.

### 50. Comment redémarrer un job Spring Batch échoué et à quoi servent les `JobParameters` ?
`🔴 Avancé` · Sujet : **Spring Batch**

**Réponse :** Le `JobRepository` mémorise l'`ExecutionContext` de chaque step ; relancer le job avec les mêmes `JobParameters` reprend au dernier chunk commité si le step est `restartable`. Les `JobParameters` identifient une instance de job : des paramètres identiques sur un job déjà `COMPLETED` provoquent `JobInstanceAlreadyCompleteException`, d'où l'ajout d'un paramètre unique (timestamp) via `RunIdIncrementer`.

### 51. Qu'est-ce que l'inversion de contrôle et l'injection de dépendances ?
`🟢 Débutant` · Sujet : **Spring**

**Réponse :** L'IoC confie au conteneur Spring la création et l'assemblage des objets (beans) au lieu que le code les instancie lui-même. L'injection de dépendances en est la mise en œuvre : Spring fournit à un bean ses collaborateurs (par constructeur, principalement). Bénéfices : découplage, testabilité (mocks), configuration centralisée.

### 52. Quels sont les scopes de bean Spring ?
`🟢 Débutant` · Sujet : **Spring**

**Réponse :** `singleton` (défaut, une instance par conteneur), `prototype` (nouvelle instance à chaque injection), et pour le web : `request`, `session`, `application`, `websocket`. Injecter un prototype dans un singleton exige un `ObjectProvider`/`@Lookup` ou un proxy scoped, sinon une seule instance est créée.

### 53. Quel est le cycle de vie d'un bean Spring ?
`🟢 Débutant` · Sujet : **Spring**

**Réponse :** Instanciation, injection des dépendances, `Aware` callbacks, `BeanPostProcessor.postProcessBeforeInitialization`, `@PostConstruct`/`InitializingBean.afterPropertiesSet`, `postProcessAfterInitialization` (création des proxies AOP), utilisation, puis `@PreDestroy`/`DisposableBean.destroy` à la fermeture du contexte.

### 54. Différence entre `@Bean` et `@Component` ?
`🟢 Débutant` · Sujet : **Spring**

**Réponse :** `@Component` (et ses spécialisations) annote une classe pour qu'elle soit détectée par le scan de composants. `@Bean` annote une méthode d'une classe `@Configuration` qui produit l'objet, utile pour des classes tierces qu'on ne peut pas annoter, ou quand la construction demande de la logique. Les deux produisent des beans gérés de la même façon.

### 55. Que fait `@Autowired` et pourquoi est-il optionnel sur les constructeurs ?
`🟢 Débutant` · Sujet : **Spring**

**Réponse :** Il marque un point d'injection. Depuis Spring 4.3, une classe avec un seul constructeur est injectée automatiquement sans annotation. Avec plusieurs beans candidats du même type, utiliser `@Qualifier`, `@Primary`, ou injecter une `List<T>`/`Map<String,T>`. L'injection par champ est déconseillée (non testable sans Spring, dépendances cachées).

### 56. Comment résoudre une dépendance circulaire entre beans ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Spring lève `BeanCurrentlyInCreationException` avec l'injection par constructeur (les références circulaires sont interdites par défaut depuis Boot 2.6). C'est un signal de conception : extraire la logique commune dans un troisième bean, utiliser des événements, ou en dernier recours `@Lazy` sur l'un des paramètres pour injecter un proxy.

### 57. Qu'est-ce que Spring AOP et comment fonctionnent les proxies ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** La programmation orientée aspect intercepte les appels de méthodes (transactions, sécurité, cache, logs) via des proxies : proxy JDK (interfaces) ou CGLIB (sous-classe, défaut dans Boot). Conséquences : seuls les appels externes au bean passent par le proxy (un appel `this.m()` interne ignore `@Transactional`/`@Cacheable`), et les méthodes `final`/`private` ne sont pas interceptées.

### 58. Qu'est-ce qu'une annotation conditionnelle (`@ConditionalOnProperty`, `@ConditionalOnMissingBean`) ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Des conditions évaluées au démarrage pour créer ou non un bean : présence d'une classe (`@ConditionalOnClass`), d'un bean (`@ConditionalOnBean`/`OnMissingBean`), d'une propriété, d'un profil, d'une application web. Elles sont le mécanisme de l'auto-configuration et permettent qu'une définition utilisateur remplace celle par défaut. `--debug` affiche le rapport de conditions.

### 59. Comment fonctionne l'ordre de chargement de la configuration (properties, YAML, variables d'environnement) ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Priorité décroissante : arguments de ligne de commande, propriétés système Java, variables d'environnement (relaxed binding : `SERVER_PORT` → `server.port`), `application-{profile}.yml`, `application.yml`, puis valeurs par défaut. Les fichiers externes au jar (répertoire `config/`) priment sur ceux du classpath. Spring Cloud Config et `spring.config.import` s'insèrent dans cette hiérarchie.

### 60. Que sont les événements Spring (`ApplicationEvent`, `@EventListener`) ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Un mécanisme publish/subscribe interne : `ApplicationEventPublisher.publishEvent(obj)` et des méthodes `@EventListener` (synchrones par défaut, `@Async` pour découpler). `@TransactionalEventListener` exécute après commit, idéal pour envoyer un e-mail ou un message Kafka seulement si la transaction a réussi. Il réduit le couplage entre modules.

### 61. Comment fonctionne `@Async` et quels sont ses pièges ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** `@EnableAsync` + `@Async` exécute la méthode dans un executor (à configurer : par défaut `SimpleAsyncTaskExecutor` sans pool avant Boot 3.2, un `ThreadPoolTaskExecutor` ensuite). Pièges : appel interne ignoré (proxy), exceptions perdues si retour `void` (définir `AsyncUncaughtExceptionHandler`), perte du contexte de sécurité/transaction, et retour `CompletableFuture` pour composer.

### 62. Comment fonctionne `@Scheduled` et comment l'exécuter en cluster ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** `@EnableScheduling` + `@Scheduled(cron=..., fixedDelay=...)` sur une méthode. Par défaut un seul thread (`spring.task.scheduling.pool.size` à augmenter). En multi-instances, chaque nœud exécute la tâche : utiliser ShedLock (verrou en base/Redis) ou Quartz en mode clustered, ou déléguer à un CronJob Kubernetes.

### 63. Qu'est-ce que le cache abstraction (`@Cacheable`, `@CacheEvict`, `@CachePut`) ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** Une couche déclarative au-dessus d'un fournisseur (Caffeine local, Redis distribué, Hazelcast) : `@Cacheable` met en cache le résultat par clé (SpEL), `@CacheEvict` invalide, `@CachePut` met à jour sans court-circuiter. Pièges : appel interne, méthodes non déterministes, absence de TTL par défaut avec `ConcurrentMapCacheManager`, sérialisation des valeurs avec Redis.

### 64. Comment gérer la validation avec Bean Validation dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring**

**Réponse :** `@Valid`/`@Validated` sur les paramètres de contrôleur déclenchent les contraintes (`@NotNull`, `@Size`, `@Email`, `@Pattern`) et lèvent `MethodArgumentNotValidException` (400). Groupes de validation, contraintes personnalisées (`@Constraint` + `ConstraintValidator`), validation des `@ConfigurationProperties` au démarrage, et `@Validated` au niveau service pour valider les appels de méthodes.

### 65. Comment gérer les erreurs de manière uniforme avec `ProblemDetail` (RFC 9457) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Spring 6 supporte nativement `ProblemDetail` (`application/problem+json`) : activer `spring.mvc.problemdetails.enabled=true` ou retourner/lever `ErrorResponseException`. Un `@RestControllerAdvice` étendant `ResponseEntityExceptionHandler` centralise la conversion des exceptions métier en réponses structurées (type, title, status, detail, instance) sans exposer les stack traces.

### 66. Qu'est-ce que `spring-boot-devtools` et le rechargement à chaud ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un module de développement : redémarrage automatique du contexte à la modification des classes (deux class loaders, redémarrage rapide), LiveReload, propriétés de dev (cache désactivé), et exclusion automatique du jar de production. Pour un vrai hot swap sans redémarrage, JRebel ou le HotSwap de la JVM (limité).

### 67. Comment tester un contrôleur avec `@WebMvcTest` et `MockMvc` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@WebMvcTest(MyController.class)` charge uniquement la couche web (contrôleurs, filtres, converters, advice), sans base ni services (à mocker avec `@MockitoBean`, remplaçant `@MockBean` en Boot 3.4). `MockMvc` (ou `MockMvcTester` AssertJ) simule des requêtes HTTP sans serveur : vérification du statut, du JSON (`jsonPath`), des headers et de la sécurité.

### 68. Comment tester la couche persistance avec `@DataJpaTest` et Testcontainers ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@DataJpaTest` charge uniquement JPA, les repositories et une base embarquée H2 par défaut, chaque test étant transactionnel avec rollback. Pour tester contre la vraie base, désactiver le remplacement (`@AutoConfigureTestDatabase(replace = NONE)`) et utiliser Testcontainers avec `@ServiceConnection` (Boot 3.1+) qui configure automatiquement l'URL du conteneur.

### 69. Différence entre `@SpringBootTest` et les tests par tranche (slices) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@SpringBootTest` charge tout le contexte (lent, mais teste l'intégration réelle, avec `webEnvironment=RANDOM_PORT` et `TestRestTemplate`/`WebTestClient`). Les slices (`@WebMvcTest`, `@DataJpaTest`, `@JsonTest`, `@RestClientTest`) chargent une couche pour des tests rapides et ciblés. Spring met en cache les contextes identiques : limiter les variations de configuration pour accélérer la suite.

### 70. Qu'est-ce que `@TestConfiguration` et comment surcharger un bean en test ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Une configuration additionnelle (non détectée par le scan) déclarée en classe interne ou importée, pour ajouter ou remplacer des beans en test (`spring.main.allow-bean-definition-overriding` si même nom). `@MockitoBean`/`@MockitoSpyBean` remplacent un bean par un mock. `@DynamicPropertySource` injecte des propriétés calculées (port d'un Testcontainer).

### 71. Comment configurer les logs dans Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Logback par défaut via `logging.level.*`, `logging.pattern`, `logging.file.name`, ou un `logback-spring.xml` avec profils. Boot 3.4 ajoute le logging structuré (`logging.structured.format.console=ecs|logstash|gelf`) en JSON pour les collecteurs. Corréler avec les traces via MDC (`traceId`, `spanId` injectés par Micrometer Tracing).

### 72. Comment construire une image Docker optimisée d'une application Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `mvn spring-boot:build-image` (Buildpacks, sans Dockerfile) ou un Dockerfile multi-stage exploitant le jar en couches (`java -Djarmode=tools -jar app.jar extract --layers`) : dépendances, snapshots, loader, application dans des couches séparées pour maximiser le cache. Utilisateur non-root, image de base JRE minimale, AppCDS/CDS pour le démarrage, `MaxRAMPercentage` plutôt que `-Xmx`.

### 73. Quelles nouveautés majeures de Spring Boot 3.x et Spring Framework 6 ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Java 17 minimum, Jakarta EE 9+ (`jakarta.*`), support des virtual threads (`spring.threads.virtual.enabled=true`, Boot 3.2), `RestClient`, `JdbcClient`, interfaces HTTP déclaratives (`@HttpExchange`), Micrometer Observation, support natif GraalVM, `ProblemDetail`, Docker Compose et Testcontainers intégrés, logging structuré (3.4), et Spring Boot 4 / Framework 7 (fin 2025) avec Jackson 3, modularisation et versioning d'API.

### 74. Comment activer les virtual threads et quel impact ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring.threads.virtual.enabled=true` (Java 21+) fait tourner Tomcat, `@Async`, `@Scheduled` et les listeners Kafka/RabbitMQ sur des virtual threads. Les applications bloquantes (JDBC, RestClient) supportent alors bien plus de requêtes concurrentes sans passer à WebFlux. Vérifier les bibliothèques utilisant `synchronized` (pinning avant Java 24) et dimensionner les pools de connexions en conséquence.

### 75. Que sont les interfaces HTTP déclaratives (`@HttpExchange`) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Une interface Java annotée (`@GetExchange("/users/{id}")`) dont Spring génère l'implémentation via `HttpServiceProxyFactory` sur un `RestClient`/`WebClient`, comme Feign mais intégré au framework. Boot 3.x/4 simplifie l'enregistrement (`@ImportHttpServices`). Avantage : client typé sans boilerplate, testable par mock.

### 76. Comment fonctionne l'intégration Docker Compose de Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Avec `spring-boot-docker-compose`, au démarrage en développement Boot lance `docker compose up` sur le fichier `compose.yaml` du projet, attend les services (PostgreSQL, Redis, Kafka…) et configure automatiquement les propriétés de connexion via `ServiceConnection`. Il arrête les conteneurs à la fermeture. Désactivé en test et en production.

### 77. Comment gérer plusieurs sources de données dans une application ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Déclarer deux `DataSource` (une `@Primary`), avec leurs `EntityManagerFactory`, `TransactionManager` et `@EnableJpaRepositories(basePackages, entityManagerFactoryRef, transactionManagerRef)` séparés. Utiliser `@Transactional("tm2")` pour cibler. Pour la cohérence entre les deux bases, éviter les transactions distribuées (JTA) : préférer l'outbox ou la compensation.

### 78. Comment fonctionnent les méthodes dérivées (query methods) de Spring Data ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Spring Data parse le nom de la méthode (`findByStatusAndCreatedAtAfterOrderByCreatedAtDesc`) pour générer la requête. Mots-clés : `And`, `Or`, `Between`, `LessThan`, `Like`, `In`, `IsNull`, `Exists`, `Distinct`, `First`/`Top`. Au-delà de deux ou trois critères, préférer `@Query`, les Specifications ou Querydsl pour la lisibilité.

### 79. Qu'est-ce que l'audit JPA (`@CreatedDate`, `@LastModifiedBy`) ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `@EnableJpaAuditing` + `@EntityListeners(AuditingEntityListener.class)` remplissent automatiquement `@CreatedDate`, `@LastModifiedDate`, `@CreatedBy`, `@LastModifiedBy`. Un `AuditorAware<T>` fournit l'utilisateur courant (depuis le `SecurityContext`). Pour l'historique complet des versions, Hibernate Envers.

### 80. Comment gérer les modifications en masse (`@Modifying`) et le cache de premier niveau ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `@Modifying @Query("update ... ")` exécute un UPDATE/DELETE JPQL directement en base, sans passer par les entités chargées : le contexte de persistance devient obsolète. Utiliser `@Modifying(clearAutomatically = true, flushAutomatically = true)` et une transaction. Pour les gros volumes, préférer JDBC batch ou Spring Batch.

### 81. Différence entre Spring Data JPA et Spring Data JDBC ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Spring Data JDBC est un ORM simplifié sans contexte de persistance, lazy loading ni cache : les agrégats (DDD) sont chargés et sauvegardés entiers, le mapping est explicite et prévisible, pas de dirty checking magique. Idéal pour des modèles simples ou une approche DDD stricte ; JPA/Hibernate reste plus riche pour les graphes complexes et les optimisations fines.

### 82. Qu'est-ce que `JdbcClient` et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Une API fluide (Spring 6.1) au-dessus de `JdbcTemplate` : `jdbcClient.sql("select ... where id = :id").param("id", id).query(User.class).single()`. Elle simplifie le SQL natif avec paramètres nommés et mapping automatique, pour les requêtes de reporting, les projections complexes ou les projets préférant le SQL explicite à JPA.

### 83. Comment gérer les transactions en lecture seule et pourquoi ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `@Transactional(readOnly = true)` : Hibernate désactive le dirty checking et le flush (moins de mémoire et de CPU), le driver peut router vers une réplique en lecture, et certaines bases optimisent. À placer sur les méthodes de service de lecture ; ce n'est pas une garantie de sécurité contre les écritures dans tous les cas.

### 84. Comment fonctionne la chaîne de filtres de Spring Security ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `DelegatingFilterProxy` → `FilterChainProxy` → une ou plusieurs `SecurityFilterChain` sélectionnées par `securityMatcher`. Chaque chaîne enchaîne des filtres ordonnés : CORS, CSRF, authentification (`BearerTokenAuthenticationFilter`, `UsernamePasswordAuthenticationFilter`), `ExceptionTranslationFilter`, `AuthorizationFilter`. Le résultat est stocké dans le `SecurityContextHolder` (ThreadLocal, ou propagation avec virtual threads).

### 85. Comment configurer plusieurs `SecurityFilterChain` (API vs pages web) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Déclarer plusieurs beans avec `@Order` et `http.securityMatcher("/api/**")` : la chaîne API stateless (JWT, CSRF désactivé, `SessionCreationPolicy.STATELESS`), la chaîne web avec formulaire de login, session et CSRF. La première chaîne dont le matcher correspond traite la requête ; la chaîne sans matcher doit être en dernier.

### 86. Comment fonctionne le client OAuth2 / OIDC login dans Spring Security ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `spring-boot-starter-oauth2-client` + `spring.security.oauth2.client.registration.*` configurent le flux Authorization Code : redirection vers le fournisseur (Keycloak, Google), échange du code, création d'un `OidcUser`, session. `OAuth2AuthorizedClientManager` fournit les access tokens pour appeler des APIs en aval, avec rafraîchissement automatique.

### 87. Comment mapper les rôles/claims d'un JWT vers des `GrantedAuthority` ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Par défaut le scope devient `SCOPE_x`. Fournir un `JwtAuthenticationConverter` avec un `JwtGrantedAuthoritiesConverter` personnalisé lisant par exemple `realm_access.roles` de Keycloak et préfixant `ROLE_`. Pour des règles complexes, un convertisseur produisant un `AbstractAuthenticationToken` avec un principal métier.

### 88. Comment tester la sécurité (`@WithMockUser`, `SecurityMockMvcRequestPostProcessors`) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `spring-security-test` fournit `@WithMockUser(roles="ADMIN")`, `@WithUserDetails`, et pour MockMvc `with(jwt().authorities(...))`, `with(csrf())`, `with(oidcLogin())`. Tester les cas 401/403 autant que les cas passants, et les règles `@PreAuthorize` avec des tests de méthode.

### 89. Qu'est-ce que Spring Authorization Server ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Un projet Spring fournissant un serveur OAuth 2.1 / OpenID Connect complet (authorization code + PKCE, client credentials, device code, JWK, consentement) pour construire son propre fournisseur d'identité ou un serveur de tokens interne, en alternative à Keycloak quand on veut une intégration Java native et personnalisable.

### 90. Comment gérer CORS dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Configurer un `CorsConfigurationSource` (origines, méthodes, headers, credentials) et `http.cors(Customizer.withDefaults())` pour que le filtre CORS s'exécute avant l'authentification (sinon le preflight OPTIONS est rejeté en 401). `@CrossOrigin` sur les contrôleurs ne suffit pas avec Spring Security. Ne jamais mettre `*` avec `allowCredentials=true`.

### 91. Qu'est-ce que Spring Cloud Gateway et comment le configurer ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Une passerelle réactive (WebFlux, ou variante MVC) : routes définies en YAML ou Java (predicates sur path/host/header, filters : réécriture, rate limiting Redis, circuit breaker, ajout de headers, relais du token OAuth2). Elle centralise l'authentification, l'observabilité et le routage vers les microservices.

### 92. Qu'est-ce que Spring Cloud Stream ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Une abstraction de messagerie : des fonctions `Function<In,Out>`, `Consumer`, `Supplier` déclarées en beans, liées à des destinations Kafka/RabbitMQ/Pulsar par configuration (`spring.cloud.stream.bindings`). Elle gère sérialisation, groupes de consommateurs, partitions, DLQ et retries, permettant de changer de broker sans modifier le code métier.

### 93. Qu'est-ce que Spring Cloud Function ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Un modèle où la logique métier est exprimée en `Function`/`Consumer`/`Supplier` Java, déployable comme endpoint HTTP, consommateur de messages, ou fonction serverless (AWS Lambda, Azure Functions, GCP) grâce à des adaptateurs. Il évite de coupler le code au fournisseur et facilite les tests unitaires.

### 94. Comment gérer les secrets dans une application Spring Cloud ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Ne jamais les mettre dans `application.yml` versionné : variables d'environnement injectées par Kubernetes (Secrets/External Secrets), Spring Cloud Vault (`spring.config.import=vault://`), AWS Secrets Manager/Parameter Store via Spring Cloud AWS, ou Config Server avec chiffrement (`{cipher}`). Rotation sans redémarrage avec `@RefreshScope` ou un rechargement de `DataSource`.

### 95. Qu'est-ce que le pattern Circuit Breaker avec Spring Cloud CircuitBreaker ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Une abstraction (`CircuitBreakerFactory`) sur Resilience4j : `cb.run(() -> appel, throwable -> fallback)`. États fermé/ouvert/semi-ouvert selon un taux d'échec sur une fenêtre glissante. Combiner avec timeouts, retries limités, bulkhead, et exposer les métriques Micrometer (`resilience4j_circuitbreaker_state`).

### 96. Comment fonctionne le versioning d'API dans Spring Framework 7 ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Spring 7 (Boot 4) introduit le support natif du versioning : `@GetMapping(version = "1.1")`, résolution de la version par header, paramètre, path ou media type (`ApiVersionConfigurer`), avec sémantique de versions (`1.1+`) et validation des versions supportées. Il remplace les solutions maison basées sur des chemins ou des headers personnalisés.

### 97. Qu'est-ce que Spring Modulith ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un projet structurant un monolithe en modules explicites (un package de premier niveau = un module) : vérification des dépendances entre modules par test (`ApplicationModules.verify()`), événements de domaine persistés (event publication registry) pour l'intégration asynchrone entre modules, documentation générée (C4), et tests par module (`@ApplicationModuleTest`). Alternative crédible aux microservices prématurés.

### 98. Comment exposer des métriques métier personnalisées avec Micrometer ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Injecter `MeterRegistry` et créer `Counter`, `Timer`, `Gauge`, `DistributionSummary` avec des tags à faible cardinalité (`orders.created{country=FR}`), ou annoter `@Timed`/`@Counted`. Utiliser l'API `Observation` (`Observation.createNotStarted("order.process", registry).observe(...)`) pour obtenir métriques et trace en une seule instrumentation. Éviter les tags à forte cardinalité (id utilisateur).

### 99. Quelles sont les bonnes pratiques de structuration d'un projet Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Package par fonctionnalité (`order`, `customer`) plutôt que par couche technique, classe `@SpringBootApplication` à la racine pour le scan, visibilité package-private pour limiter l'exposition (facilité par Spring Modulith), DTO distincts des entités, `@ConfigurationProperties` typées, exceptions métier centralisées, et tests par tranche à côté de quelques tests d'intégration complets.

### 100. Comment migrer une application de Spring Boot 2.x vers 3.x ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Passer par la dernière 2.7, Java 17+, puis migrer `javax.*` → `jakarta.*` (OpenRewrite automatise), mettre à jour les dépendances (Hibernate 6, Spring Security 6 sans `WebSecurityConfigurerAdapter`, `authorizeHttpRequests`), les propriétés renommées (`spring-boot-properties-migrator`), la trailing slash matching (désactivé), et Micrometer Tracing à la place de Sleuth. Tester exhaustivement, notamment JPA (changements de génération SQL).
