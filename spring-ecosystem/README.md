# 🌱 Spring Ecosystem

> Spring Core, Boot, Data, Batch, Cloud, Security, Actuator

**50 questions**

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
