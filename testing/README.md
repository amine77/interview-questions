# ✅ Testing

> JUnit, Mockito, Cypress, Pact, mutation testing

**50 questions**

---

### 1. Différence entre un mock et un spy avec Mockito ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Un mock est entièrement simulé. Un spy enveloppe un objet réel, appelant les vraies méthodes sauf comportements surchargés.

### 2. Différence entre `cy.get()` et `cy.find()` ?
`🟢 Débutant` · Sujet : **Tests Cypress**

**Réponse :** `cy.get()` sélectionne depuis tout le document. `cy.find()` cherche des descendants à partir d'un élément déjà sélectionné.

### 3. Différence test unitaire / test d'intégration ?
`🟢 Débutant` · Sujet : **Tests Java**

**Réponse :** Unitaire = unité isolée avec mocks. Intégration = interaction entre composants réels.

### 4. À quoi servent les fixtures ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Fichiers de données statiques (JSON) simulant des réponses API ou fournissant des données de test, via `cy.fixture()`.

### 5. À quoi sert `@BeforeEach` ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Exécutée avant chaque test pour initialiser un état commun, garantissant l'indépendance entre tests.

### 6. Différence `cy.visit()` / `cy.request()` ?
`🟢 Débutant` · Sujet : **Tests Cypress**

**Réponse :** `visit` charge une page avec rendu JS. `request` fait une requête HTTP directe sans rendu.

### 7. `@ParameterizedTest` ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Exécute un test plusieurs fois avec différents jeux de données (@ValueSource, @CsvSource, @MethodSource).

### 8. À quoi sert `cy.intercept()` ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Intercepte/modifie les requêtes réseau, pour stubbing ou vérification.

### 9. Que fait `@Mock` avec Mockito ?
`🟢 Débutant` · Sujet : **Tests Java**

**Réponse :** Crée un objet simulé dont le comportement peut être défini via when/thenReturn.

### 10. Assertion avec `should()` ?
`🟢 Débutant` · Sujet : **Tests Cypress**

**Réponse :** Vérifie qu'une condition est vraie, avec retry automatique gérant l'asynchronisme.

### 11. `@SpringBootTest` ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Charge le contexte Spring complet pour tests d'intégration, à utiliser avec parcimonie.

### 12. Custom command ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Commande définie via `Cypress.Commands.add()` encapsulant une séquence répétitive (ex: login).

### 13. Qu'est-ce que le contract testing (avec un outil comme Pact) et quel problème résout-il ?
`🟠 Intermédiaire` · Sujet : **Contract Testing**

**Réponse :** Le consommateur d'une API définit ses attentes ("contrat"), vérifiées automatiquement des deux côtés en CI/CD, détectant les breaking changes entre microservices sans tests d'intégration end-to-end coûteux.

### 14. Qu'est-ce que le mutation testing et en quoi diffère-t-il de la couverture de code ?
`🟠 Intermédiaire` · Sujet : **Mutation Testing**

**Réponse :** Introduit des "mutants" dans le code pour vérifier si les tests les détectent, évaluant la qualité réelle des assertions plutôt que le simple pourcentage de lignes exécutées.

### 15. Qu'est-ce que la pyramide des tests et pourquoi la respecter ?
`🟢 Débutant` · Sujet : **Tests Java**

**Réponse :** Beaucoup de tests unitaires (rapides, isolés), moins de tests d'intégration (base, HTTP), très peu de tests end-to-end (lents, fragiles). Respecter cette proportion donne un feedback rapide et des suites stables ; une pyramide inversée (« cône de glace ») rend la CI lente et les échecs difficiles à diagnostiquer.

### 16. Qu'est-ce que le pattern AAA / Given-When-Then ?
`🟢 Débutant` · Sujet : **Tests Java**

**Réponse :** Structurer chaque test en trois blocs : Arrange (préparer les données et mocks), Act (appeler le code testé), Assert (vérifier le résultat). Given-When-Then est la formulation BDD équivalente. Un test devrait n'avoir qu'un « When » et tester un comportement unique, nommé explicitement (`shouldRejectOrderWhenStockIsEmpty`).

### 17. Différence entre `@MockBean` (déprécié) / `@MockitoBean` et `@Mock` ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** `@Mock` crée un mock Mockito pur, sans contexte Spring (`@ExtendWith(MockitoExtension.class)`). `@MockitoBean` (Spring Boot 3.4, remplace `@MockBean`) remplace un bean dans l'ApplicationContext d'un test Spring. Attention : chaque combinaison différente de mocks bean crée un nouveau contexte, ralentissant la suite.

### 18. Différence entre `@WebMvcTest`, `@DataJpaTest` et `@SpringBootTest` ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Ce sont des « test slices » : `@WebMvcTest` ne charge que la couche web (contrôleurs, filtres, `MockMvc`), `@DataJpaTest` la couche JPA avec base embarquée et transactions annulées, `@JsonTest`, `@RestClientTest`… `@SpringBootTest` charge tout le contexte, à réserver aux tests d'intégration complets.

### 19. Comment tester un contrôleur REST avec `MockMvc` ou `WebTestClient` ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** `MockMvc` simule les requêtes HTTP sans serveur : `mockMvc.perform(get("/api/x").with(jwt())).andExpect(status().isOk()).andExpect(jsonPath("$.name").value("a"))`. `WebTestClient` fait de même pour WebFlux ou contre un vrai serveur (`@SpringBootTest(webEnvironment = RANDOM_PORT)`). Spring 6.2 ajoute `MockMvcTester` avec AssertJ.

### 20. Qu'est-ce qu'AssertJ et pourquoi le préférer aux assertions JUnit ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Une librairie d'assertions fluides : `assertThat(list).hasSize(3).extracting("name").containsExactly("a","b","c")`. Avantages : lisibilité, autocomplétion typée, messages d'erreur détaillés, assertions sur exceptions (`assertThatThrownBy`), collections, Optional, et objets récursifs (`usingRecursiveComparison`).

### 21. Comment tester du code asynchrone ou avec des délais (Awaitility) ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Éviter `Thread.sleep`. Awaitility attend une condition avec timeout : `await().atMost(5, SECONDS).untilAsserted(() -> assertThat(repo.count()).isEqualTo(1))`. Pour les `CompletableFuture`, utiliser `join()`/`get(timeout)`. Pour le temps, injecter un `Clock` et le figer (`Clock.fixed`) plutôt que d'attendre réellement.

### 22. Comment tester avec Testcontainers une application Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Déclarer un conteneur (`@Container static PostgreSQLContainer<?> db = new PostgreSQLContainer<>("postgres:16")`) avec `@Testcontainers`, et brancher la datasource via `@ServiceConnection` (Spring Boot 3.1+) ou `@DynamicPropertySource`. Un conteneur `static` est partagé entre les tests d'une classe ; un singleton réutilisé accélère la suite (`testcontainers.reuse.enable`).

### 23. Qu'est-ce qu'un test paramétré avec `@MethodSource` / `@CsvSource` et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** `@ParameterizedTest` exécute le même test avec différents jeux de données : `@ValueSource` (valeurs simples), `@CsvSource` (lignes CSV), `@EnumSource`, `@MethodSource` (objets complexes fournis par une méthode statique). Idéal pour les règles de validation, conversions et cas limites.

### 24. Qu'est-ce que le property-based testing (jqwik) ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Au lieu de cas fixes, on déclare une propriété qui doit toujours être vraie (`encode(decode(x)) == x`) et le framework génère des centaines d'entrées aléatoires, puis réduit (shrinking) le contre-exemple trouvé au cas minimal. Il révèle des bugs que les exemples choisis à la main ne couvrent pas.

### 25. Qu'est-ce que ArchUnit ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Une librairie qui teste les règles d'architecture en JUnit : « les classes du package `domain` ne dépendent pas de `infrastructure` », « les contrôleurs sont annotés `@RestController` », « pas de cycles entre packages ». Elle empêche la dérive d'une architecture hexagonale ou en couches.

### 26. Différence entre test unitaire « solitaire » et « sociable » ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Le test solitaire (école mockiste) isole la classe en mockant toutes ses dépendances. Le test sociable (école classique, Detroit) laisse les vraies collaborations en place et ne mocke que les frontières (I/O, réseau). Les tests sociables sont moins couplés à l'implémentation et résistent mieux aux refactorings.

### 27. Quels sont les pièges d'un usage excessif des mocks ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Tests qui vérifient les interactions plutôt que le comportement, cassés à chaque refactoring, faux sentiment de sécurité (les mocks ne détectent pas les changements de contrat), et configuration verbeuse. Règle : mocker les frontières lentes ou non déterministes, pas les objets du domaine ; préférer fakes en mémoire ou Testcontainers.

### 28. Qu'est-ce que la couverture de code et quelles sont ses limites ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** JaCoCo mesure les lignes/branches exécutées par les tests. Une couverture élevée ne signifie pas que le comportement est vérifié (tests sans assertions), et 100 % n'est pas un objectif rentable. Utiliser la couverture pour détecter les zones non testées, la couverture de branches plutôt que de lignes, et compléter par le mutation testing.

### 29. Comment rendre les tests indépendants de l'ordre d'exécution et éviter les tests flaky ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Pas d'état statique partagé, base réinitialisée (`@Transactional` sur les tests ou `@Sql` de nettoyage), pas de dépendance à l'heure réelle (Clock injecté), ports aléatoires, pas de `Thread.sleep`, données de test uniques. JUnit 5 exécute par défaut dans un ordre déterministe mais non garanti ; `@TestMethodOrder` n'est pas une solution.

### 30. Comment exécuter les tests en parallèle avec JUnit 5 et Maven ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** `junit.jupiter.execution.parallel.enabled=true` avec `mode.default=concurrent` dans `junit-platform.properties`, à condition que les tests soient thread-safe. Maven Surefire supporte aussi `forkCount`/`reuseForks` pour paralléliser par JVM. Les tests Spring partagent le cache de contexte ; Testcontainers doit alors être en singleton.

### 31. Qu'est-ce que le BDD avec Cucumber et quand est-ce pertinent ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Les scénarios sont écrits en Gherkin (`Given/When/Then`) lisibles par le métier, liés à des step definitions Java. Pertinent quand les règles métier sont complexes et que le métier participe réellement à la rédaction ; sinon, il ajoute une couche de maintenance sans valeur par rapport à des tests JUnit bien nommés.

### 32. Comment tester un consumer/producer Kafka ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Avec `spring-kafka-test` (`@EmbeddedKafka`) ou Testcontainers (`KafkaContainer`, plus fidèle). On publie un message et on attend (Awaitility) l'effet attendu (ligne en base, message dans un topic de sortie lu par un consumer de test). Tester aussi la sérialisation, la gestion d'erreur et l'idempotence en rejouant le même message.

### 33. Comment tester la sécurité Spring (rôles, JWT) ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** `spring-security-test` fournit `@WithMockUser(roles = "ADMIN")`, `@WithUserDetails`, et les post-processors `MockMvc` `.with(jwt().authorities(...))` ou `.with(csrf())`. Tester systématiquement les cas 401 (non authentifié) et 403 (rôle insuffisant), pas seulement le chemin heureux.

### 34. Qu'est-ce que WireMock et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Un serveur HTTP de simulation qui répond selon des stubs (`stubFor(get("/api").willReturn(okJson(...)))`) pour tester les clients HTTP sans dépendre du service réel : erreurs 500, latences, timeouts, retries. Il s'intègre à Spring via `@AutoConfigureWireMock` ou Testcontainers. Différence avec Pact : WireMock ne vérifie pas le contrat côté fournisseur.

### 35. Comment tester les migrations Flyway/Liquibase ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Lancer la migration sur une base Testcontainers vide dans un test d'intégration (Spring le fait au démarrage du contexte), vérifier le schéma résultant, et ajouter un test qui applique les migrations sur un dump de production anonymisé pour détecter les scripts incompatibles avec les données réelles. Interdire la modification d'une migration déjà appliquée (checksum).

### 36. Quelle est la différence entre Cypress et Playwright ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Cypress s'exécute dans le navigateur, avec une API synchrone à retry automatique, un time-travel debugger et un écosystème mature, mais limité au multi-onglet et à un seul navigateur par test. Playwright pilote Chromium, Firefox et WebKit via CDP/protocoles natifs, supporte multi-contexte, parallélisation native et auto-waiting ; il est devenu le choix par défaut de nombreuses équipes.

### 37. Comment sélectionner des éléments de façon robuste (`data-testid`) ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Éviter les sélecteurs CSS de style ou de structure (`.btn-primary`, `div > span:nth-child(2)`) qui cassent à chaque refonte. Utiliser des attributs dédiés `data-cy`/`data-testid`, ou des sélecteurs par rôle et texte accessible (`cy.findByRole('button', { name: /submit/i })` via Testing Library), qui testent aussi l'accessibilité.

### 38. Comment gérer l'authentification dans des tests E2E sans passer par l'UI à chaque fois ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Se connecter une fois via API (`cy.request` vers le endpoint de login ou obtention d'un token OIDC), stocker la session avec `cy.session()` (mise en cache entre tests), puis injecter cookies/tokens. Le formulaire de login est testé une seule fois dans un test dédié.

### 39. Comment gérer les données de test et l'isolation dans des tests E2E ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Chaque test crée ses propres données via API ou seeding (`cy.task` appelant la base) et les nettoie, plutôt que de dépendre d'un état partagé. Utiliser des identifiants uniques (uuid) pour éviter les collisions en parallèle, et des comptes de test dédiés par worker.

### 40. Qu'est-ce que le component testing avec Cypress ou Storybook ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Monter un composant Angular/React isolé dans un vrai navigateur (`cy.mount(MyComponent, { componentProperties })`) pour tester rendu, interactions et responsive sans lancer l'application complète. Storybook documente les états d'un composant et permet des tests d'interaction et visuels (Chromatic) sur chaque story.

### 41. Comment tester une application Angular avec Jest ou Vitest plutôt que Karma ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Karma/Jasmine est déprécié. Angular CLI supporte les builders `@angular-devkit/build-angular:jest` (expérimental) et, depuis Angular 20, Vitest comme runner expérimental via `@angular/build:unit-test`. Jest/Vitest tournent en Node avec jsdom : plus rapide, pas de navigateur, snapshots et mocks intégrés. `TestBed` reste utilisable.

### 42. Comment gérer les tests flaky en E2E ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Utiliser les mécanismes d'attente intégrés plutôt que `cy.wait(ms)`, intercepter et attendre les requêtes réseau (`cy.intercept` + `cy.wait('@alias')`), stabiliser les données, désactiver les animations, isoler les tests, activer les retries (`retries: { runMode: 2 }`) en mesure temporaire et quarantaine des tests instables avec suivi.

### 43. Comment intégrer Cypress/Playwright dans une pipeline CI ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Image Docker officielle avec navigateurs, application démarrée en amont (`start-server-and-test` ou environnement éphémère), exécution headless avec parallélisation par shards, artefacts vidéo/screenshots sur échec, rapport JUnit pour l'intégration CI, et exécution sur les merge requests avec un sous-ensemble smoke puis la suite complète en nightly.

### 44. Qu'est-ce que le test visuel (visual regression testing) ?
`🟠 Intermédiaire` · Sujet : **Tests Cypress**

**Réponse :** Comparer des captures d'écran d'un composant ou d'une page avec une référence validée, pixel par pixel ou perceptuellement, pour détecter les régressions CSS invisibles aux tests fonctionnels. Outils : Playwright `toHaveScreenshot`, Percy, Chromatic, BackstopJS. Exige des environnements déterministes (polices, animations, données).

### 45. Différence entre contract testing consumer-driven (Pact) et validation OpenAPI ?
`🟠 Intermédiaire` · Sujet : **Contract Testing**

**Réponse :** Pact : le consommateur définit les interactions dont il a besoin ; le fournisseur vérifie qu'il les honore, via un broker qui bloque le déploiement en cas d'incompatibilité (`can-i-deploy`). Validation OpenAPI (Spring Cloud Contract, openapi-validator) : on vérifie que requêtes/réponses respectent la spécification publiée, sans savoir ce que les consommateurs utilisent réellement.

### 46. Qu'est-ce que Spring Cloud Contract ?
`🟠 Intermédiaire` · Sujet : **Contract Testing**

**Réponse :** Un outil de contract testing où le fournisseur écrit des contrats (Groovy/YAML) qui génèrent à la fois des tests côté producteur et des stubs (WireMock) publiés pour les consommateurs. Le producteur garantit ainsi que ses stubs correspondent à son comportement réel.

### 47. Qu'est-ce qu'un test de performance et quels outils utiliser ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Vérifier débit, latence (p95/p99) et comportement sous charge : test de charge (charge attendue), de stress (jusqu'à la rupture), d'endurance (fuites), de pics. Outils : Gatling (Scala/Java DSL, rapports riches), k6 (JavaScript, CI-friendly), JMeter. Intégrer des seuils en CI pour détecter les régressions de performance.

### 48. Comment tester les scénarios de résilience (timeouts, circuit breaker) ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** Avec WireMock ou Toxiproxy (Testcontainers) pour injecter latence, coupures et erreurs, puis vérifier que le circuit breaker s'ouvre, que le fallback répond, que les retries respectent le backoff et que les timeouts sont honorés. Ces tests documentent le comportement dégradé attendu.

### 49. Comment intégrer PIT (Pitest) dans un projet Maven et interpréter le score ?
`🟠 Intermédiaire` · Sujet : **Mutation Testing**

**Réponse :** Ajouter le plugin `pitest-maven` avec `pitest-junit5-plugin`, cibler les packages critiques (`targetClasses`) car l'exécution est coûteuse, et lancer `mvn pitest:mutationCoverage`. Le rapport liste les mutants survivants (code modifié sans test échoué) : chacun révèle un test manquant ou une assertion trop faible. Un score de 70-80 % sur le domaine est un bon objectif.

### 50. Qu'est-ce que le test « approval » ou snapshot côté backend ?
`🟠 Intermédiaire` · Sujet : **Tests Java**

**Réponse :** On enregistre la sortie d'une fonction (JSON, texte, rapport) comme référence approuvée et on compare les exécutions suivantes à celle-ci (ApprovalTests, Spring `JsonContent` assertions). Utile pour verrouiller le comportement d'un code legacy avant refactoring (« golden master ») et pour les sorties complexes difficiles à décrire par assertions.
