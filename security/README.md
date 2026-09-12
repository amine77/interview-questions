# 🔒 Security & Vulnerabilities

> OWASP Top 10, XSS, CSRF, SSRF, Zero Trust, SBOM, secure coding

**20 questions**

---

### 1. Qu'est-ce qu'une attaque XSS ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Injection de scripts malveillants dans une page consultée par d'autres utilisateurs. Protection : échappement des sorties, en-têtes CSP.

### 2. Qu'est-ce qu'une injection SQL ?
`🟢 Débutant` · Sujet : **Vulnérabilités Web**

**Réponse :** Insertion de code SQL malveillant via une entrée non filtrée. Protection : requêtes préparées/paramétrées.

### 3. Qu'est-ce que CSRF ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Force un utilisateur authentifié à exécuter une action non désirée. Protection : tokens CSRF, attribut SameSite.

### 4. Broken Access Control ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Restrictions d'accès mal appliquées, permettant accès non autorisé (ex: IDOR).

### 5. Défense en profondeur ?
`🟢 Débutant` · Sujet : **Vulnérabilités Web**

**Réponse :** Superposition de plusieurs couches de sécurité indépendantes.

### 6. Insecure Deserialization ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Désérialisation de données non fiables sans validation, pouvant permettre exécution de code arbitraire.

### 7. Quelles sont les bonnes pratiques pour valider les entrées utilisateur côté serveur ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Toujours valider côté serveur même si une validation existe côté client, utiliser des listes blanches plutôt que des listes noires, s'appuyer sur des frameworks de validation (Bean Validation `@Valid`/`@NotNull`), et échapper/encoder les sorties selon le contexte (HTML, SQL, URL).

### 8. Qu'est-ce qu'une attaque par injection de dépendances malveillante (dependency confusion) ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Technique où un attaquant publie un package malveillant portant le même nom qu'un package interne privé sur un registre public, exploitant une mauvaise résolution de dépendances.

### 9. Principe du moindre privilège appliqué au code ?
`🟢 Débutant` · Sujet : **Code sécurisé**

**Réponse :** Concevoir chaque composant pour n'avoir accès qu'aux données/fonctionnalités nécessaires à son rôle, réduisant la surface d'impact.

### 10. Qu'est-ce que le SSRF ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Faille où un attaquant manipule le serveur pour effectuer des requêtes vers des ressources internes non censées être accessibles.

### 11. Principe de fail securely ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** En cas d'erreur non gérée, le système refuse l'accès par défaut plutôt que de l'accorder.

### 12. Content Security Policy (CSP) et protection XSS ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** En-tête HTTP définissant une liste blanche des sources autorisées, empêchant l'exécution de code injecté même en cas de faille XSS.

### 13. Principe de secure by default ?
`🟢 Débutant` · Sujet : **Code sécurisé**

**Réponse :** Configuration par défaut la plus sécurisée possible, obligeant un choix explicite pour assouplir la sécurité.

### 14. Subresource Integrity (SRI) ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Hash cryptographique attendu pour une ressource externe (CDN) ; le navigateur refuse l'exécution si le contenu ne correspond pas.

### 15. Principle of complete mediation ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Chaque accès à une ressource protégée doit être vérifié systématiquement, sans cache non sécurisé des décisions d'autorisation.

### 16. Qu'est-ce que l'injection (A03 du OWASP Top 10) et comment s'en prémunir ?
`🟢 Débutant` · Sujet : **OWASP Top 10**

**Réponse :** Une faille où des données non fiables sont interprétées comme du code par l'interpréteur cible (SQL, NoSQL, LDAP, OS). Prévention : requêtes paramétrées/préparées, validation stricte des entrées, principe du moindre privilège sur les comptes de base de données.

### 17. Qu'est-ce que le principe de "Zero Trust Architecture" ?
`🟠 Intermédiaire` · Sujet : **Zero Trust**

**Réponse :** Un modèle de sécurité qui ne fait confiance à aucune requête par défaut, qu'elle provienne du réseau interne ou externe, exigeant une vérification systématique de l'identité et du contexte (device, localisation) pour chaque accès, contrairement au modèle périmétrique traditionnel basé sur la confiance du réseau interne.

### 18. Qu'est-ce qu'un SBOM (Software Bill of Materials) ?
`🟢 Débutant` · Sujet : **SBOM**

**Réponse :** Un inventaire structuré de tous les composants logiciels (dépendances, bibliothèques, versions) d'une application, permettant de tracer l'exposition à une vulnérabilité découverte dans une dépendance tierce.

### 19. Différence entre chiffrement "at-rest" et "in-transit", et rôle d'un KMS ?
`🟠 Intermédiaire` · Sujet : **Chiffrement / KMS**

**Réponse :** At-rest protège les données stockées, in-transit protège la transmission (TLS). Un KMS centralise génération, rotation et contrôle d'accès aux clés cryptographiques.

### 20. Qu'est-ce que la "Broken Authentication" (A07) ?
`🟢 Débutant` · Sujet : **OWASP Top 10**

**Réponse :** Faiblesses dans la gestion de l'authentification/session permettant de compromettre des identifiants ou tokens, ex : sessions qui n'expirent jamais.
