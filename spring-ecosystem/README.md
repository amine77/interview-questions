# 🌱 Spring Ecosystem

> Spring Core, Boot, Data, Batch, Cloud, Security, Actuator

**37 questions**

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
