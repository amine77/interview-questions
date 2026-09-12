# 🔒 Security & Vulnerabilities

> OWASP Top 10, XSS, CSRF, SSRF, Zero Trust, SBOM, secure coding

**51 questions**

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

### 21. Qu'est-ce que le « Security Misconfiguration » (A05) et ses exemples fréquents ?
`🟠 Intermédiaire` · Sujet : **OWASP Top 10**

**Réponse :** Configuration par défaut ou incomplète : consoles d'administration exposées, stack traces en production, en-têtes de sécurité absents, buckets S3 publics, comptes par défaut, CORS `*`, Actuator ouvert. Remède : durcissement automatisé (IaC, images de base minimales), scans de configuration et revues régulières.

### 22. Qu'est-ce que « Vulnerable and Outdated Components » (A06) et comment s'en protéger ?
`🟠 Intermédiaire` · Sujet : **OWASP Top 10**

**Réponse :** Utiliser des dépendances avec CVE connues (Log4Shell, Spring4Shell). Protection : inventaire (SBOM), scan SCA en CI (OWASP Dependency-Check, Snyk, Trivy), mises à jour automatisées (Renovate/Dependabot), suppression des dépendances inutilisées et images de base à jour.

### 23. Qu'est-ce que « Cryptographic Failures » (A02) ?
`🟠 Intermédiaire` · Sujet : **OWASP Top 10**

**Réponse :** Exposition de données sensibles par cryptographie faible ou absente : mots de passe hachés en MD5/SHA-1 sans sel, TLS désactivé ou obsolète, clés codées en dur, chiffrement maison. Bonnes pratiques : bcrypt/Argon2 pour les mots de passe, AES-GCM, TLS 1.2+, gestion de clés par KMS, classifier les données.

### 24. Qu'est-ce que « Insecure Design » (A04) et que sont les threat modeling / abuse cases ?
`🟠 Intermédiaire` · Sujet : **OWASP Top 10**

**Réponse :** Défauts de conception plutôt que d'implémentation : absence de limite de tentatives, flux métier contournable, absence de séparation des rôles. Le threat modeling (STRIDE) et les abuse cases identifient dès la conception comment un attaquant détournerait la fonctionnalité, avant d'écrire le code.

### 25. Qu'est-ce que « Software and Data Integrity Failures » (A08) ?
`🟠 Intermédiaire` · Sujet : **OWASP Top 10**

**Réponse :** Confiance dans des mises à jour, plugins ou pipelines non vérifiés : CI/CD compromise (SolarWinds), CDN sans SRI, désérialisation non signée. Réponses : signature des artefacts (Sigstore/cosign), SLSA, vérification des checksums, pipelines à privilèges minimaux.

### 26. Qu'est-ce que « Security Logging and Monitoring Failures » (A09) ?
`🟠 Intermédiaire` · Sujet : **OWASP Top 10**

**Réponse :** Absence de journalisation des événements de sécurité (échecs d'authentification, changements de droits), logs non centralisés ou non surveillés, retardant la détection d'intrusion. Bonnes pratiques : logs structurés sans données sensibles, alerting, intégration SIEM, conservation adaptée.

### 27. Qu'est-ce que l'IDOR (Insecure Direct Object Reference) ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Accès à une ressource en modifiant un identifiant dans l'URL (`/invoices/1234` → `/1235`) sans vérification que l'utilisateur en est propriétaire. Correctif : contrôle d'autorisation systématique côté serveur sur chaque objet, et éventuellement identifiants non séquentiels (UUID) comme défense secondaire.

### 28. Qu'est-ce que la CORS et quelles erreurs de configuration sont dangereuses ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Cross-Origin Resource Sharing autorise un navigateur à appeler une API depuis une autre origine. Dangereux : `Access-Control-Allow-Origin` reflétant l'origine de la requête avec `Allow-Credentials: true`, ou wildcard sur une API authentifiée. Il faut une liste blanche d'origines explicite ; CORS ne protège pas contre les appels serveur-à-serveur.

### 29. Différence entre XSS stocké, réfléchi et basé sur le DOM ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Stocké : le payload est persisté (commentaire) et servi à tous. Réfléchi : injecté via un paramètre d'URL et renvoyé dans la réponse. DOM-based : le JavaScript client insère une donnée non fiable dans le DOM (`innerHTML`, `location.hash`). Protection : encodage contextuel, frameworks qui échappent par défaut (Angular, React), CSP, `Trusted Types`.

### 30. Qu'est-ce que le clickjacking et comment s'en prémunir ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Une page malveillante charge le site cible dans une iframe invisible et incite l'utilisateur à cliquer sur des éléments cachés. Protection : en-tête `X-Frame-Options: DENY` ou directive CSP `frame-ancestors 'none'`, et cookies `SameSite`.

### 31. Quels en-têtes HTTP de sécurité faut-il configurer ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** `Strict-Transport-Security` (HSTS), `Content-Security-Policy`, `X-Content-Type-Options: nosniff`, `X-Frame-Options`/`frame-ancestors`, `Referrer-Policy`, `Permissions-Policy`, et suppression de `Server`/`X-Powered-By`. Spring Security en applique plusieurs par défaut ; vérifier avec securityheaders.com ou OWASP ZAP.

### 32. Quelles différences entre les attributs de cookie `HttpOnly`, `Secure` et `SameSite` ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** `HttpOnly` interdit l'accès par JavaScript (limite le vol de session par XSS). `Secure` n'envoie le cookie qu'en HTTPS. `SameSite=Lax/Strict` empêche l'envoi sur les requêtes cross-site (défense CSRF), `None` l'autorise mais exige `Secure`.

### 33. Qu'est-ce que le path traversal et l'upload de fichier dangereux ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Path traversal : `../../etc/passwd` dans un nom de fichier pour lire hors du répertoire prévu. Upload dangereux : fichier exécutable ou double extension servi par le serveur. Protections : normaliser et vérifier que le chemin résolu reste dans le dossier autorisé, renommer les fichiers, valider le type réel (magic bytes), stocker hors webroot ou dans un bucket.

### 34. Qu'est-ce qu'une attaque ReDoS ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Une expression régulière avec backtracking catastrophique (`(a+)+$`) peut prendre un temps exponentiel sur une entrée conçue, bloquant un thread. Prévention : éviter les quantificateurs imbriqués, limiter la longueur des entrées, utiliser des moteurs linéaires (RE2) ou des timeouts.

### 35. Qu'est-ce que le rate limiting et pourquoi est-il un contrôle de sécurité ?
`🟠 Intermédiaire` · Sujet : **Vulnérabilités Web**

**Réponse :** Limiter le nombre de requêtes par client/IP/utilisateur protège contre le brute force, le credential stuffing, l'énumération et le déni de service applicatif. Implémentations : Bucket4j côté application, API Gateway, ingress NGINX, WAF. Répondre `429 Too Many Requests` avec `Retry-After`.

### 36. Comment stocker les mots de passe correctement ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Jamais en clair ni chiffrés de façon réversible : hachage lent avec sel unique via bcrypt, scrypt ou Argon2id (recommandé), coût ajusté pour ~100 ms. Ajouter un « pepper » stocké hors base, imposer des politiques (longueur, liste de mots de passe compromis) et permettre le rehash lors de la connexion si le coût évolue.

### 37. Comment gérer les secrets dans une application ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Jamais dans le code ou Git (scanner avec gitleaks/trufflehog), pas dans les images Docker. Injecter à l'exécution depuis un gestionnaire (Vault, AWS Secrets Manager, Kubernetes Secrets chiffrés/External Secrets), avec rotation, audit d'accès et principe du moindre privilège. Masquer les secrets dans les logs.

### 38. Qu'est-ce qu'une attaque par timing et comment comparer des secrets en toute sécurité ?
`🔴 Avancé` · Sujet : **Code sécurisé**

**Réponse :** Une comparaison classique (`equals`) s'arrête au premier octet différent, révélant par mesure de temps combien de caractères sont corrects. Utiliser une comparaison en temps constant : `MessageDigest.isEqual()` en Java, `crypto.timingSafeEqual` en Node.

### 39. Pourquoi et comment durcir la désérialisation JSON avec Jackson ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Le polymorphisme par défaut (`enableDefaultTyping`) permet à un attaquant de désigner des classes gadget. Ne jamais l'activer, utiliser `@JsonTypeInfo` avec une liste blanche de sous-types, `FAIL_ON_UNKNOWN_PROPERTIES` pertinent, limiter la taille des payloads et garder Jackson à jour.

### 40. Qu'est-ce que l'assignation de masse (mass assignment) et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Lier directement le corps de requête à une entité JPA permet à un client d'envoyer `"role": "ADMIN"` ou `"balance": 9999`. Utiliser des DTO dédiés par cas d'usage, ne mapper que les champs autorisés, et valider avec Bean Validation.

### 41. Qu'est-ce que la validation Bean Validation (`@Valid`, `@NotNull`) et où l'appliquer ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Jakarta Bean Validation déclare des contraintes sur les DTO (`@NotBlank`, `@Size`, `@Email`, `@Pattern`, contraintes custom), vérifiées par Spring sur `@Valid @RequestBody`. Appliquer à la frontière (contrôleur, messages Kafka), renvoyer des erreurs 400 structurées, et ne pas confondre validation et autorisation.

### 42. Différence entre SAST, DAST et IAST ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** SAST analyse le code source sans l'exécuter (SonarQube, Semgrep, CodeQL) : tôt dans le cycle, faux positifs. DAST attaque l'application en fonctionnement (OWASP ZAP, Burp) : trouve les problèmes de configuration réels. IAST instrumente l'application pendant les tests pour combiner les deux. SCA analyse les dépendances.

### 43. Qu'est-ce que le pentest et en quoi diffère-t-il d'un scan de vulnérabilités ?
`🟠 Intermédiaire` · Sujet : **Code sécurisé**

**Réponse :** Un scan est automatisé et détecte des faiblesses connues. Un test d'intrusion est mené par des humains qui enchaînent les vulnérabilités, testent la logique métier et évaluent l'impact réel, avec un périmètre et des règles d'engagement définis. Les deux sont complémentaires et souvent exigés par les référentiels (PCI DSS, ISO 27001).

### 44. Différence entre chiffrement symétrique et asymétrique, et qu'est-ce que le chiffrement d'enveloppe ?
`🟠 Intermédiaire` · Sujet : **Chiffrement / KMS**

**Réponse :** Symétrique (AES) : une clé partagée, rapide, adapté aux données. Asymétrique (RSA, ECC) : paire publique/privée, lent, adapté à l'échange de clés et aux signatures. Le chiffrement d'enveloppe chiffre les données avec une clé de données (DEK) elle-même chiffrée par une clé maître (KEK) gardée dans le KMS, permettant la rotation sans rechiffrer les données.

### 45. Différence entre hachage, chiffrement, encodage et signature ?
`🟠 Intermédiaire` · Sujet : **Chiffrement / KMS**

**Réponse :** Encodage (Base64) : réversible, aucune sécurité. Chiffrement : réversible avec une clé, protège la confidentialité. Hachage : irréversible, vérifie l'intégrité ou stocke des mots de passe. Signature : hachage chiffré par clé privée, garantit intégrité, authenticité et non-répudiation. HMAC : intégrité avec clé symétrique.

### 46. Comment fonctionne TLS et qu'est-ce que le mTLS ?
`🟠 Intermédiaire` · Sujet : **Chiffrement / KMS**

**Réponse :** Le handshake TLS authentifie le serveur via son certificat (chaîne de confiance vers une CA), négocie une clé de session via échange de clés (ECDHE) puis chiffre symétriquement. En mTLS, le client présente aussi un certificat : authentification mutuelle utilisée entre services (service mesh, Istio) et pour les API B2B.

### 47. Qu'est-ce que la gestion des identités machine (SPIFFE/SPIRE, workload identity) ?
`🟠 Intermédiaire` · Sujet : **Zero Trust**

**Réponse :** Plutôt que des secrets statiques, chaque workload reçoit une identité cryptographique de courte durée (certificat SVID, token OIDC) émise automatiquement par la plateforme. Elle sert à s'authentifier auprès du cloud (IAM Roles for Service Accounts, GCP Workload Identity) ou d'autres services via mTLS, sans clé à distribuer.

### 48. Différence entre OAuth2, OpenID Connect et SAML ?
`🔴 Avancé` · Sujet : **Zero Trust**

**Réponse :** OAuth2 est un cadre d'autorisation (délégation d'accès à une API via un access token). OpenID Connect est une couche d'authentification sur OAuth2 ajoutant l'ID token (JWT) et le endpoint userinfo. SAML est le standard d'entreprise plus ancien basé sur XML pour le SSO. Pour une SPA, on utilise Authorization Code + PKCE.

### 49. Pourquoi le flux Authorization Code + PKCE est-il recommandé pour les SPA et applications mobiles ?
`🔴 Avancé` · Sujet : **Zero Trust**

**Réponse :** L'ancien flux Implicit exposait le token dans l'URL. Avec PKCE, le client génère un `code_verifier`, envoie son hash (`code_challenge`), et ne peut échanger le code contre un token qu'en présentant le verifier, ce qui neutralise l'interception du code. Il ne nécessite pas de secret client, impossible à protéger dans un navigateur.

### 50. Où stocker un access token côté navigateur et comment gérer le refresh ?
`🔴 Avancé` · Sujet : **Zero Trust**

**Réponse :** Éviter `localStorage` (lisible par XSS). Options : en mémoire (perdu au rechargement, renouvelé par refresh token en cookie `HttpOnly`), ou pattern BFF (Backend For Frontend) où le serveur garde les tokens et la SPA n'utilise qu'un cookie de session `HttpOnly, Secure, SameSite`. Les refresh tokens doivent être à rotation avec détection de réutilisation.

### 51. Qu'est-ce que le framework SLSA et la signature d'artefacts avec Sigstore ?
`🟠 Intermédiaire` · Sujet : **SBOM**

**Réponse :** SLSA (Supply-chain Levels for Software Artifacts) définit des niveaux de garantie sur la provenance d'un build (source contrôlée, build reproductible, attestations signées). Sigstore/cosign permet de signer images et artefacts sans gérer de clés (keyless via OIDC), et une politique d'admission (Kyverno) peut refuser toute image non signée.
