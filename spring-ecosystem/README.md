# 🌱 Spring Ecosystem

> Spring Core, Boot, Data, Batch, Cloud, Security, Actuator

**300 questions**

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

### 101. Comment Spring MVC traite-t-il une requête HTTP de bout en bout ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `DispatcherServlet` reçoit la requête, consulte les `HandlerMapping` pour trouver le contrôleur, exécute les `HandlerInterceptor` (`preHandle`), résout les arguments (`HandlerMethodArgumentResolver` : `@PathVariable`, `@RequestBody` via `HttpMessageConverter`), appelle la méthode, convertit le retour (`@ResponseBody` → JSON) ou résout une vue, gère les exceptions (`HandlerExceptionResolver`, `@ControllerAdvice`), puis `postHandle`/`afterCompletion`.

### 102. Différence entre `@Controller` et `@RestController`, `@RequestParam` et `@PathVariable` ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `@RestController` = `@Controller` + `@ResponseBody` : le retour est sérialisé dans le corps au lieu d'être un nom de vue. `@PathVariable` lit un segment d'URL (`/users/{id}`), `@RequestParam` un paramètre de query string ou de formulaire (`?page=2`), avec `required`, `defaultValue` et conversion de type automatique.

### 103. Comment fonctionnent les `HttpMessageConverter` et comment en ajouter un ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Ils convertissent le corps des requêtes/réponses selon `Content-Type`/`Accept` : Jackson pour JSON, XML, `String`, `byte[]`, Protobuf. Boot les auto-configure ; on personnalise via `WebMvcConfigurer.extendMessageConverters` ou un bean `Jackson2ObjectMapperBuilderCustomizer` (dates ISO, `NON_NULL`, modules). Une erreur 415 signale l'absence de converter pour le type demandé.

### 104. Qu'est-ce qu'un `HandlerInterceptor` et quelle différence avec un `Filter` ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Un `Filter` (Servlet) s'exécute avant le `DispatcherServlet`, sans connaissance du contrôleur, pour les préoccupations transverses bas niveau (sécurité, logs bruts, CORS). Un `HandlerInterceptor` s'exécute autour de la méthode de contrôleur avec accès au handler choisi (audit, métriques par endpoint, vérification de headers métier). Les deux se déclarent en beans ; l'ordre se contrôle par `@Order`/`addInterceptors`.

### 105. Comment gérer les uploads de fichiers ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `@RequestParam MultipartFile file` ou `@RequestPart`, avec `spring.servlet.multipart.max-file-size`/`max-request-size`. Streamer vers le stockage (`file.getInputStream()`) plutôt que charger en mémoire, valider type et taille, générer un nom sûr, et pour les gros fichiers préférer un upload direct vers S3 via URL présignée.

### 106. Comment renvoyer un fichier ou un flux volumineux sans saturer la mémoire ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Retourner `ResponseEntity<StreamingResponseBody>` ou `Resource` (`InputStreamResource`) avec `Content-Disposition` et `Content-Type`, en écrivant par blocs. Pour les réponses longues, `ResponseBodyEmitter`/`SseEmitter` ou `Flux` avec WebFlux. Éviter `byte[]` sur des fichiers de plusieurs Mo.

### 107. Comment fonctionnent la négociation de contenu et le versioning d'API ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Le `ContentNegotiationManager` choisit le format selon `Accept` (ou un paramètre), et `produces`/`consumes` sur les mappings filtrent. Versioning classique : préfixe d'URL (`/v1`), header (`X-API-Version`), ou media type (`application/vnd.app.v2+json`) ; Spring 7 le rend natif (`version` sur les mappings). Toujours documenter la politique de dépréciation.

### 108. Qu'est-ce que `@ResponseStatus`, `ResponseEntity` et comment choisir ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `ResponseEntity<T>` contrôle statut, headers et corps par requête (201 avec `Location`, 204). `@ResponseStatus` fixe un statut par défaut sur une méthode ou une classe d'exception. Pour les APIs, `ResponseEntity` (ou le retour direct pour le 200) plus un `@RestControllerAdvice` pour les erreurs est le duo standard.

### 109. Comment fonctionne le traitement asynchrone dans Spring MVC (`Callable`, `DeferredResult`) ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Un contrôleur retournant `Callable`, `DeferredResult` ou `CompletableFuture` libère le thread Tomcat pendant le traitement ; la réponse est écrite quand le résultat est disponible (`spring.mvc.async.request-timeout`). Utile pour les long-polling et appels lents ; avec les virtual threads, le simple code bloquant devient souvent suffisant.

### 110. Comment sécuriser et documenter une API avec OpenAPI (springdoc) ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `springdoc-openapi-starter-webmvc-ui` génère la spécification à partir des contrôleurs et annotations (`@Operation`, `@Schema`, `@Parameter`) et sert Swagger UI. Bonnes pratiques : groupes par version, schémas de sécurité déclarés (Bearer), exemples, désactivation ou protection de l'UI en production, et contrôle en CI de la compatibilité du contrat (openapi-diff).

### 111. Qu'est-ce que Spring WebFlux et quand le choisir plutôt que Spring MVC ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** Une pile réactive non bloquante (Reactor, Netty) exposant `Mono`/`Flux`. À choisir pour les gateways, le streaming, l'agrégation d'appels massivement concurrents ou les clients réactifs de bout en bout (R2DBC, Kafka réactif). Sinon MVC + virtual threads reste plus simple à écrire, tester et déboguer.

### 112. Différence entre `Mono` et `Flux`, et qu'est-ce que la backpressure ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** `Mono<T>` : 0 ou 1 élément ; `Flux<T>` : 0..n. Rien ne s'exécute avant `subscribe()`. La backpressure permet au consommateur de demander n éléments (`request(n)`) pour ne pas être submergé ; les opérateurs `onBackpressureBuffer/Drop/Latest` gèrent les producteurs plus rapides.

### 113. Quels sont les pièges classiques en programmation réactive avec Spring ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** Appel bloquant dans une chaîne (JDBC, `Thread.sleep`, `block()`) : utiliser `Schedulers.boundedElastic` ou BlockHound pour détecter ; perte du `MDC`/contexte (utiliser `Context`, Micrometer context propagation) ; oublier de s'abonner ; exceptions avalées ; `flatMap` sans limite de concurrence ; tests avec `StepVerifier` négligés.

### 114. Comment gérer la transaction et la persistance réactive (R2DBC) ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** `spring-boot-starter-data-r2dbc` avec `ReactiveCrudRepository`, `DatabaseClient`, et `@Transactional` supporté par `ReactiveTransactionManager` (contexte transactionnel propagé dans le `Context` Reactor). Pas de lazy loading ni de relations JPA : modéliser en agrégats simples ou utiliser des jointures explicites.

### 115. Comment exposer du Server-Sent Events et des WebSockets ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** SSE : endpoint retournant `Flux<ServerSentEvent<T>>` avec `produces = TEXT_EVENT_STREAM_VALUE` (MVC supporte aussi via `SseEmitter`). WebSocket : `WebSocketHandler` réactif et `SimpleUrlHandlerMapping`, ou en MVC `spring-websocket` avec STOMP et un broker (`@MessageMapping`, `SimpMessagingTemplate`, relais RabbitMQ pour le multi-instances).

### 116. Comment fonctionne `SpringApplication` et que peut-on personnaliser au démarrage ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `SpringApplication.run` crée l'`ApplicationContext` adapté (servlet, réactif, none), charge l'`Environment`, applique les `ApplicationContextInitializer` et `ApplicationListener` (`spring.factories`/`META-INF/spring/*.imports`), affiche la bannière, rafraîchit le contexte, exécute `CommandLineRunner`/`ApplicationRunner`. On personnalise via `SpringApplicationBuilder` (profils, propriétés par défaut, `web(NONE)`, `lazyInitialization`).

### 117. Différence entre `CommandLineRunner`, `ApplicationRunner` et `@EventListener(ApplicationReadyEvent)` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Les runners s'exécutent après le démarrage du contexte mais avant que l'application ne soit signalée prête ; `ApplicationRunner` reçoit des arguments parsés. `ApplicationReadyEvent` est publié une fois l'application prête à servir (après les runners) : préférable pour du warm-up ou des notifications. Une exception dans un runner arrête l'application.

### 118. Comment structurer les propriétés avec `@ConfigurationProperties` imbriquées, listes et validation ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un record ou une classe (`@ConfigurationProperties(prefix="app.mail")`) avec champs imbriqués, `List<T>`, `Map<String,T>`, `Duration`/`DataSize` convertis automatiquement (`10s`, `5MB`), `@Validated` + contraintes Bean Validation, `@DefaultValue`. Activer avec `@EnableConfigurationProperties` ou `@ConfigurationPropertiesScan` ; le processor génère la métadonnée pour l'autocomplétion IDE.

### 119. Comment gérer la configuration par environnement sans profils multiples ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un seul `application.yml` avec des placeholders `${DB_URL}` résolus par variables d'environnement (12-factor), plus `application-local.yml` pour le poste du développeur. Les profils restent utiles pour des beans différents (mocks, adaptateurs), pas pour dupliquer des valeurs. `spring.config.import` charge des fichiers externes ou Vault/Config Server.

### 120. Que sont les `spring.factories` / `AutoConfiguration.imports` et comment fonctionne l'ordre des auto-configurations ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Les auto-configurations sont listées dans `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` et chargées après les configurations utilisateur, ordonnées par `@AutoConfigureBefore/After/Order`. Elles utilisent `@ConditionalOnMissingBean` pour se retirer si l'utilisateur fournit son bean. `--debug` ou Actuator `/conditions` affichent ce qui a été appliqué et pourquoi.

### 121. Comment écrire une auto-configuration réutilisable dans un starter d'entreprise ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Module `xxx-spring-boot-autoconfigure` avec classes `@AutoConfiguration` conditionnelles, `@ConfigurationProperties` documentées, métadonnées (`additional-spring-configuration-metadata.json`), et un module `xxx-spring-boot-starter` ne contenant que les dépendances. Tester avec `ApplicationContextRunner` (conditions, remplacement par l'utilisateur). Ne pas faire de scan de composants dans une auto-configuration.

### 122. Comment tester une auto-configuration avec `ApplicationContextRunner` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `new ApplicationContextRunner().withConfiguration(AutoConfigurations.of(MyAutoConfig.class)).withPropertyValues("app.x=1").run(ctx -> assertThat(ctx).hasSingleBean(X.class))`. On vérifie aussi les cas où une classe est absente (`withClassLoader(new FilteredClassLoader(...))`) et où l'utilisateur fournit son propre bean (`withUserConfiguration`).

### 123. Que fournit Actuator au-delà de `/health` et `/metrics` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `/info` (build, git), `/env` et `/configprops` (configuration effective, valeurs sensibles masquées), `/beans`, `/conditions`, `/mappings`, `/loggers` (changer un niveau à chaud), `/threaddump`, `/heapdump`, `/prometheus`, `/scheduledtasks`, `/startup`, `/sbom` (Boot 3.3). Exposer sélectivement (`management.endpoints.web.exposure.include`) et sur un port de management séparé.

### 124. Comment écrire un `HealthIndicator` personnalisé et l'intégrer aux probes Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un bean implémentant `HealthIndicator` (ou `ReactiveHealthIndicator`) retournant `Health.up()/down().withDetail(...)`. Les groupes `management.endpoint.health.group.readiness.include=readinessState,db` composent les probes ; une dépendance externe non critique ne doit pas rendre le Pod non-ready ni le redémarrer (liveness minimale).

### 125. Comment fonctionne le graceful shutdown dans Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `server.shutdown=graceful` + `spring.lifecycle.timeout-per-shutdown-phase=30s` : à SIGTERM, le serveur cesse d'accepter des connexions et laisse finir les requêtes en cours avant d'arrêter le contexte (`SmartLifecycle` phases). Sous Kubernetes, combiner avec la readiness passant à `false` et un `preStop` pour laisser le temps aux Endpoints d'être mis à jour.

### 126. Comment personnaliser Tomcat embarqué (threads, timeouts, compression, HTTP/2) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Propriétés `server.tomcat.threads.max`, `server.tomcat.accept-count`, `server.tomcat.connection-timeout`, `server.compression.enabled`, `server.http2.enabled` (avec TLS), `server.max-http-request-header-size`, accès aux logs `server.tomcat.accesslog.*`. Pour aller plus loin, un `WebServerFactoryCustomizer<TomcatServletWebServerFactory>`. Jetty et Undertow sont interchangeables via les starters.

### 127. Qu'est-ce que Spring Boot AOT et comment préparer une application pour GraalVM Native ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-boot:process-aot` génère à la compilation le code d'enregistrement des beans et les hints de réflexion, ce qui supprime la découverte dynamique au démarrage. Pour Native Image : `native-maven-plugin` ou Buildpacks (`-Pnative`), éviter la réflexion non déclarée (`@RegisterReflectionForBinding`, `RuntimeHintsRegistrar`), tester en natif (les proxies CGLIB et certaines bibliothèques exigent des hints). Gains : démarrage < 100 ms, mémoire réduite ; coût : build long, débogage plus difficile.

### 128. Comment gérer les dépendances et versions avec le BOM Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Le parent `spring-boot-starter-parent` (ou l'import `spring-boot-dependencies` en BOM) fixe les versions cohérentes de centaines de bibliothèques ; on ne déclare pas de version pour les dépendances gérées, et on surcharge via des propriétés (`<jackson-bom.version>`) avec prudence. Spring Cloud a son propre BOM à aligner avec la version Boot (tableau de compatibilité).

### 129. Comment gérer les erreurs de `JSON` malformé, types invalides et enums inconnus ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Elles produisent `HttpMessageNotReadableException` (400) : les intercepter dans le `@RestControllerAdvice` pour renvoyer un `ProblemDetail` lisible sans exposer la stack. Configurer Jackson : `FAIL_ON_UNKNOWN_PROPERTIES=false` si tolérant, `READ_UNKNOWN_ENUM_VALUES_AS_NULL`, `@JsonFormat` pour les dates, et valider ensuite avec Bean Validation.

### 130. Comment fonctionnent les `@JsonView`, `@JsonIgnore` et les DTO dans une API Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@JsonIgnore`/`@JsonIgnoreProperties` masquent des champs, `@JsonView` expose des vues différentes d'un même objet selon le contrôleur. En pratique, des DTO dédiés (records) par cas d'usage sont plus clairs, évitent d'exposer des entités JPA (lazy loading, récursion, fuite de champs) et découplent l'API du modèle.

### 131. Comment implémenter un repository personnalisé (fragment) ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Déclarer une interface `OrderRepositoryCustom` avec sa classe `OrderRepositoryImpl` (suffixe `Impl` obligatoire) utilisant `EntityManager`, `JdbcClient` ou Querydsl, puis faire hériter `OrderRepository extends JpaRepository<Order, Long>, OrderRepositoryCustom`. Spring Data compose les fragments ; utile pour les requêtes dynamiques ou les projections complexes.

### 132. Différence entre projections interface, class (DTO) et dynamiques ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Interface : getters correspondant aux colonnes (proxy, supporte SpEL et projections imbriquées). Class/record : constructeur DTO, requête `SELECT new` optimisée. Dynamique : `<T> List<T> findByStatus(String s, Class<T> type)` choisit la projection à l'appel. Les projections évitent de charger des entités complètes et de déclencher le lazy loading.

### 133. Comment utiliser Querydsl ou JPA Criteria pour des filtres dynamiques ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `Specification<T>` (Criteria API) composable (`where(hasStatus(s)).and(createdAfter(d))`), ou Querydsl avec Q-classes générées (`QOrder.order.status.eq(s)`), typé et lisible, via `QuerydslPredicateExecutor`. Les deux évitent la concaténation de JPQL ; Querydsl reste le plus agréable pour les recherches multi-critères.

### 134. Comment fonctionne le `EntityManager` et le contexte de persistance dans une transaction Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Spring injecte un proxy `@PersistenceContext` lié à la transaction courante : les entités chargées sont gérées (dirty checking, cache de premier niveau) jusqu'au commit/flush. Hors transaction (ou avec `open-in-view=false` après le service), les entités sont détachées : accéder à une relation lazy lève `LazyInitializationException`. `flush()` synchronise sans committer ; `clear()` vide le contexte (imports massifs).

### 135. Qu'est-ce que `@Version`, `@DynamicUpdate`, `@Immutable` et quand les utiliser ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `@Version` : verrouillage optimiste (échec `ObjectOptimisticLockingFailureException` à convertir en 409). `@DynamicUpdate` : `UPDATE` ne contenant que les colonnes modifiées (utile pour de grosses tables, coût de génération SQL). `@Immutable` : entité en lecture seule, Hibernate ignore les modifications et optimise. Les records/DTO restent préférables aux entités immuables pour la lecture.

### 136. Comment gérer les relations bidirectionnelles et les cascades sans pièges ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Définir le côté propriétaire (`@JoinColumn`) et `mappedBy` de l'autre côté, maintenir les deux côtés via des méthodes utilitaires (`addItem`), `cascade = ALL` + `orphanRemoval` uniquement sur les compositions (agrégat), jamais sur `@ManyToMany`. Exclure les relations de `toString`/`equals`/`hashCode` (boucles, chargements lazy) ; baser `equals` sur un identifiant métier ou l'id une fois assigné.

### 137. Comment implémenter la recherche full-text ou géospatiale avec Spring Data ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** PostgreSQL : `@Query` native avec `to_tsvector`/`@@` ou PostGIS, mappage des types via Hibernate Spatial ou colonnes JSONB (`@JdbcTypeCode(SqlTypes.JSON)`). Sinon Spring Data Elasticsearch/OpenSearch avec `@Document` et repositories dédiés, synchronisés depuis la base par événements ou CDC. Éviter `LIKE '%x%'` sur de grands volumes.

### 138. Comment gérer le soft delete et le multi-tenant avec Hibernate ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Hibernate 6.4+ : `@SoftDelete` sur l'entité (colonne booléenne ou timestamp, filtrée automatiquement). Multi-tenant : `@TenantId` sur une colonne + `CurrentTenantIdentifierResolver`, ou schéma/base par tenant via `MultiTenantConnectionProvider`. Vérifier les requêtes natives et les jointures qui contournent ces filtres.

### 139. Comment utiliser Spring Data avec MongoDB et Redis ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** MongoDB : `@Document`, `MongoRepository`, `MongoTemplate` pour les agrégations, index déclarés (`@Indexed`, auto-index-creation à désactiver en prod), transactions multi-documents sur replica set. Redis : `RedisTemplate`/`StringRedisTemplate` avec sérialiseurs configurés (JSON), `@RedisHash` pour les objets, Spring Cache avec TTL, Spring Session, pub/sub et streams via `ReactiveRedisTemplate`.

### 140. Qu'est-ce que Spring Data REST et pourquoi est-il rarement utilisé en production ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Il expose automatiquement les repositories en API HATEOAS (`/orders`, pagination, recherche par query methods). Pratique pour un prototype ou un back-office, mais il couple l'API au modèle de données, complique les règles métier, la validation et la sécurité fine. Pour une API publique, préférer des contrôleurs et DTO explicites.

### 141. Comment fonctionne le `SecurityContextHolder` et sa propagation aux threads asynchrones ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Le contexte d'authentification est stocké par défaut dans un `ThreadLocal` (stratégie `MODE_THREADLOCAL`) ; il n'est pas transmis aux threads d'un pool. Solutions : `MODE_INHERITABLETHREADLOCAL` (risqué avec les pools), `DelegatingSecurityContextExecutor`/`DelegatingSecurityContextAsyncTaskExecutor`, ou propagation explicite. Avec WebFlux, `ReactiveSecurityContextHolder` via le `Context`.

### 142. Comment implémenter une authentification personnalisée (API key, header interne) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Un `OncePerRequestFilter` qui lit le header, valide la clé (service, cache), construit un `Authentication` (`UsernamePasswordAuthenticationToken` authentifié avec autorités) et le place dans le `SecurityContext`, ajouté via `http.addFilterBefore(filter, UsernamePasswordAuthenticationFilter.class)`. Ou un `AuthenticationProvider` dédié avec un `AuthenticationManager`. Toujours répondre 401 propre en cas d'échec via `AuthenticationEntryPoint`.

### 143. Comment gérer les autorisations par requête avec `authorizeHttpRequests` ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `http.authorizeHttpRequests(a -> a.requestMatchers("/admin/**").hasRole("ADMIN").requestMatchers(HttpMethod.GET, "/public/**").permitAll().anyRequest().authenticated())` ; l'ordre compte (première règle correspondante). Depuis Security 6, `requestMatchers` déduit MVC/AntPath ; utiliser `PathPatternRequestMatcher` explicite en cas de plusieurs servlets. Préférer la sécurité par défaut « deny » + ouverture explicite.

### 144. Comment fonctionnent `@PreAuthorize` avec SpEL avancé et les `PermissionEvaluator` ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `@PreAuthorize("hasRole('ADMIN') or #order.ownerId == authentication.name")` accède aux paramètres, à l'authentification et à des beans (`@authz.canEdit(#id)`). `hasPermission(#id, 'Order', 'WRITE')` délègue à un `PermissionEvaluator` centralisant les règles. `@PostAuthorize`/`@PostFilter` agissent sur le retour. Activer avec `@EnableMethodSecurity`.

### 145. Comment protéger contre les attaques courantes avec Spring Security (headers, CSRF, session) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Headers par défaut : `X-Content-Type-Options`, `X-Frame-Options`, `Cache-Control`, HSTS ; ajouter une CSP (`http.headers(h -> h.contentSecurityPolicy(...))`). CSRF activé pour les sessions (token `XSRF-TOKEN` pour les SPA avec `CookieCsrfTokenRepository`), gestion de session (`sessionFixation().migrateSession()`, `maximumSessions(1)`), `requiresChannel` HTTPS, et limitation des tentatives par un filtre/`AuthenticationFailureHandler` + cache.

### 146. Comment intégrer Spring Security avec un frontend Angular (SPA) hébergé séparément ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Deux options : (1) Resource Server JWT : Angular obtient le jeton via OIDC (code + PKCE) et l'envoie en `Authorization: Bearer` ; CORS configuré, CSRF désactivé, stateless. (2) BFF : Spring Cloud Gateway ou Boot en client OIDC avec session cookie, CSRF cookie `XSRF-TOKEN` lu par Angular (`withXsrfConfiguration`), `TokenRelay` vers les APIs. La seconde est plus sûre pour le navigateur.

### 147. Comment gérer la déconnexion et l'expiration des jetons côté Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Sessions : `http.logout()` invalide la session, supprime les cookies, redirige ; avec OIDC client, `OidcClientInitiatedLogoutSuccessHandler` déconnecte aussi l'IdP ; back-channel logout supporté depuis Security 6.2. JWT : expiration courte, refresh côté client, et si révocation immédiate nécessaire, introspection (`opaqueToken()`) ou denylist consultée dans un `OAuth2TokenValidator`.

### 148. Qu'est-ce que le `OAuth2AuthorizedClientManager` et comment appeler une API en aval avec le jeton de l'utilisateur ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Il obtient/rafraîchit les access tokens des clients enregistrés. Avec `RestClient`/`WebClient`, ajouter l'intercepteur `OAuth2ClientHttpRequestInterceptor` (Security 6.4) ou `ServletOAuth2AuthorizedClientExchangeFilterFunction` : le jeton de l'utilisateur courant (ou client credentials) est ajouté automatiquement et rafraîchi. C'est le cœur du pattern BFF/TokenRelay.

### 149. Comment auditer et journaliser les événements de sécurité ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Spring publie des `AuthenticationSuccessEvent`, `AbstractAuthenticationFailureEvent`, `AuthorizationDeniedEvent` (avec `AuthorizationEventPublisher`) : les écouter pour tracer connexions, échecs et refus dans des logs structurés ou un SIEM. Actuator `/auditevents` avec `AuditEventRepository` conserve un historique en mémoire ; en production, envoyer vers un stockage durable.

### 150. Comment configurer un job Spring Batch avec Boot 3 (sans `@EnableBatchProcessing`) ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Boot 3 auto-configure `JobRepository`, `JobLauncher` et le `DataSource` ; on déclare des beans `Job` et `Step` avec `JobBuilder(name, jobRepository)` et `StepBuilder(...).<I,O>chunk(size, transactionManager).reader().processor().writer().build()`. `@EnableBatchProcessing` désactive désormais l'auto-configuration. `spring.batch.jdbc.initialize-schema=always` crée les tables de métadonnées.

### 151. Quels readers et writers standards connaître ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Readers : `FlatFileItemReader` (CSV), `JdbcCursorItemReader`/`JdbcPagingItemReader`, `JpaPagingItemReader`, `KafkaItemReader`, `JsonItemReader`, `StaxEventItemReader` (XML). Writers : `JdbcBatchItemWriter`, `JpaItemWriter`, `FlatFileItemWriter`, `KafkaItemWriter`, `CompositeItemWriter`. Préférer les readers paginés ou par curseur aux chargements complets en mémoire.

### 152. Comment gérer les erreurs : skip, retry, restart et `ExecutionContext` ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** `.faultTolerant().skip(ParseException.class).skipLimit(100).retry(DeadlockLoserDataAccessException.class).retryLimit(3)` avec `SkipListener` pour journaliser. Le restart reprend au dernier chunk committé grâce à l'`ExecutionContext` persisté par les readers stateful (ligne courante, dernier id). Les `JobParameters` identifient l'instance : un job terminé COMPLETED ne se relance pas avec les mêmes paramètres (ajouter un `run.id` incrémental si voulu).

### 153. Comment paralléliser un job Spring Batch ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Multi-threaded step (`taskExecutor`, readers thread-safe seulement), parallel steps (`split` en flow), partitioning (`Partitioner` découpe par plage d'ids, chaque partition exécutée localement ou à distance), remote chunking (workers via messagerie). Le partitioning local est le plus courant ; l'écriture doit tolérer la concurrence.

### 154. Comment planifier, monitorer et exploiter des jobs Spring Batch ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Lancer via `JobLauncher` sur `@Scheduled`, un CronJob Kubernetes (`spring.batch.job.name` + arrêt de l'application), ou un orchestrateur (Airflow). Monitorer avec les tables de métadonnées (`BATCH_JOB_EXECUTION`, statut, durée, exceptions), les métriques Micrometer `spring.batch.*`, et des `JobExecutionListener` pour alerter. Purger périodiquement les métadonnées.

### 155. Comment fonctionne Spring Cloud Config Server et le rafraîchissement à chaud ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Le serveur sert la configuration depuis Git/Vault/base par application et profil (`/app/prod`) ; les clients l'importent (`spring.config.import=configserver:`). `@RefreshScope` recrée les beans concernés à `POST /actuator/refresh` ; Spring Cloud Bus (Kafka/RabbitMQ) propage le refresh à toutes les instances. Les `@ConfigurationProperties` se rafraîchissent automatiquement.

### 156. Qu'est-ce qu'OpenFeign et comment le configurer proprement ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Un client HTTP déclaratif (`@FeignClient(name, url)`) intégré à Spring Cloud : load balancing, décodeurs d'erreurs (`ErrorDecoder`), intercepteurs (token), timeouts et retries par client, circuit breaker via `spring.cloud.openfeign.circuitbreaker.enabled`. Feign est en maintenance ; pour les nouveaux projets, les interfaces `@HttpExchange` de Spring sont l'alternative recommandée.

### 157. Comment gérer la découverte de services sur Kubernetes sans Eureka ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Le DNS et les Services Kubernetes suffisent : appeler `http://orders-service` ; Spring Cloud Kubernetes peut charger ConfigMaps/Secrets et exposer un `DiscoveryClient` sur l'API Kubernetes, mais il ajoute des permissions RBAC. Eureka/Consul restent pertinents hors Kubernetes ou pour du client-side load balancing fin.

### 158. Comment implémenter un rate limiter et un circuit breaker dans Spring Cloud Gateway ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Filtre `RequestRateLimiter` avec `RedisRateLimiter` (replenishRate, burstCapacity) et un `KeyResolver` (utilisateur, IP, API key) ; filtre `CircuitBreaker` (Resilience4j) avec `fallbackUri`. Ajouter `Retry` (méthodes idempotentes seulement), timeouts par route (`metadata.response-timeout`), et exposer les métriques.

### 159. Qu'est-ce que Spring Cloud Contract ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Le contract testing : un contrat (Groovy/YAML) décrit requête/réponse ; côté producteur, des tests générés vérifient que l'API respecte le contrat ; côté consommateur, un stub (WireMock) généré à partir du même contrat permet de tester sans le service réel. Il détecte les ruptures de contrat en CI avant l'intégration.

### 160. Comment gérer les transactions distribuées entre microservices Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Cloud**

**Réponse :** Éviter XA/JTA : préférer la saga (chorégraphie par événements Kafka ou orchestration via un service/Temporal), l'outbox transactionnel (écrire l'événement dans la même transaction que la donnée, publié ensuite par un relais ou Debezium), l'idempotence des consommateurs, et la compensation. Spring Modulith fournit un event publication registry pour l'outbox intra-application.

### 161. Comment implémenter le pattern Outbox avec Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Dans la transaction métier, insérer une ligne `outbox` (id, agrégat, type, payload JSON). Un `@Scheduled` (avec `SKIP LOCKED` pour le multi-instances) ou Debezium lit et publie vers Kafka puis marque/supprime la ligne ; les consommateurs dédupliquent par id d'événement. `@TransactionalEventListener(AFTER_COMMIT)` seul ne suffit pas (perte possible en cas de crash après commit).

### 162. Comment intégrer Kafka dans Spring Boot (Spring Kafka) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-kafka` : `KafkaTemplate` pour produire (sérialiseurs JSON, `ProducerListener`), `@KafkaListener(topics, groupId, concurrency)` pour consommer avec conteneurs, `DefaultErrorHandler` (backoff, DLT via `DeadLetterPublishingRecoverer`), `@RetryableTopic`, transactions (`KafkaTransactionManager`), et tests avec `@EmbeddedKafka` ou Testcontainers. Configurer `ack-mode` et l'idempotence du producteur.

### 163. Comment intégrer RabbitMQ (Spring AMQP) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-boot-starter-amqp` : `RabbitTemplate` (publisher confirms, `MessageConverter` JSON), `@RabbitListener` sur des queues déclarées en beans (`Queue`, `Exchange`, `Binding`), acquittement manuel ou automatique, retries via `RetryTemplate`/dead-letter exchange avec TTL, prefetch pour le débit, et `RabbitListenerContainerFactory` concurrent. Idempotence côté consommateur comme avec Kafka.

### 164. Qu'est-ce que Spring Integration et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Une implémentation des Enterprise Integration Patterns (channels, transformers, routers, splitters, aggregators, adaptateurs fichiers/FTP/JMS/HTTP/Kafka) avec une DSL Java. Utile pour des flux d'intégration complexes (polling de répertoires SFTP, agrégation de messages), mais lourd pour un simple consommateur Kafka : Spring Kafka/Cloud Stream suffisent alors.

### 165. Comment envoyer des e-mails et générer des documents dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-boot-starter-mail` + `JavaMailSender` (SMTP configuré, `MimeMessageHelper` pour HTML et pièces jointes), gabarits Thymeleaf pour le corps, envoi asynchrone via file/`@Async` avec retry, et fournisseur transactionnel (SES, SendGrid) en production. Documents : OpenPDF/iText, JasperReports, ou HTML → PDF (openhtmltopdf) avec Thymeleaf.

### 166. Comment gérer les WebSockets/STOMP avec Spring MVC et le scaler ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@EnableWebSocketMessageBroker`, endpoint `registerStompEndpoints`, broker simple en mémoire ou relais vers RabbitMQ/ActiveMQ (`enableStompBrokerRelay`) pour partager les abonnements entre instances, `@MessageMapping` pour recevoir, `SimpMessagingTemplate.convertAndSendToUser` pour cibler un utilisateur. Sécuriser avec `AuthorizationManager` de messages et le handshake authentifié.

### 167. Comment implémenter un endpoint de long-running task avec suivi d'état ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Retourner 202 avec un identifiant et une URL de statut, exécuter le traitement dans une file (Kafka/RabbitMQ) ou un executor dédié, persister l'état (PENDING, RUNNING, DONE, FAILED, progression) en base/Redis, endpoint `GET /tasks/{id}` (ou SSE pour le temps réel), idempotence à la soumission, et nettoyage des tâches anciennes. Jamais de traitement long dans le thread de requête.

### 168. Comment fonctionne `RestClient` et comment le configurer (timeouts, intercepteurs, erreurs) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `RestClient.builder().baseUrl(...).requestFactory(factory avec timeouts).requestInterceptor(auth).defaultStatusHandler(...)` puis `.get().uri("/x/{id}", id).retrieve().body(Dto.class)`. Boot 3.4 fournit `RestClient.Builder` auto-configuré (`spring.http.client.*` pour les timeouts et le connecteur : JDK, Apache, Jetty). Un builder par service, jamais un client sans timeout.

### 169. Comment tester un client HTTP avec `@RestClientTest` et MockRestServiceServer/WireMock ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@RestClientTest(MyClient.class)` charge le client et un `MockRestServiceServer` pour stubber les réponses (`expect(requestTo(...)).andRespond(withSuccess(json, APPLICATION_JSON))`). Pour des scénarios plus réalistes (délais, pannes, TLS), WireMock (`wiremock-spring-boot`) en test d'intégration. Tester les erreurs (4xx/5xx, timeout) autant que le cas nominal.

### 170. Comment gérer les dates, fuseaux et formats dans une API Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Stocker en UTC (`Instant`/`OffsetDateTime`, colonnes `timestamptz`), exposer en ISO-8601 (`spring.jackson.serialization.write-dates-as-timestamps=false`, `@JsonFormat` si besoin), `spring.jackson.time-zone`, `@DateTimeFormat` pour les paramètres de requête, et fixer la timezone de la JVM/du conteneur (`TZ=UTC`) pour éviter les décalages entre environnements. Convertir vers le fuseau utilisateur uniquement à l'affichage.

### 171. Comment internationaliser les messages d'erreur et de validation ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `MessageSource` avec `messages_fr.properties`, `LocaleResolver` (header `Accept-Language`), messages de contraintes en `{app.validation.email}` résolus par le `LocalValidatorFactoryBean` lié au `MessageSource` (`spring.messages.basename`). Les codes d'erreur restent stables pour les clients ; seul le libellé est localisé.

### 172. Comment gérer les uploads et le stockage S3 avec Spring Cloud AWS ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-cloud-aws-starter-s3` fournit `S3Template` (upload/download, URLs présignées) et les credentials via la chaîne AWS (IRSA sur EKS, pas de clés en dur). Streamer les fichiers, définir le `Content-Type`, chiffrer côté serveur, et utiliser des URLs présignées pour les uploads directs depuis le navigateur.

### 173. Comment concevoir un service multi-tenant avec Spring (résolution du tenant, isolation) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Résoudre le tenant par sous-domaine, header ou claim du jeton dans un filtre, le stocker dans un `ThreadLocal`/`ScopedValue`, l'appliquer aux données (`@TenantId`, schéma ou `AbstractRoutingDataSource` par tenant), au cache (préfixe de clé), aux logs (MDC) et aux métriques (tag borné). Tester systématiquement les fuites inter-tenants.

### 174. Comment fonctionne `AbstractRoutingDataSource` et le routage lecture/écriture ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un `DataSource` qui choisit la source selon une clé de contexte (`determineCurrentLookupKey`) : tenant, ou lecture vs écriture. Pour router les lectures vers une réplique, utiliser `TransactionSynchronizationManager.isCurrentTransactionReadOnly()` avec `LazyConnectionDataSourceProxy` (sinon la connexion est prise avant que `readOnly` soit connu). Attention à la latence de réplication.

### 175. Comment implémenter des feature flags dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Propriétés `@ConfigurationProperties` rafraîchissables pour les cas simples, ou un fournisseur (Unleash, LaunchDarkly, OpenFeature SDK, Togglz) évalué par utilisateur/contexte avec cache local. Encapsuler dans un service (`features.isEnabled("new-checkout", ctx)`), utiliser `@ConditionalOnProperty` uniquement pour les beans au démarrage, et supprimer les flags obsolètes.

### 176. Comment gérer les migrations de base avec Flyway dans Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-boot-starter-flyway` (ou `flyway-database-postgresql` en Flyway 10) exécute `db/migration/V1__init.sql` au démarrage avant JPA ; `spring.jpa.hibernate.ddl-auto=validate` vérifie la cohérence. Bonnes pratiques : migrations immuables, une par changement, compatibles avec l'ancienne version de l'application (expand/contract), migrations Java pour les données complexes, `baseline-on-migrate` pour les bases existantes, et exécution en job séparé sur les gros déploiements.

### 177. Comment diagnostiquer un démarrage lent ou une application qui ne démarre pas ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Lire la première exception de la pile (souvent noyée sous les `BeanCreationException` imbriquées), `--debug` pour le rapport d'auto-configuration, Actuator `/startup` avec `BufferingApplicationStartup` pour le temps par étape, `spring.main.lazy-initialization` pour isoler, vérifier les connexions externes bloquantes (base, Kafka, Config Server) avec timeouts, et les migrations Flyway longues.

### 178. Comment gérer les `@Transactional` dans les tests et pourquoi peut-ce masquer des bugs ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@Transactional` sur un test annule la transaction à la fin (base propre), mais garde le contexte de persistance ouvert : le lazy loading fonctionne alors qu'il échouerait en production, les contraintes différées ne sont pas vérifiées, et les `@TransactionalEventListener` ne se déclenchent pas. Pour les tests d'intégration réalistes, préférer des données nettoyées explicitement (SQL de nettoyage, `@Sql`) sans transaction de test.

### 179. Comment utiliser `@Sql`, `@DirtiesContext` et les fixtures de test efficacement ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@Sql("/data.sql")` charge des données avant un test (ou `@SqlGroup`), `@Sql(executionPhase = AFTER_TEST_METHOD)` nettoie. `@DirtiesContext` force la recréation du contexte (lent : à éviter, préférer réinitialiser l'état). Testcontainers avec réutilisation (`withReuse(true)`) et un contexte partagé rendent la suite rapide ; fixtures via builders plutôt que gros fichiers SQL.

### 180. Comment fonctionne Micrometer Observation et comment instrumenter un service ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** L'API `Observation` unifie métriques et traces : `Observation.createNotStarted("order.place", registry).lowCardinalityKeyValue("type", t).observe(() -> ...)` ou `@Observed`. Boot 3 instrumente automatiquement MVC, RestClient, JDBC (avec datasource-micrometer), Kafka. Les `ObservationHandler` personnalisent ; les tags à forte cardinalité vont dans `highCardinalityKeyValue` (traces uniquement).

### 181. Comment propager le contexte de trace (traceId) dans les logs, threads et messages ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Micrometer Tracing (Brave ou OTel) place `traceId`/`spanId` dans le MDC (pattern de log), propage via les headers W3C `traceparent` dans RestClient/WebClient/Kafka automatiquement, et via `ContextPropagation`/`ContextSnapshot` pour les executors (`spring.task.execution` instrumenté). Vérifier la propagation dans `@Async` et les listeners Kafka avec `observation-enabled`.

### 182. Comment exporter traces et métriques vers OpenTelemetry ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `micrometer-tracing-bridge-otel` + `opentelemetry-exporter-otlp` avec `management.otlp.tracing.endpoint`, et `micrometer-registry-otlp` pour les métriques (ou Prometheus scrape). Alternative : l'agent Java OpenTelemetry (instrumentation sans code, plus complète) ; ne pas cumuler les deux. Régler l'échantillonnage (`management.tracing.sampling.probability`) en production.

### 183. Comment sécuriser une application Spring Boot en production (checklist) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Actuator restreint et sur port séparé, pas de `/env` exposé, secrets hors code, TLS ou proxy avec `forward-headers-strategy`, dépendances scannées (OWASP, Dependabot), CSP/HSTS, validation systématique, `ProblemDetail` sans stack, utilisateur non-root dans l'image, logs sans données sensibles, mise à jour régulière de Boot (CVE Spring), et tests de sécurité automatisés (ZAP en CI).

### 184. Comment construire un mono-repo multi-modules Spring Boot (Maven/Gradle) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un parent avec `dependencyManagement` (BOM Boot), des modules par domaine ou couche (`api`, `domain`, `infrastructure`, `app`), un seul module `app` avec le plugin Boot (`repackage`), les autres en jars ordinaires ; `spring-boot-starter-test` en scope test partout ; tests d'architecture (ArchUnit) pour les dépendances entre modules ; builds incrémentaux (Gradle) et cache CI.

### 185. Comment fonctionne Spring Shell et quand créer un outil CLI en Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Spring Shell 3 expose des commandes (`@Command`) avec complétion, aide, validation et interactivité, réutilisant les beans de l'application (services, repositories) : pratique pour des outils d'administration, migrations de données ou opérations de support. Pour des CLI légers, picocli (avec support Boot) démarre plus vite, surtout en natif.

### 186. Comment gérer les schémas d'événements et la sérialisation avec Spring Kafka et Avro/Protobuf ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Schema Registry (Confluent ou Apicurio) avec `KafkaAvroSerializer`/`KafkaProtobufSerializer`, classes générées au build (plugin Maven), compatibilité définie par sujet, et `specific.avro.reader=true` côté consommateur. Versionner les schémas comme du code, tester la compatibilité en CI, et éviter JSON sans schéma pour les contrats entre équipes.

### 187. Comment fonctionnent les `Converter`, `Formatter` et `PropertyEditor` dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Le `ConversionService` convertit types de paramètres et propriétés (`String` → `Enum`, `Duration`, objets personnalisés) via des `Converter<S,T>` déclarés en beans (`WebMvcConfigurer.addFormatters`) ; `Formatter` gère la localisation (dates, nombres). `@ConfigurationPropertiesBinding` sur un converter l'applique au binding de configuration. Utile pour des identifiants typés (`OrderId`) dans les contrôleurs.

### 188. Comment implémenter la pagination et le filtrage d'une API REST proprement ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Paramètres `page`/`size`/`sort` mappés sur `Pageable` (limiter `size` max via `spring.data.web.pageable.max-page-size`), réponse enveloppée (contenu, page, total) plutôt que `Page` brut, pagination par curseur (keyset) pour les grands volumes, filtres via un objet de critères validé + `Specification`, et documentation OpenAPI des paramètres. Ne pas exposer les noms de colonnes internes dans `sort`.

### 189. Comment gérer les gros volumes de lecture (export CSV de millions de lignes) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Streaming de bout en bout : `JdbcTemplate.queryForStream`/`Stream<T>` JPA avec `@QueryHints(fetchSize)` dans une transaction en lecture seule, écriture ligne à ligne dans `StreamingResponseBody` ou dans un fichier S3 puis lien de téléchargement (job asynchrone), `EntityManager.detach` ou `clear` périodiquement, compression gzip. Jamais `findAll()` en mémoire.

### 190. Comment utiliser les virtual threads avec JDBC, Kafka et `@Async` sans surprises ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** JDBC : la limite devient le pool HikariCP (dimensionner et surveiller `pending`). Kafka : les listeners restent limités par le nombre de partitions/concurrency. `@Async`/`@Scheduled` : `SimpleAsyncTaskExecutor` virtuel sans limite : borner avec un `Semaphore` ou `TaskDecorator`. Éviter les `ThreadLocal` lourds et les `synchronized` autour d'I/O (pinning avant Java 24) ; profiler avec JFR `VirtualThreadPinned`.

### 191. Comment faire du rate limiting côté application (Bucket4j, Resilience4j) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Bucket4j (token bucket, en mémoire ou distribué via Redis/Hazelcast) dans un filtre ou intercepteur, clé par utilisateur/API key, réponse 429 avec `Retry-After`. Resilience4j `RateLimiter` pour protéger un appel sortant vers un fournisseur à quota. Placer la limite globale dans la gateway et une limite fine par ressource dans le service.

### 192. Comment concevoir des événements de domaine avec Spring Modulith et les publier vers Kafka ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Publier des événements (`ApplicationEventPublisher`) dans la transaction ; Modulith les persiste (event publication registry) et les livre aux `@ApplicationModuleListener` (asynchrone, transactionnel, avec rejeu des non complétés au redémarrage). `@Externalized("orders.created")` publie automatiquement vers Kafka/AMQP/JMS, formant un outbox intégré.

### 193. Comment gérer les erreurs de désérialisation et les messages empoisonnés avec Spring Kafka ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `ErrorHandlingDeserializer` enveloppe le désérialiseur pour transformer une exception en `DeserializationException` traitée par le `DefaultErrorHandler` (au lieu d'une boucle infinie), envoi en DLT avec headers d'origine, backoff exponentiel, exceptions non réessayables (`addNotRetryableExceptions`), et alerte sur le DLT. Journaliser la clé et l'offset, jamais le payload sensible.

### 194. Comment gérer la configuration des timeouts de bout en bout (client, serveur, base, messagerie) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Définir un budget par requête et le décliner : `server.tomcat.connection-timeout`, `spring.mvc.async.request-timeout`, timeouts RestClient (connexion/lecture), `spring.datasource.hikari.connection-timeout` et `spring.transaction.default-timeout`, `@Transactional(timeout)`, `spring.kafka.producer.properties.delivery.timeout.ms`, timeouts du load balancer plus longs que ceux de l'application. Documenter la chaîne pour éviter les 504 mystérieux.

### 195. Comment faire coexister plusieurs versions d'une API et déprécier proprement ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Contrôleurs séparés par version partageant les services, DTO versionnés, header `Deprecation`/`Sunset` sur l'ancienne version, métriques d'usage par version pour décider du retrait, documentation OpenAPI par groupe, tests de contrat sur chaque version, et politique de support annoncée (par exemple N-1 pendant 6 mois).

### 196. Comment concevoir des tests d'architecture pour une application Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** ArchUnit : interdire les dépendances des couches domaine vers Spring/JPA (architecture hexagonale), vérifier que les contrôleurs n'appellent pas les repositories, que `@Transactional` est sur les services, nommage des packages, absence de `field injection`. Spring Modulith `verify()` pour les dépendances entre modules. Exécutés en CI comme des tests unitaires.

### 197. Comment mettre en place l'idempotence des endpoints POST ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un header `Idempotency-Key` obligatoire, stockage (Redis/base) de la clé avec l'état (en cours, terminé + réponse) et une contrainte unique pour gérer la concurrence, rejeu de la réponse enregistrée pour une clé déjà traitée, TTL de conservation, et association clé ↔ utilisateur pour éviter les collisions. Implémenté en filtre/intercepteur ou dans le service pour les opérations critiques (paiement).

### 198. Comment gérer le cache HTTP côté serveur avec Spring (ETag, `Cache-Control`) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `ShallowEtagHeaderFilter` calcule un ETag sur le corps (économise la bande passante, pas le calcul) ; mieux : ETag métier (version de l'entité) avec `ResponseEntity.ok().eTag(v).cacheControl(CacheControl.maxAge(...))` et `WebRequest.checkNotModified(etag)` pour répondre 304 sans charger. Pour les mises à jour, `If-Match` implémente le verrouillage optimiste HTTP (412 en cas de conflit).

### 199. Comment monitorer et alerter sur une application Spring Boot en production (indicateurs clés) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Taux d'erreur 5xx et latence p95/p99 par endpoint (`http.server.requests`), saturation des pools (Tomcat threads, HikariCP pending), GC et heap, lag Kafka, échecs de circuit breakers, health des dépendances, taux de logs ERROR, et métriques métier (commandes/min). Alertes basées sur des SLO (burn rate) plutôt que sur des seuils de CPU.

### 200. Quelles sont les nouveautés de Spring Boot 4 et Spring Framework 7 à connaître ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Java 17+ (21 recommandé), Jakarta EE 11, Jackson 3, modularisation des starters (`spring-boot-webmvc`, `spring-boot-jackson`), versioning d'API natif, `@HttpExchange` avec enregistrement simplifié, résilience intégrée (`@Retryable`, `@ConcurrencyLimit` dans le framework), Null-safety JSpecify, suppression des APIs dépréciées (`RestTemplate` reste mais `WebClient`/`RestClient` recommandés), et support renforcé de GraalVM/AOT. Vérifier le guide de migration officiel.

### 201. Qu'est-ce que l'`ApplicationContext` et quelles sont ses implémentations courantes ?
`🟢 Débutant` · Sujet : **Spring Core**

**Réponse :** Le conteneur IoC de Spring : il instancie, configure et assemble les beans, publie des événements, résout les messages (i18n) et les ressources. Implémentations : `AnnotationConfigApplicationContext` (config Java), `AnnotationConfigServletWebServerApplicationContext` (Boot MVC), `ReactiveWebServerApplicationContext` (WebFlux), `GenericApplicationContext` (AOT/native). `BeanFactory` est l'interface minimale sous-jacente.

### 202. Qu'est-ce que `@Configuration` avec `proxyBeanMethods` et pourquoi cela compte-t-il ?
`🟢 Débutant` · Sujet : **Spring Core**

**Réponse :** Une classe `@Configuration` est proxifiée (CGLIB) pour que les appels entre méthodes `@Bean` retournent le même singleton. `proxyBeanMethods = false` (lite mode) supprime le proxy : démarrage plus rapide et compatible natif, mais les appels directs entre méthodes `@Bean` créent de nouvelles instances ; il faut alors injecter les dépendances en paramètres de méthode. Boot utilise le lite mode dans ses auto-configurations.

### 203. Comment fonctionnent `@Primary`, `@Qualifier`, `@Order` et l'injection de collections ?
`🟢 Débutant` · Sujet : **Spring Core**

**Réponse :** Avec plusieurs beans d'un type, `@Primary` désigne le défaut, `@Qualifier("name")` (ou une annotation qualifier personnalisée) choisit explicitement. Injecter `List<Handler>` ou `Map<String, Handler>` récupère tous les beans du type, triés par `@Order`/`Ordered` : pattern courant pour les chaînes de traitement, stratégies et validateurs enfichables.

### 204. Différence entre `@PostConstruct`, `InitializingBean`, `@Bean(initMethod)` et `SmartLifecycle` ?
`🟢 Débutant` · Sujet : **Spring Core**

**Réponse :** `@PostConstruct` (standard, préféré) et `afterPropertiesSet` s'exécutent après l'injection des dépendances du bean ; `initMethod` pour les classes tierces. `SmartLifecycle` (`start`/`stop`, `getPhase`, `isAutoStartup`) s'exécute après le rafraîchissement complet du contexte, avec un ordre de phases, utile pour démarrer/arrêter proprement des consommateurs ou des serveurs (Spring Kafka l'utilise).

### 205. Qu'est-ce que `ObjectProvider` et l'injection paresseuse ?
`🟢 Débutant` · Sujet : **Spring Core**

**Réponse :** `ObjectProvider<T>` (ou `Optional<T>`, `@Autowired(required=false)`) permet d'obtenir un bean optionnel (`getIfAvailable`), unique (`getIfUnique`), ou de le résoudre tard (`getObject`) pour les prototypes et les dépendances circulaires. `@Lazy` sur un point d'injection injecte un proxy résolu au premier appel. Ils évitent les échecs au démarrage pour des dépendances facultatives.

### 206. Comment Spring résout-il les placeholders et SpEL (`@Value`, `#{}`) et quelles limites ?
`🟠 Intermédiaire` · Sujet : **Spring Core**

**Réponse :** `${prop:default}` est résolu par le `PropertySourcesPlaceholderConfigurer` depuis l'`Environment` ; `#{expr}` évalue du SpEL (accès aux beans, maths, conditions, `systemProperties`). `@Value` convient aux valeurs isolées ; pour des groupes de propriétés, `@ConfigurationProperties` est typé, validable et rechargeable. Éviter la logique dans SpEL et les `@Value` disséminés.

### 207. Qu'est-ce que `Environment`, `PropertySource` et comment ajouter une source de configuration personnalisée ?
`🟠 Intermédiaire` · Sujet : **Spring Core**

**Réponse :** L'`Environment` agrège des `PropertySource` ordonnées (ligne de commande, système, env, fichiers). Ajouter une source : `EnvironmentPostProcessor` (enregistré dans `spring.factories`, avant le contexte), ou `spring.config.import` avec un `ConfigDataLoader` personnalisé (Boot 2.4+) pour charger depuis une base, un service ou un format spécifique. Placer la source à la bonne priorité (`addFirst`/`addLast`).

### 208. Comment fonctionne le `ResourceLoader` et l'abstraction `Resource` ?
`🟠 Intermédiaire` · Sujet : **Spring Core**

**Réponse :** `Resource` unifie l'accès aux fichiers (`file:`), au classpath (`classpath:`), aux URL et aux ressources de servlet ; `ResourceLoader`/`ResourcePatternResolver` (`classpath*:templates/*.html`) résolvent des motifs. Injectable via `@Value("classpath:data.json") Resource r`. Dans un jar, les ressources ne sont pas des fichiers : utiliser `getInputStream()` plutôt que `getFile()`.

### 209. Comment fonctionne l'AOP avec `@Aspect` (pointcuts, advices, ordre) et comment tester un aspect ?
`🟠 Intermédiaire` · Sujet : **Spring Core**

**Réponse :** `@Aspect` + `@Component` avec `@Around`/`@Before`/`@AfterReturning`/`@AfterThrowing`, pointcuts par expression (`execution(* com.app.service.*.*(..))`, `@annotation(Audited)`, `within`), `@Order` pour l'ordre des aspects (transactions en `Ordered.LOWEST_PRECEDENCE` par défaut). Tester via le contexte (le proxy doit exister) ou avec `AspectJProxyFactory` pour un test unitaire ciblé. Préférer les annotations aux expressions par package.

### 210. Comment implémenter un bean scope personnalisé ou un scope par requête dans un contexte non web (Kafka, batch) ?
`🟠 Intermédiaire` · Sujet : **Spring Core**

**Réponse :** Implémenter `Scope` (`get`, `remove`, `registerDestructionCallback`) et l'enregistrer via `CustomScopeConfigurer` ; stocker l'état dans un `ThreadLocal`/`ScopedValue` posé par un listener ou un intercepteur (par message Kafka, par étape batch). Alternative plus simple : un service stateless prenant le contexte en paramètre, ou des `ScopedValue` sans scope Spring.

### 211. Qu'est-ce que la propagation de contexte (MDC, sécurité, locale, traces) et comment la gérer avec `TaskDecorator` ?
`🟠 Intermédiaire` · Sujet : **Spring Core**

**Réponse :** Les `ThreadLocal` (MDC, `SecurityContext`, `LocaleContext`, `RequestAttributes`) ne suivent pas les threads d'un executor. `TaskDecorator` (Boot : `spring.task.execution` accepte un bean `TaskDecorator`) copie le contexte avant l'exécution et le nettoie après ; Micrometer `ContextPropagatingTaskDecorator` gère traces et MDC. Avec les virtual threads, `ScopedValue` est l'alternative structurelle.

### 212. Comment fonctionnent `@ModelAttribute`, `@InitBinder`, `@SessionAttributes` et `WebDataBinder` ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `@ModelAttribute` lie les paramètres de requête à un objet (formulaires) ou ajoute des attributs communs au modèle ; `@InitBinder` personnalise le `WebDataBinder` (formats de dates, champs autorisés `setAllowedFields` contre le mass assignment) ; `@SessionAttributes` conserve un attribut de modèle en session entre requêtes (formulaires multi-pages). Surtout pertinent pour les applications à vues serveur (Thymeleaf).

### 213. Comment construire une application web à vues serveur avec Thymeleaf et HTMX dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Thymeleaf rend des templates HTML côté serveur (`th:text`, fragments, layouts, formulaires liés au modèle, `sec:authorize`), avec cache en production ; HTMX ajoute l'interactivité par attributs (`hx-get`, `hx-target`, `hx-swap`) en renvoyant des fragments HTML depuis des contrôleurs (`htmx-spring-boot`). Résultat : peu de JavaScript, SEO naturel, développement rapide pour les back-offices et sites de contenu, sans SPA.

### 214. Comment gérer le contenu statique et les ressources versionnées dans Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `static/`, `public/`, `resources/` servis sous `/`, avec cache (`spring.web.resources.cache.cachecontrol.max-age`) et resource chain (`spring.web.resources.chain.strategy.content.enabled=true` pour des URLs hachées et `ResourceUrlProvider`/Thymeleaf dialect pour les réécrire). Pour une SPA Angular servie par Boot, un contrôleur de fallback vers `index.html` pour les routes non-API. En production, préférer un CDN ou Nginx pour les statiques.

### 215. Comment personnaliser Jackson dans Spring Boot (dates, naming, modules, mixins, vues) ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Propriétés `spring.jackson.*` (`default-property-inclusion`, `property-naming-strategy`, `time-zone`, `serialization.*`), un bean `Jackson2ObjectMapperBuilderCustomizer` (modules, mixins pour des classes tierces, sérialiseurs personnalisés, `@JsonComponent`), ou un `ObjectMapper` complet (remplace la config Boot). `@JsonFormat`/`@JsonProperty` sur les DTO, et `JsonMixin` (Boot 2.7+) pour annoter sans modifier les classes.

### 216. Comment fonctionne la gestion des sessions HTTP dans Spring Boot et comment l'externaliser ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Session Tomcat en mémoire par défaut (perdue au redémarrage, non partagée). Spring Session (`spring-session-data-redis`/JDBC) stocke la session dans Redis/base avec un filtre transparent, cookie configurable (`server.servlet.session.cookie.*`, `SameSite`), timeout, et `FindByIndexNameSessionRepository` pour lister/invalider les sessions d'un utilisateur. Nécessaire dès qu'il y a plusieurs instances derrière un load balancer sans affinité.

### 217. Comment gérer le CORS finement (par route, credentials, preflight, cache) ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `WebMvcConfigurer.addCorsMappings` (`allowedOriginPatterns`, `allowedMethods`, `allowCredentials`, `maxAge` pour cacher le preflight, `exposedHeaders`) ou `@CrossOrigin` ; avec Spring Security, déclarer aussi `http.cors()` (sinon le preflight est rejeté). Jamais `*` avec `allowCredentials=true` ; lister les origines par environnement ; et préférer un même domaine via reverse proxy quand possible.

### 218. Comment implémenter des webhooks entrants sécurisés dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Endpoint dédié sans CSRF (stateless), vérification de signature HMAC sur le corps brut (lire le `byte[]` avant la désérialisation, `ContentCachingRequestWrapper` si nécessaire), horodatage anti-rejeu, réponse 2xx rapide puis traitement asynchrone (file), idempotence par identifiant d'événement, rate limiting, journalisation, et endpoint de replay pour les échecs. Documenter les IPs sources si l'émetteur les publie.

### 219. Comment gérer les gros payloads, la compression et les limites de taille ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** `server.max-http-request-header-size`, `spring.servlet.multipart.max-*`, `server.tomcat.max-swallow-size`, `server.compression.enabled` (+ `mime-types`, `min-response-size`), et un filtre limitant la taille du corps JSON (413) pour éviter les attaques par volume ; streaming pour les gros corps (`InputStream` en paramètre) ; et limites cohérentes avec le reverse proxy (`client_max_body_size` Nginx, ALB).

### 220. Comment implémenter le pattern « request-scoped context » (tenant, corrélation) proprement ?
`🟠 Intermédiaire` · Sujet : **Spring MVC**

**Réponse :** Un `OncePerRequestFilter` extrait tenant/corrélation depuis headers ou jeton, les place dans le MDC et un objet de contexte (bean `@RequestScope` ou `ThreadLocal` nettoyé en `finally`), les propage aux threads asynchrones via `TaskDecorator` et aux appels sortants via un intercepteur `RestClient` (header `X-Correlation-Id`). Exposer un accès typé (`TenantContext.current()`) plutôt que des lectures du MDC.

### 221. Comment fonctionne le `WebClient` (filtres, retries, timeouts, connection pool, backpressure) ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** `WebClient.builder().baseUrl().filter(ExchangeFilterFunction)` (auth, logs, corrélation), `retrieve()`/`exchangeToMono()`, `onStatus` pour les erreurs, `retryWhen(Retry.backoff(3, 500ms).filter(transient))`, timeouts via `HttpClient` Reactor Netty (`responseTimeout`, `ConnectionProvider` pour le pool, `maxConnections`, `pendingAcquireTimeout`), et `bodyToFlux` pour le streaming. Utilisable aussi dans une application MVC (réactif pour les appels sortants seulement).

### 222. Comment gérer les erreurs et le `Context` dans une chaîne Reactor (MDC, tracing) ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** `onErrorResume`, `onErrorMap`, `doOnError`, `onErrorReturn` selon le besoin ; `Mono.deferContextual`/`contextWrite` pour transporter des données (tenant, trace) sans ThreadLocal ; Micrometer context propagation (`Hooks.enableAutomaticContextPropagation()`) rend MDC et traces disponibles dans les opérateurs. Ne jamais utiliser `block()` dans un thread non bloquant (Reactor lève une erreur).

### 223. Qu'est-ce que le `RouterFunction` (functional endpoints) et quand le préférer aux contrôleurs annotés ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** `RouterFunctions.route().GET("/users/{id}", handler::get).build()` déclare les routes en code, avec des `HandlerFunction` ; disponible en WebFlux et en MVC (`RouterFunction<ServerResponse>` MVC 6). Avantages : routes explicites et composables, compatibilité native, pas de réflexion ; inconvénient : moins d'annotations (validation, OpenAPI moins automatique). Les contrôleurs annotés restent le choix majoritaire.

### 224. Comment tester une application WebFlux (`WebTestClient`, `StepVerifier`) ?
`🟠 Intermédiaire` · Sujet : **WebFlux**

**Réponse :** `@WebFluxTest` + `WebTestClient` (`get().uri().exchange().expectStatus().isOk().expectBody(Dto.class)`) pour les endpoints, `StepVerifier.create(flux).expectNext(...).verifyComplete()` pour les chaînes réactives avec `withVirtualTime` pour les délais, `MockWebServer`/WireMock pour les `WebClient`, et `@DataR2dbcTest` avec Testcontainers pour la persistance.

### 225. Comment fonctionne la journalisation des requêtes HTTP (access log, `CommonsRequestLoggingFilter`, `HttpExchangeRepository`) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Access log Tomcat (`server.tomcat.accesslog.*`, pattern avec durée et headers), `CommonsRequestLoggingFilter` pour les corps (dev uniquement, données sensibles), Actuator `httpexchanges` avec un `HttpExchangeRepository` en mémoire pour le débogage, ou un filtre personnalisé émettant des logs structurés (méthode, path normalisé, statut, durée, corrélation) sans payloads. En production, les métriques `http.server.requests` remplacent l'analyse de logs.

### 226. Comment implémenter un endpoint Actuator personnalisé ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@Component @Endpoint(id = "cache")` avec `@ReadOperation`, `@WriteOperation`, `@DeleteOperation` ; `@WebEndpoint` pour HTTP uniquement, `@Selector` pour les paramètres de chemin. Exposer via `management.endpoints.web.exposure.include`, protéger par Spring Security (rôle opérateur), et documenter. Utile pour des opérations d'exploitation (vider un cache, changer un flag) sans redéploiement.

### 227. Comment utiliser `@Retryable`, `@Recover` et la résilience intégrée à Spring 7 ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Spring Retry (`spring-retry`) : `@EnableRetry`, `@Retryable(retryFor, maxAttempts, backoff = @Backoff(delay, multiplier))`, `@Recover` en repli, `RetryTemplate` programmatique. Spring Framework 7 intègre `@Retryable`/`RetryTemplate` et `@ConcurrencyLimit` dans le noyau (`spring-core` resilience), réduisant le besoin de Resilience4j pour les cas simples. Réserver les retries aux opérations idempotentes et transitoires.

### 228. Comment structurer une application Spring Boot en architecture hexagonale ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Packages `domain` (entités, services métier, ports = interfaces) sans dépendance Spring/JPA, `application` (cas d'usage, transactions), `adapters/in` (contrôleurs REST, listeners Kafka) et `adapters/out` (JPA, clients HTTP, producteurs). Les adaptateurs implémentent les ports ; la configuration Spring assemble le tout ; ArchUnit vérifie les dépendances. Les entités JPA sont distinctes du domaine (mappers) ou partagées pragmatiquement pour les petits projets.

### 229. Comment gérer les mappings entre entités, DTO et modèle de domaine (MapStruct, records) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** MapStruct génère des mappers typés à la compilation (`@Mapper(componentModel = "spring")`, `@Mapping`, mappings imbriqués, mise à jour d'entités `@MappingTarget`), sans réflexion ni surcoût. Les records comme DTO ; les mappers manuels restent acceptables pour les cas simples. Éviter ModelMapper (réflexion, erreurs silencieuses) et le mapping dans les contrôleurs.

### 230. Comment implémenter la validation métier au-delà de Bean Validation (règles, agrégats, erreurs multiples) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Bean Validation pour la syntaxe des entrées ; les règles métier dans le domaine (méthodes de l'agrégat levant des exceptions ou retournant un `Result`), un `Validator` de domaine collectant plusieurs erreurs (`List<Violation>`) converties en `ProblemDetail` avec `errors[]`, et des contraintes de base (unicité) confirmées par la base (gestion de `DataIntegrityViolationException` → 409). Tester les règles sans Spring.

### 231. Comment gérer la concurrence optimiste jusqu'à l'API (ETag/If-Match, 409/412) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Exposer la `@Version` de l'entité comme ETag dans les réponses ; les clients envoient `If-Match` sur `PUT`/`PATCH` ; le service compare (ou laisse JPA lever `ObjectOptimisticLockingFailureException`) et renvoie 412/409 avec un `ProblemDetail` invitant à recharger. Angular gère la reprise (afficher le diff, réappliquer). Cela évite les écrasements silencieux entre utilisateurs.

### 232. Comment implémenter `PATCH` correctement (JSON Merge Patch, JSON Patch, DTO partiels) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** JSON Merge Patch (`application/merge-patch+json`) : fusionner sur une représentation JSON de la ressource via `ObjectMapper.readerForUpdating` ou `json-patch`, puis valider ; JSON Patch (`application/json-patch+json`) : opérations `add/remove/replace` appliquées via une bibliothèque ; ou DTO avec `Optional`/`JsonNullable` (OpenAPI) pour distinguer « absent » de « null ». Toujours revalider l'objet résultant et gérer la concurrence.

### 233. Comment gérer les uploads/downloads volumineux avec S3 et Spring (présigné, streaming, multipart) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Uploads : le backend génère une URL présignée (`S3Presigner`) et le client envoie directement à S3 (pas de transit par l'application), puis notifie ou S3 émet un événement ; multipart présigné pour les très gros fichiers. Downloads : URL présignée ou streaming via `ResponseInputStream` → `StreamingResponseBody` avec `Content-Length`. Valider le type au callback, scanner antivirus si nécessaire, et chiffrer côté S3.

### 234. Comment implémenter une API GraphQL avec Spring for GraphQL ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-boot-starter-graphql` : schéma `.graphqls` dans `resources/graphql`, `@Controller` avec `@QueryMapping`, `@MutationMapping`, `@SchemaMapping` pour les champs, `@BatchMapping`/DataLoader contre le N+1, subscriptions (WebSocket), sécurité par `@PreAuthorize`, pagination par connexions (Relay), tests avec `GraphQlTester`, et limites de complexité/profondeur des requêtes pour éviter les abus.

### 235. Comment implémenter gRPC dans Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-grpc` (projet officiel, 2025) ou `grpc-spring-boot-starter` : services générés depuis `.proto` (plugin protobuf-maven), `@GrpcService` implémentant le stub, intercepteurs (auth, logs, métriques), clients injectés (`@GrpcClient`), TLS/mTLS, health et réflexion pour les outils, tests avec un serveur in-process. Adapté aux communications internes à faible latence ; REST/JSON reste pour les clients externes.

### 236. Comment concevoir un service de notifications (e-mail, push, SMS) résilient dans Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Publier une demande dans une file (Kafka/SQS) plutôt qu'envoyer dans la transaction métier ; un consommateur idempotent choisit le canal via une stratégie (`Map<Channel, NotificationSender>`), rend le gabarit, appelle le fournisseur avec timeouts/circuit breaker/retries, enregistre le statut, et route les échecs vers une DLQ. Préférences utilisateur et limitation de fréquence avant l'envoi ; métriques par canal.

### 237. Comment gérer la localisation des données (formats, monnaies, fuseaux) dans un backend international ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Stocker en formats neutres (`Instant`, montants en `BigDecimal` + code devise ISO, `Locale` de l'utilisateur en profil), formater uniquement à la présentation (côté client ou via `MessageSource`/`NumberFormat` avec la locale résolue par `LocaleResolver`), API avec `Accept-Language`, conversions de fuseaux explicites (`ZoneId` utilisateur), et tests avec plusieurs locales (`Locale.setDefault` piégeux : fixer la locale JVM en `en`/`UTC` en production).

### 238. Comment implémenter un système de jobs planifiés distribués et observables (ShedLock, Quartz, JobRunr) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** ShedLock : verrou base/Redis autour de `@Scheduled` (`@SchedulerLock(lockAtMostFor)`) pour une seule exécution par cluster. Quartz (starter Boot) : persistance JDBC, cluster, triggers dynamiques, misfire handling. JobRunr : jobs en base avec dashboard, retries, planification récurrente et exécution distribuée. Exposer métriques (durée, échecs) et alerter sur les jobs non exécutés.

### 239. Comment concevoir une API de recherche avancée (Elasticsearch/OpenSearch) avec Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Spring Data Elasticsearch (`@Document`, `ElasticsearchOperations`, `Criteria`/`NativeQuery`) ou le client Java officiel ; index alimenté par événements (outbox/Kafka) ou CDC depuis la base de vérité, avec réindexation complète possible ; mapping explicite (analyzers, keyword), pagination `search_after`, agrégations pour les facettes, surlignage, et fallback vers la base si le cluster est indisponible. Tester avec Testcontainers Elasticsearch.

### 240. Comment intégrer Redis au-delà du cache (verrous, rate limiting, pub/sub, streams, sessions) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `StringRedisTemplate`/Lettuce : `SET NX PX` pour les verrous simples (ou Redisson pour des verrous robustes), scripts Lua atomiques pour le rate limiting, `RedisMessageListenerContainer` pour pub/sub (invalidation de cache L1), Redis Streams avec `StreamMessageListenerContainer` pour des files légères avec groupes de consommateurs, Spring Session, et compteurs/sorted sets pour les classements. Timeouts client et gestion de la panne.

### 241. Comment fonctionne Spring Cloud Stream avec Kafka en détail (fonctions, bindings, DLQ, partitions, tests) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Beans `Function<Order, Invoice>`/`Consumer`/`Supplier` liés par `spring.cloud.function.definition` et `spring.cloud.stream.bindings.process-in-0.destination`, groupes, `partitionKeyExpression` côté producteur, DLQ via `enableDlq`, retries et backoff, sérialisation via `MessageConverter` ou Kafka natif (Avro), `StreamBridge` pour publier dynamiquement, et `TestChannelBinder` pour les tests sans broker. Kafka Streams binder pour les topologies.

### 242. Comment concevoir la gestion des erreurs et retries sur les consommateurs Kafka Spring (blocking vs non-blocking retries) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Blocking : `DefaultErrorHandler` avec `ExponentialBackOff` réessaie sur place (bloque la partition, simple). Non-blocking : `@RetryableTopic(attempts, backoff, dltTopicSuffix)` publie dans des topics de retry `-retry-1000`, `-retry-2000` puis DLT, sans bloquer les autres messages (ordre par clé perdu). Choisir selon l'importance de l'ordre ; classifier les exceptions (réessayables ou non) et alerter sur le DLT.

### 243. Comment fonctionne `KafkaTemplate` transactionnel avec JPA (`ChainedTransactionManager` déprécié, outbox) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Combiner une transaction base et Kafka n'est pas atomique : le `ChainedTransactionManager` (déprécié) validait dans l'ordre avec risque d'incohérence ; l'approche fiable est l'outbox (ou Kafka-first + consommateur mettant à jour la base de façon idempotente). Les transactions Kafka (`KafkaTransactionManager`, `@Transactional` sur le listener) couvrent uniquement consume-transform-produce entre topics.

### 244. Comment gérer les sérialiseurs Kafka JSON de Spring en toute sécurité (type headers, trusted packages) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `JsonSerializer` ajoute des headers de type ; `JsonDeserializer` exige `spring.json.trusted.packages` (jamais `*` en production, risque de désérialisation arbitraire) ou un `TypeMapper` explicite ; désactiver `spring.json.use.type.headers` et fixer `spring.json.value.default.type` pour des contrats indépendants de Spring ; utiliser des schémas (Avro/Protobuf) pour l'interopérabilité multi-langages.

### 245. Comment fonctionne Spring Kafka avec les virtual threads, la concurrence et l'ack manuel ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `concurrency` crée N conteneurs (threads) par listener, chacun avec ses partitions ; `AckMode.MANUAL_IMMEDIATE` + `Acknowledgment.acknowledge()` valide après traitement ; `spring.threads.virtual.enabled` fait tourner les listeners sur des virtual threads (utile si le traitement est bloquant). Le parallélisme reste borné par les partitions ; pour plus, batch listener (`@KafkaListener(batch = true)`) avec traitement parallèle interne et ack en fin de lot.

### 246. Comment concevoir un producteur Kafka fiable dans Spring (config, callbacks, métriques, ordre) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `acks=all`, `enable.idempotence=true`, `delivery.timeout.ms`, `linger.ms`/`compression` selon le débit, `KafkaTemplate.send` avec `CompletableFuture` et callback de log/métrique d'échec (ne pas ignorer le futur), clé stable pour l'ordre, `ProducerListener`, métriques Micrometer `kafka.producer.*`, et `KafkaAdmin`/`NewTopic` beans pour créer les topics avec la bonne configuration (ou GitOps). Sur échec définitif, outbox ou alerte.

### 247. Comment intégrer Spring Boot avec AWS (Spring Cloud AWS 3.x : S3, SQS, SNS, Secrets, Parameter Store, DynamoDB) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Starters `spring-cloud-aws-starter-*` : `S3Template`/`S3Resource` (`s3://bucket/key` injectable), `@SqsListener`/`SqsTemplate`, `SnsTemplate`, `spring.config.import=aws-secretsmanager:/app/` et `aws-parameterstore:`, `DynamoDbTemplate`, credentials via la chaîne du SDK v2 et région auto-détectée, LocalStack pour le local (`spring.cloud.aws.endpoint`). Tests avec Testcontainers LocalStack.

### 248. Comment fonctionne Spring Cloud Vault et la rotation dynamique de credentials de base ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring.config.import=vault://` charge les secrets KV ; le backend database de Vault génère des credentials PostgreSQL temporaires (leases) que Spring Cloud Vault renouvelle et, à expiration, régénère en mettant à jour le `DataSource` (`spring.cloud.vault.database.enabled`, `LeaseAwareVaultPropertySource`, HikariCP `setUsername/Password` sans redémarrage via un `SecretLeaseListener`). Authentification par Kubernetes auth ou AppRole.

### 249. Comment concevoir des tests d'intégration rapides et fiables sur un gros projet Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Un seul contexte partagé (classe de base abstraite avec `@SpringBootTest` + Testcontainers statiques réutilisés, `@ServiceConnection`), pas de `@MockitoBean` variés (chaque combinaison recrée un contexte), nettoyage de données par test (SQL ciblé ou `@Sql`), parallélisation par module Maven/Gradle, séparation unit/integration (`failsafe`), tests par tranche pour les couches, et surveillance du temps de suite en CI (budget). Le cache de contexte de Spring est la clé.

### 250. Comment fonctionne le `AuthorizationManager` et comment implémenter une autorisation personnalisée par ressource ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Depuis Security 6, `AuthorizationManager<T>` remplace `AccessDecisionManager` : `check(authentication, object)` retourne une `AuthorizationDecision`. On l'utilise dans `authorizeHttpRequests(a -> a.requestMatchers("/orders/{id}").access(orderAuthz))` avec accès aux variables de chemin (`RequestAuthorizationContext`), ou pour la sécurité de méthode. Il centralise des règles métier (propriété, tenant) au-delà des rôles.

### 251. Comment implémenter l'authentification à facteurs multiples (MFA/TOTP) avec Spring Security ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Après le login mot de passe, placer une `Authentication` partielle (autorité `MFA_REQUIRED`) et restreindre toutes les routes sauf `/mfa` via un `AuthorizationManager` ; vérifier le code TOTP (bibliothèque `dev.samstevens.totp`/`java-otp`), puis remplacer par une `Authentication` complète. Ou déléguer entièrement à un IdP (Keycloak/Cognito) qui gère MFA, passkeys et récupération : recommandé.

### 252. Comment intégrer les passkeys/WebAuthn dans Spring Security 6.4+ ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `http.webAuthn(w -> w.rpName("App").rpId("app.example.com").allowedOrigins("https://app.example.com"))` active les endpoints `/webauthn/register/options`, `/webauthn/register`, `/webauthn/authenticate/options`, `/login/webauthn` ; implémenter `PublicKeyCredentialUserEntityRepository` et `UserCredentialRepository` en base (par défaut en mémoire) ; côté Angular, appeler `navigator.credentials` avec les options reçues. Prévoir plusieurs passkeys par utilisateur et une méthode de secours.

### 253. Comment implémenter le « remember me » et la gestion des sessions concurrentes ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** `http.rememberMe(r -> r.tokenRepository(jdbcRepo).tokenValiditySeconds(...))` avec des tokens persistés (série/token, rotation) plutôt que le hash simple ; `sessionManagement(s -> s.maximumSessions(1).maxSessionsPreventsLogin(false))` avec `SessionRegistry` (Spring Session `SpringSessionBackedSessionRegistry` en multi-instances) pour limiter ou lister les sessions et permettre « déconnecter les autres appareils ».

### 254. Comment sécuriser les Server-Sent Events, WebSockets et les endpoints de longue durée ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Authentifier au handshake (cookie de session ou jeton en query/`Sec-WebSocket-Protocol`, jamais dans l'URL loggée si possible), autoriser par `AuthorizationManager<Message>` pour STOMP (`@EnableWebSocketSecurity`), vérifier l'`Origin` (CSRF WebSocket), expirer les connexions dont le jeton a expiré (fermeture côté serveur à `exp`), limiter le nombre de connexions par utilisateur et gérer les timeouts des proxies.

### 255. Comment concevoir un système d'API keys pour des partenaires (émission, stockage, rotation, quotas) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Clé aléatoire à haute entropie affichée une seule fois, stockée hachée (SHA-256 suffit pour un secret aléatoire), préfixe identifiable pour les scanners de secrets, association à un client avec scopes et quota, rotation avec chevauchement (deux clés actives), révocation immédiate, journalisation d'usage, rate limiting par clé, filtre Spring Security produisant une `Authentication` typée, et transmission en header (pas en query).

### 256. Comment implémenter l'authentification de service à service (client credentials, mTLS, jetons internes) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Client credentials OAuth2 via `OAuth2AuthorizedClientManager` (jetons courts, audience ciblée) injectés dans `RestClient` ; ou mTLS via un service mesh/`X509` authentication (`http.x509()`) ; ou jetons signés internes (JWT court avec `iss` de service et clés dans un JWKS interne). Éviter les secrets partagés statiques ; propager l'identité utilisateur avec le token exchange quand la chaîne agit pour un utilisateur.

### 257. Comment gérer l'autorisation sur les données (row-level) dans Spring Data ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Filtrer dans les requêtes par tenant/propriétaire (paramètres issus du `SecurityContext` via un `AuditorAware`-like `CurrentUser`), `@PostFilter`/`@PostAuthorize` uniquement pour de petites collections (chargement complet puis filtrage), Hibernate `@Filter` activé par un aspect/intercepteur de session, ou RLS PostgreSQL avec `SET LOCAL` par transaction. Ne jamais compter sur le client pour envoyer le bon identifiant.

### 258. Comment traiter les données personnelles (RGPD) dans une application Spring : chiffrement, masquage, suppression, audit ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Chiffrement au niveau champ pour les données très sensibles (`AttributeConverter` JPA avec AES-GCM et clés dans KMS/Vault, en gardant à l'esprit l'impact sur les recherches), masquage dans les logs (converters Logback, `@ToString.Exclude`), pseudonymisation dans les environnements hors production, droit à l'effacement (suppression ou anonymisation avec événements vers les autres systèmes), registre des traitements, et journalisation des accès aux données sensibles.

### 259. Comment tester la sécurité de bout en bout (401/403, CSRF, CORS, headers, JWT expirés) ?
`🟠 Intermédiaire` · Sujet : **Spring Sécurité**

**Réponse :** Tests MockMvc par endpoint avec `anonymous()`, `with(jwt())`, rôles insuffisants, CSRF absent/présent, preflight CORS (`options` avec `Origin`), assertions sur les headers de sécurité, jetons expirés/signés par une autre clé (Nimbus pour générer), et tests d'intégration avec Keycloak en Testcontainers pour le flux réel. Compléter par un scan DAST (ZAP) en CI et une revue des `permitAll`.

### 260. Comment fonctionne le cache de second niveau Hibernate et quand l'activer ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Cache par entité/collection (`@Cacheable`, `@Cache(usage = READ_ONLY|NONSTRICT_READ_WRITE|READ_WRITE)`) via JCache/Ehcache/Infinispan/Redis, partagé entre sessions ; utile pour les données de référence rarement modifiées et lues souvent. Pièges : invalidation en cluster, cohérence avec les modifications hors JPA, cache de requêtes (`hibernate.cache.use_query_cache`) très sensible aux modifications. Mesurer le taux de hit ; souvent un cache applicatif ciblé suffit.

### 261. Comment gérer les identifiants (UUID v7, séquences, `@GeneratedValue` stratégies) avec Hibernate 6 ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `GenerationType.SEQUENCE` avec `allocationSize` (batch d'ids, compatible avec le batching d'inserts) plutôt que `IDENTITY` (désactive le batching), `@UuidGenerator(style = TIME)` ou un générateur UUID v7 personnalisé pour des UUID ordonnés, identifiants assignés côté application (entités avec `Persistable` pour éviter le `SELECT` avant `INSERT`), et `equals` basé sur l'id une fois assigné. Migrer une stratégie d'id est une opération de schéma délicate.

### 262. Comment gérer les requêtes natives et les résultats non mappés (DTO, `Tuple`, `@SqlResultSetMapping`) ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `@Query(nativeQuery = true)` retournant une projection interface (colonnes → getters), `Tuple`/`Object[]`, ou `@SqlResultSetMapping` + `@ConstructorResult` ; `JdbcClient` pour du SQL sans JPA avec `RowMapper`/mapping automatique de records ; paramètres nommés ; pagination native nécessitant une `countQuery`. Tester sur la vraie base (dialecte).

### 263. Comment implémenter l'event sourcing léger ou l'historisation des entités (Envers) ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Hibernate Envers (`@Audited`) crée des tables `_AUD` avec révisions (auteur, timestamp via `RevisionListener`) et permet de requêter l'état à une révision. Pour un vrai event sourcing, stocker les événements (table append-only, Axon, EventStoreDB) et reconstruire les agrégats, avec des projections ; c'est un choix architectural lourd à réserver aux domaines qui en tirent une vraie valeur (audit fort, replays).

### 264. Comment gérer les gros graphes d'objets et les suppressions en masse sans exploser la mémoire ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Éviter `cascade = REMOVE` sur des milliers d'enfants (chargement + delete unitaire) : `@Modifying` bulk delete par requête, `ON DELETE CASCADE` en base, ou Spring Batch ; pour les mises à jour massives, `StatelessSession` ou JDBC batch ; `EntityManager.clear()` périodique dans les boucles ; `@BatchSize` et `Slice` pour parcourir ; et surveiller `hibernate.generate_statistics`.

### 265. Comment fonctionne Spring Data avec les bases NoSQL en mode réactif (MongoDB, Redis, Cassandra) ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** `ReactiveMongoRepository`/`ReactiveMongoTemplate` (change streams, transactions réactives), `ReactiveRedisTemplate` (streams, pub/sub réactifs), `ReactiveCassandraRepository`. Mêmes conventions de query methods, résultats `Mono`/`Flux`. À combiner avec WebFlux uniquement ; en MVC + virtual threads, les repositories bloquants sont plus simples.

### 266. Comment gérer les fuseaux et types temporels JPA/Hibernate 6 correctement ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Hibernate 6 mappe `Instant`/`OffsetDateTime` en `TIMESTAMP WITH TIME ZONE` (`hibernate.timezone.default_storage = NORMALIZE_UTC` recommandé) et `LocalDateTime` sans fuseau (ambigu, à éviter pour des instants) ; fixer la timezone JVM en UTC ; colonnes `timestamptz` en PostgreSQL ; `@Column(columnDefinition)` explicite dans les migrations Flyway ; tester avec un fuseau JVM différent pour détecter les erreurs de conversion.

### 267. Comment implémenter des recherches géographiques et des types spécifiques (arrays, enums, JSON) avec Hibernate 6 ?
`🟠 Intermédiaire` · Sujet : **Spring Data**

**Réponse :** Hibernate 6 supporte nativement `@JdbcTypeCode(SqlTypes.JSON)`, les tableaux (`String[]` → `text[]`), `@Enumerated` ou `@JdbcTypeCode(SqlTypes.NAMED_ENUM)` pour les enums PostgreSQL, et Hibernate Spatial pour les géométries (PostGIS) avec fonctions dans JPQL/HQL (`distance`, `within`). Vérifier le dialecte et écrire des requêtes natives quand HQL ne suffit pas.

### 268. Comment concevoir un job Spring Batch idempotent et rejouable (paramètres, `ExecutionContext`, écritures) ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Paramètres identifiants (date métier, fichier) pour une instance unique, écritures idempotentes (upsert, ou vérification d'existence), état de reprise stocké dans l'`ExecutionContext` par le reader, transactions par chunk, et `allowStartIfComplete` ou nouveau paramètre pour forcer une réexécution. Les effets de bord externes (envoi d'e-mails) doivent être tracés pour ne pas être répétés au restart.

### 269. Comment lire et écrire des fichiers volumineux (CSV, fixed-length, JSON) et gérer les erreurs de format ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** `FlatFileItemReader` avec `DelimitedLineTokenizer`/`FixedLengthTokenizer` et `FieldSetMapper`, `linesToSkip` pour l'entête, `strict`, encodage explicite, `skip(FlatFileParseException)` avec `SkipListener` pour journaliser les lignes rejetées dans un fichier d'anomalies, `FlatFileItemWriter` avec `headerCallback`, et `MultiResourceItemReader` pour plusieurs fichiers. Pour S3, `S3Resource` de Spring Cloud AWS.

### 270. Comment orchestrer plusieurs jobs et dépendances (flows, décisions, jobs imbriqués, orchestrateur externe) ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** Flows avec `on("COMPLETED").to(step2).from(step1).on("FAILED").to(cleanup)`, `JobExecutionDecider` pour les branchements, `split` pour le parallèle, `JobStep` pour imbriquer. Pour des dépendances entre applications, un orchestrateur (Airflow, Argo Workflows, Kubernetes CronJobs chaînés par événements) plutôt que des jobs monolithiques ; Spring Cloud Data Flow/Task pour un écosystème Spring.

### 271. Comment tester un job Spring Batch (`@SpringBatchTest`, `JobLauncherTestUtils`, tests d'étapes) ?
`🟠 Intermédiaire` · Sujet : **Spring Batch**

**Réponse :** `@SpringBatchTest` fournit `JobLauncherTestUtils` (`launchJob`, `launchStep("step")`) et `JobRepositoryTestUtils` pour nettoyer, `StepScopeTestExecutionListener` pour tester des composants `@StepScope` avec un `StepExecution` factice, données via Testcontainers, et assertions sur `ExitStatus`, compteurs (`readCount`, `writeCount`, `skipCount`) et le contenu écrit. Tester séparément readers/processors/writers en unitaire.

### 272. Comment concevoir le logging structuré et la corrélation dans une application Spring Boot (JSON, MDC, sampling) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `logging.structured.format.console=ecs` (Boot 3.4) ou Logback JSON encoder, champs `traceId`/`spanId` via Micrometer, `tenant`/`userId` (pseudonymisé) via MDC posé par filtre et propagé, niveau par package, `logging.structured.json.add` pour des champs fixes (service, version), pas de payloads ni de secrets, et échantillonnage/débounce des logs très fréquents. Les logs doivent être interrogeables par corrélation dans Loki/Elastic.

### 273. Comment définir et mesurer des SLO pour un service Spring (métriques, alertes burn rate) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Définir les SLI depuis `http.server.requests` (taux de succès, latence p99 sous seuil via histogrammes `management.metrics.distribution.percentiles-histogram`), fixer un objectif (99,9 % sur 30 jours), calculer le budget d'erreur et alerter sur le burn rate (Prometheus multi-fenêtres). Micrometer Observation permet d'ajouter des SLI métier (commandes validées). Documenter les SLO et les revoir avec le produit.

### 274. Comment gérer les dépendances de version et la sécurité de la supply chain d'un projet Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** BOM Boot pour la cohérence, Dependabot/Renovate groupés, `versions-maven-plugin` pour l'audit, OWASP Dependency-Check/Snyk/Trivy en CI avec seuil bloquant, SBOM généré (`cyclonedx-maven-plugin`, Actuator `/sbom`), signature des artefacts, vérification des checksums (`--strict-checksums`, Gradle dependency verification), miroir d'artefacts interne (Nexus/Artifactory) avec quarantaine, et suivi des CVE Spring via les advisories officielles.

### 275. Comment concevoir une API idempotente et résiliente pour des clients mobiles peu fiables ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Clés d'idempotence sur les écritures, réponses compactes (projections, compression), pagination par curseur, synchronisation par `updated_since`, `ETag`/304 pour économiser la bande passante, retries côté client avec backoff et déduplication côté serveur, timeouts courts, versionnement d'API strict (clients non mis à jour), et endpoints de batch pour réduire les allers-retours.

### 276. Comment gérer les longues transactions métier (paniers, réservations) sans transactions base longues ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Modéliser l'état intermédiaire explicitement (entité `Reservation` en statut `PENDING` avec expiration), transactions courtes par étape, job d'expiration ou TTL, verrouillage optimiste sur la confirmation, et saga pour les étapes externes (paiement). Les transactions base restent de l'ordre de la milliseconde ; le « long » vit dans le modèle de domaine.

### 277. Comment concevoir un module de paiement avec Spring (PSP, webhooks, idempotence, réconciliation) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Ne jamais manipuler de données carte (tokenisation côté PSP, PCI SAQ-A), intents de paiement créés avec clé d'idempotence, état persisté (`CREATED`, `AUTHORIZED`, `CAPTURED`, `FAILED`, `REFUNDED`), webhooks vérifiés par signature et traités de façon idempotente avec file, réconciliation quotidienne avec les rapports du PSP, montants en `BigDecimal`/centimes entiers avec devise, journal d'audit immuable, et tests avec le sandbox du PSP.

### 278. Comment implémenter des exports et rapports (CSV, Excel, PDF) sans dégrader le service ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Exports asynchrones (job + fichier vers S3 + notification), streaming pour les CSV synchrones de taille modérée, Apache POI en mode `SXSSF` (streaming) pour Excel, JasperReports ou HTML → PDF pour les documents, limites de taille/durée, pagination des requêtes, exécution sur des workers dédiés, et cache des rapports périodiques. Ne jamais construire un `byte[]` de plusieurs centaines de Mo dans une requête HTTP.

### 279. Comment fonctionne le `Problem Details` avec des erreurs de validation détaillées et l'internationalisation ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Étendre `ResponseEntityExceptionHandler`, surcharger `handleMethodArgumentNotValid` pour construire un `ProblemDetail` avec `setProperty("errors", List.of(new FieldError(field, code, message)))`, résoudre les messages via `MessageSource` selon la locale, fixer `type` vers une documentation d'erreurs, `instance` sur le path, et un `errorCode` stable pour les clients. Tester le format avec `jsonPath`.

### 280. Comment concevoir des tests de contrat entre un frontend Angular et une API Spring (Pact, OpenAPI) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Pact : le front écrit des interactions attendues (consumer tests) publiées au Pact Broker ; le backend les vérifie avec `pact-jvm` + `@Provider` en CI (`can-i-deploy`). OpenAPI : contrat source de vérité, validation des réponses réelles contre le schéma en test (`springdoc` + `openapi-validator`/`swagger-request-validator`), et client Angular généré. Les deux approches empêchent les ruptures silencieuses.

### 281. Comment mettre en place les tests de performance et de charge d'une application Spring en CI ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Gatling ou k6 avec des scénarios réalistes contre un environnement éphémère (Docker Compose/Testcontainers ou namespace Kubernetes), seuils (assertions sur p95, taux d'erreur) faisant échouer le pipeline, exécution nightly plutôt qu'à chaque commit, JMH pour les composants critiques, profils JFR collectés pendant le test, et comparaison avec la baseline pour détecter les régressions.

### 282. Comment gérer la configuration des `HttpMessageConverter` pour d'autres formats (CSV, Protobuf, YAML, streaming NDJSON) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Ajouter un `HttpMessageConverter` (ex. `ProtobufHttpMessageConverter`, converter CSV personnalisé avec Jackson CSV, YAML via `YAMLMapper`) et déclarer `produces`/`consumes` ; NDJSON (`application/x-ndjson`) via `StreamingResponseBody` ou `Flux` en WebFlux pour le streaming ligne par ligne ; négociation de contenu par `Accept`. Tester la sérialisation et documenter les formats dans OpenAPI.

### 283. Comment fonctionne le `Docker Compose` de Boot avec des profils, et comment partager la configuration locale d'équipe ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring.docker.compose.file`, `spring.docker.compose.profiles.active` pour n'activer que certains services, `lifecycle-management` (`start-only` pour garder les conteneurs), `readiness` par healthcheck, labels `org.springframework.boot.ignore`/`service-connection` pour contrôler l'auto-configuration. Committer `compose.yaml` avec des versions fixées identiques aux Testcontainers pour cohérence dev/test.

### 284. Comment concevoir une application Spring modulaire déployable en monolithe ou en microservices (modulith → services) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Modules Spring Modulith avec APIs explicites et événements pour toute communication inter-module ; persistance par module (schémas séparés) ; pas de transactions transverses ; événements externalisables (`@Externalized`) vers Kafka. Ainsi, extraire un module en service consiste à le déployer seul avec les mêmes contrats (événements, APIs), sans réécriture. Tester les modules isolément (`@ApplicationModuleTest`).

### 285. Comment fonctionnent les `@ConditionalOnExpression`, `@Profile` avec expressions et les configurations par fonctionnalité ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@Profile("prod & !maintenance")` (expressions logiques), `@ConditionalOnExpression("${feature.x.enabled} and '${env}' == 'eu'")`, `@ConditionalOnCloudPlatform(KUBERNETES)`, `@ConditionalOnJava`, et conditions personnalisées (`Condition` interface, `SpringBootCondition` avec messages de rapport). Préférer des conditions sur propriétés typées (`@ConditionalOnProperty`) aux expressions complexes, et garder les feature flags runtime hors des conditions de démarrage.

### 286. Comment implémenter un système de plugins ou d'extensions à chaud dans une application Spring ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Éviter le chargement dynamique de jars (class loaders, sécurité) : préférer des points d'extension typés (interfaces découvertes via `List<Extension>` injectée, `ServiceLoader`, ou `spring.factories` de starters), configuration par propriétés/flags, et des scripts sandboxés (GraalJS/Polyglot avec limites) si une logique utilisateur est nécessaire. Pour un vrai hot-plug, PF4J ou une architecture par services séparés.

### 287. Comment gérer les erreurs de connexion transitoires aux dépendances (base, Redis, Kafka) au démarrage et en fonctionnement ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Démarrage : HikariCP `initialization-fail-timeout` (ou `-1` pour tolérer), Flyway `connectRetries`, Kafka admin `fail-fast=false`, readiness restant `false` tant que les dépendances critiques manquent, Kubernetes redémarre si besoin. Fonctionnement : timeouts courts, retries avec backoff sur les opérations idempotentes, circuit breaker et dégradation (cache absent → aller à la base), et alertes sur les métriques de pool/erreurs.

### 288. Comment sécuriser et exposer une API à des partenaires externes (gateway, quotas, documentation, versioning, monitoring) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Une API gateway (Spring Cloud Gateway, Kong, AWS API Gateway) en frontal avec authentification (OAuth2 client credentials ou API keys), quotas et rate limiting par partenaire, WAF, journalisation et analytics, documentation OpenAPI publiée sur un portail, versioning explicite avec politique de dépréciation, environnement sandbox, SLA mesuré, et contact/alertes pour les partenaires. Le service derrière reste simple et protégé.

### 289. Comment fonctionnent les `BeanFactoryPostProcessor`, `BeanDefinitionRegistryPostProcessor` et `ImportBeanDefinitionRegistrar` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Ils interviennent avant l'instanciation des beans : `BeanFactoryPostProcessor` modifie les définitions (propriétés, placeholders), `BeanDefinitionRegistryPostProcessor` enregistre de nouvelles définitions dynamiquement, `ImportBeanDefinitionRegistrar` (via `@Import`) enregistre des beans à partir des métadonnées d'annotation (comme `@EnableJpaRepositories`). Utiles pour des frameworks internes (enregistrer un client par entrée de configuration) ; à utiliser avec parcimonie car ils compliquent l'AOT.

### 290. Comment enregistrer des beans dynamiquement à partir de la configuration (un client HTTP par fournisseur configuré) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `BeanDefinitionRegistryPostProcessor` lisant l'`Environment` (`Binder.get(env).bind("clients", ...)`) et enregistrant une `BeanDefinition` par entrée avec `GenericBeanDefinition`/`BeanDefinitionBuilder` et un nom dérivé ; ou, plus simple, une `Map<String, Client>` construite dans une méthode `@Bean` à partir des `@ConfigurationProperties`, injectée là où nécessaire. La seconde approche est plus lisible et compatible natif.

### 291. Comment fonctionne le rechargement à chaud de la configuration sans Spring Cloud (`@RefreshScope` alternatives) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Lire les valeurs à chaque usage depuis un bean de configuration rafraîchi par un watcher (fichier ConfigMap monté via `WatchService`, ou polling d'un service) et publié par événement ; les `@ConfigurationProperties` peuvent être reliées via `Binder` sur demande ; pour les composants nécessitant une reconstruction (`DataSource`), exposer une méthode de rechargement explicite. Spring Cloud Kubernetes offre le reload de ConfigMaps ; les feature flags gèrent le runtime.

### 292. Quelles bonnes pratiques pour écrire une bibliothèque interne partagée entre services Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Starter avec auto-configuration conditionnelle et propriétés documentées, pas de scan de composants, dépendances en `optional`/`provided` pour ne pas imposer de versions, compatibilité avec plusieurs versions de Boot testée (`ApplicationContextRunner`), versionnement SemVer avec `japicmp`, pas d'état global, hints AOT fournis, et documentation avec exemples. Éviter de mettre du métier partagé dans une bibliothèque : préférer des services ou des événements.

### 293. Comment intégrer Spring AI dans une application existante (ChatClient, outils, RAG, observabilité) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `spring-ai-starter-model-openai`/`anthropic`/`bedrock` ou `ollama`, `ChatClient.Builder` injecté avec `defaultSystem`, `advisors` (mémoire, `QuestionAnswerAdvisor` pour le RAG via un `VectorStore` pgvector), outils `@Tool` sur des beans métier (validation des entrées, permissions), sorties structurées vers des records, métriques et traces Micrometer (tokens, latence, coût), gestion des timeouts/retries, et evals automatisés sur des jeux de prompts.

### 294. Comment concevoir un agent ou un workflow LLM côté serveur avec Spring de façon sûre ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Boucle d'appels d'outils bornée (itérations max, budget de tokens), outils idempotents et sous autorisation de l'utilisateur courant (le `SecurityContext` s'applique aux `@Tool`), validation humaine pour les actions irréversibles, journalisation de chaque appel (prompt, outil, résultat) pour l'audit, sandbox pour tout code généré, timeouts, et tests de non-régression. Traiter les sorties du modèle comme des entrées non fiables.

### 295. Comment fonctionne la migration Boot 3 → Boot 4 (Framework 7) : étapes et points d'attention ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Java 17+ (21 recommandé), Jakarta EE 11 (Servlet 6.1, Persistence 3.2 / Hibernate 7), Jackson 3 (nouveau package et défauts : dates ISO, `FAIL_ON_UNKNOWN_PROPERTIES=false`), starters modularisés (nouvelles coordonnées), suppression des APIs dépréciées en 3.x (`RestTemplate` conservé), Spring Security 7, `@Retryable` intégré, null-safety JSpecify (warnings), Spring Data 4 et Kafka 4. Utiliser OpenRewrite et lire la note de migration ; passer par la dernière 3.5 avec dépréciations résolues.

### 296. Comment concevoir un service Spring Boot « cloud-native » de bout en bout (checklist finale) ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Stateless et configurable par environnement, secrets externalisés, probes et graceful shutdown, logs JSON + métriques + traces avec corrélation, timeouts/retries/circuit breakers sur chaque dépendance, idempotence des écritures et consommateurs, migrations rétrocompatibles, tests par tranche + intégration Testcontainers + contrat, image minimale non-root, pipeline avec scans, IaC/GitOps, SLO et alertes, documentation OpenAPI/AsyncAPI et runbooks. Chaque élément se vérifie en revue avant la mise en production.

### 297. Comment implémenter un endpoint de téléchargement avec reprise (`Range`) et un endpoint de streaming vidéo/audio ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Utiliser `ResourceRegion`/`HttpRange` : Spring MVC supporte nativement les requêtes `Range` quand on retourne un `Resource` (`ResponseEntity<Resource>`), renvoyant 206 avec `Content-Range` ; pour un contrôle fin, `HttpRange.parseRanges` + `ResourceRegion` ; `Accept-Ranges: bytes`, ETag pour la validation, et streaming depuis S3 par range GET. Limiter la taille des plages et journaliser les abus.

### 298. Comment fonctionnent `@JsonTest`, `JacksonTester` et les tests de sérialisation ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@JsonTest` configure Jackson comme en production (customizers inclus) et injecte `JacksonTester<T>` : `json.write(obj)` avec assertions `extractingJsonPathStringValue("$.name")`, `json.parse(content)` pour la désérialisation, et `isEqualToJson("expected.json")`. Il détecte les régressions de format (dates, naming, champs ignorés) sans démarrer le web.

### 299. Comment implémenter un cache de réponses HTTP côté serveur pour des GET coûteux avec invalidation ciblée ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** `@Cacheable` sur la méthode de service avec clé composée (paramètres + tenant), TTL via `RedisCacheConfiguration.entryTtl`, `@CacheEvict` sur les écritures concernées (ou événements d'invalidation par tag/préfixe avec Redis `SCAN` limité, ou Caffeine par clés), ETag dérivé de la version pour permettre 304, et métriques de hit. Ne pas cacher de réponses dépendantes de l'utilisateur sans l'inclure dans la clé.

### 300. Comment gérer les `@Transactional` sur des méthodes `private`, `final`, `static` ou appelées via `this` ?
`🟠 Intermédiaire` · Sujet : **Spring Boot**

**Réponse :** Le proxy Spring n'intercepte que les appels externes sur des méthodes publiques non finales : un `@Transactional` sur une méthode privée ou appelée en interne est ignoré silencieusement (le mode AspectJ le permettrait). Solutions : déplacer la méthode dans un autre bean, s'auto-injecter (`ObjectProvider<Self>`), ou utiliser `TransactionTemplate` programmatique. Un test d'architecture peut interdire `@Transactional` sur des méthodes non publiques.
