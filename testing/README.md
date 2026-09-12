# ✅ Testing

> JUnit, Mockito, Cypress, Pact, mutation testing

**14 questions**

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
