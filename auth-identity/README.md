# 🪪 Authentification & Identité

> Keycloak, flux OIDC, SCIM, sessions vs tokens, passkeys/WebAuthn

**50 questions**

---

### 1. Différence entre identification, authentification et autorisation ?
`🟢 Débutant` · Sujet : **Concepts**

**Réponse :** Identification : déclarer qui on est (identifiant). Authentification : le prouver (mot de passe, clé, biométrie, facteur multiple). Autorisation : décider ce qu'on a le droit de faire (rôles, permissions, politiques). Un système sécurisé sépare clairement ces trois étapes ; OAuth 2 traite l'autorisation déléguée, OIDC ajoute l'authentification.

### 2. Qu'est-ce qu'un fournisseur d'identité (IdP) et pourquoi centraliser l'identité ?
`🟢 Débutant` · Sujet : **Concepts**

**Réponse :** Un service qui authentifie les utilisateurs et émet des jetons ou assertions (Keycloak, Entra ID, Okta, Auth0, Cognito). Centraliser évite que chaque application gère mots de passe et MFA, permet le SSO, l'application uniforme des politiques (rotation, verrouillage, MFA), la révocation centrale et l'audit.

### 3. Qu'est-ce que le SSO et quelles technologies le permettent ?
`🟢 Débutant` · Sujet : **Concepts**

**Réponse :** Une authentification unique donnant accès à plusieurs applications sans se reconnecter : session sur l'IdP, chaque application redirige vers lui et reçoit un jeton. Protocoles : OpenID Connect (moderne, JSON/JWT, web et mobile), SAML 2.0 (XML, historique, fédération entreprise), Kerberos (réseau Windows). Le SSO exige aussi une déconnexion unique (SLO) cohérente.

### 4. Quels sont les rôles dans OAuth 2 ?
`🟢 Débutant` · Sujet : **OAuth/OIDC**

**Réponse :** Resource Owner (l'utilisateur), Client (l'application qui veut accéder), Authorization Server (émet les jetons après consentement/authentification), Resource Server (l'API qui valide les jetons). Le client n'obtient jamais le mot de passe de l'utilisateur : il reçoit un access token à portée limitée.

### 5. Différence entre OAuth 2 et OpenID Connect ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** OAuth 2 est un cadre d'autorisation déléguée (accès à des ressources) qui ne dit rien de l'identité. OIDC est une couche d'authentification par-dessus : il ajoute l'ID token (JWT décrivant l'utilisateur authentifié), le endpoint `userinfo`, le scope `openid`, la découverte (`.well-known/openid-configuration`) et les JWKS. « Se connecter avec Google » est OIDC.

### 6. Comment fonctionne le flux Authorization Code avec PKCE ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Le client génère un `code_verifier` aléatoire et envoie son hash (`code_challenge`) en redirigeant l'utilisateur vers l'IdP ; après authentification, l'IdP redirige avec un `code` ; le client échange le code contre les jetons en fournissant le `code_verifier`, que l'IdP vérifie. PKCE empêche l'exploitation d'un code intercepté et est obligatoire pour tous les clients dans OAuth 2.1.

### 7. Pourquoi les flux Implicit et Resource Owner Password sont-ils dépréciés ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Implicit renvoyait l'access token dans l'URL (fuite via historique, referer, logs) sans possibilité de PKCE ni refresh sûr. Password Grant donnait le mot de passe à l'application, annulant les bénéfices de la délégation et empêchant MFA et fédération. OAuth 2.1 les supprime au profit d'Authorization Code + PKCE, y compris pour les SPA et mobiles.

### 8. Quand utiliser le flux Client Credentials ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Pour l'authentification machine à machine sans utilisateur (service A appelant l'API B, job batch) : le client s'authentifie avec son identifiant et son secret (ou mieux, un certificat mTLS ou un JWT signé par clé privée) et obtient un access token portant ses propres permissions. Les secrets doivent être stockés dans un gestionnaire de secrets et tournés.

### 9. Qu'est-ce que le Device Authorization Flow ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Pour les appareils sans navigateur ou clavier (TV, CLI, IoT) : l'appareil affiche un code court et une URL ; l'utilisateur les saisit sur un autre appareil et s'authentifie ; l'appareil interroge périodiquement l'IdP jusqu'à obtenir les jetons. Utilisé par les CLI cloud (`gh auth login`, `az login`).

### 10. Que contiennent access token, ID token et refresh token, et à qui sont-ils destinés ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Access token : destiné à l'API (audience), prouve l'autorisation, souvent JWT ou opaque, courte durée (5-15 min). ID token : destiné au client, JWT décrivant l'utilisateur (sub, name, email, auth_time, amr), jamais à envoyer aux APIs. Refresh token : destiné au client pour obtenir de nouveaux access tokens sans réauthentification, longue durée, à protéger et faire tourner.

### 11. Comment un Resource Server valide-t-il un JWT ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Vérifier la signature avec la clé publique récupérée via le JWKS de l'émetteur (mise en cache, rotation par `kid`), l'émetteur (`iss`), l'audience (`aud`), l'expiration (`exp`, avec tolérance d'horloge), `nbf`, l'algorithme attendu (refuser `none` et les changements d'algorithme), puis extraire scopes/rôles. Spring Security fait cela avec `oauth2ResourceServer().jwt()` et `issuer-uri`.

### 12. JWT ou jeton opaque : comment choisir ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** JWT : validation locale sans appel réseau, scalable, mais non révocable avant expiration (d'où des durées courtes) et exposant des claims. Opaque : simple chaîne validée par introspection (`/introspect`) auprès de l'IdP, révocable instantanément, contenu privé, au prix d'un appel par requête (à cacher). Souvent : JWT pour les APIs internes, opaque ou courts pour les cas sensibles.

### 13. Comment gérer la révocation et la déconnexion avec des JWT ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Access tokens très courts + refresh tokens révocables côté IdP (rotation à chaque usage, détection de réutilisation), liste de révocation ou « jti denylist » en cache pour les cas urgents, back-channel logout OIDC (l'IdP notifie les applications), et front-channel/RP-initiated logout pour terminer les sessions. Accepter qu'un JWT reste valide quelques minutes après révocation, ou passer à l'introspection.

### 14. Qu'est-ce que les scopes, les claims et les audiences ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Scopes : permissions demandées par le client (`openid profile orders:read`), accordées avec ou sans consentement. Claims : informations dans le jeton (identité, rôles, groupes, claims personnalisés). Audience (`aud`) : le ou les destinataires légitimes ; une API doit refuser un jeton dont elle n'est pas l'audience, sinon un jeton obtenu pour un service est réutilisable sur un autre.

### 15. Qu'est-ce que le Token Exchange (RFC 8693) et l'appel en chaîne de services ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Un service recevant un jeton utilisateur et devant appeler un autre service peut soit propager le jeton (si l'audience le permet, à éviter), soit l'échanger auprès de l'IdP contre un jeton ciblé (nouvelle audience, scopes réduits, `act` claim traçant la délégation). Cela préserve le contexte utilisateur tout en respectant le moindre privilège.

### 16. Qu'est-ce que DPoP et le mTLS-bound token ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Des mécanismes liant un jeton au client qui l'a obtenu (sender-constrained) : avec DPoP, le client signe chaque requête avec une clé dont l'empreinte est dans le jeton ; avec mTLS, le jeton est lié au certificat client. Un jeton volé devient inutilisable sans la clé. OAuth 2.1 et FAPI (finance) les recommandent.

### 17. Qu'est-ce que PAR, JAR et le profil FAPI ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Pushed Authorization Requests : le client envoie les paramètres d'autorisation directement à l'IdP et redirige avec une référence, évitant la manipulation de l'URL. JAR : paramètres dans un JWT signé. FAPI (Financial-grade API) combine PKCE, PAR, sender-constrained tokens et signatures pour les APIs bancaires/open banking. Utiles dès que les enjeux dépassent le login classique.

### 18. Session côté serveur ou jetons côté client : quelles différences ?
`🟠 Intermédiaire` · Sujet : **Sessions vs tokens**

**Réponse :** Session : identifiant opaque dans un cookie `HttpOnly`, état côté serveur (mémoire, Redis), révocation immédiate, simple pour les applications web classiques, exige un store partagé en multi-instances. Jetons (JWT) : sans état côté serveur, adaptés aux APIs et clients multiples, mais révocation difficile et stockage côté client délicat. Beaucoup d'architectures combinent : session avec le navigateur, jetons vers les APIs (BFF).

### 19. Où stocker les jetons dans une SPA ?
`🟠 Intermédiaire` · Sujet : **Sessions vs tokens**

**Réponse :** `localStorage` est accessible à tout script (XSS = vol de jeton) ; les cookies `HttpOnly; Secure; SameSite` sont invisibles au JS mais exposés au CSRF (mitigé par SameSite et anti-CSRF). Recommandation actuelle : ne pas manipuler de jetons dans le navigateur, via un Backend-for-Frontend qui garde les jetons et expose une session cookie ; à défaut, jetons en mémoire avec refresh silencieux et rotation.

### 20. Qu'est-ce que le pattern BFF pour l'authentification ?
`🟠 Intermédiaire` · Sujet : **Sessions vs tokens**

**Réponse :** Un backend dédié au frontend gère le flux OIDC (code + PKCE), stocke les jetons côté serveur, maintient une session cookie avec le navigateur, et ajoute l'access token aux appels vers les APIs. La SPA ne voit jamais de jeton, ce qui neutralise le vol par XSS et simplifie le refresh. Implémentations : Spring Cloud Gateway avec `TokenRelay`, Auth.js, oauth2-proxy.

### 21. Comment sécuriser les cookies de session ?
`🟠 Intermédiaire` · Sujet : **Sessions vs tokens**

**Réponse :** `HttpOnly` (inaccessible au JS), `Secure` (HTTPS seulement), `SameSite=Lax` ou `Strict` (CSRF), `Path` et `Domain` restreints, préfixe `__Host-`, identifiant aléatoire long, régénération après login (fixation de session), expiration d'inactivité et absolue, et invalidation côté serveur à la déconnexion. Spring Session externalise la session dans Redis pour le multi-instances.

### 22. Comment protéger une application contre le CSRF selon le mode d'authentification ?
`🟠 Intermédiaire` · Sujet : **Sessions vs tokens**

**Réponse :** Le CSRF n'existe que si le navigateur envoie automatiquement les credentials (cookies). Avec cookies de session : token anti-CSRF (Spring Security, double submit), `SameSite`, vérification de l'`Origin`. Avec un `Authorization: Bearer` ajouté par le code : pas de CSRF possible, mais exposition au XSS. Le BFF avec cookie SameSite + anti-CSRF est le compromis recommandé.

### 23. Qu'est-ce que Keycloak et ses concepts de base ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Un serveur d'identité open source (Red Hat) : realms (espaces isolés d'utilisateurs et de configuration), clients (applications : public, confidential, bearer-only), rôles (realm et client), groupes, identity providers (fédération vers Google, SAML, autres OIDC), user federation (LDAP/AD), flux d'authentification configurables, thèmes, et console d'administration/API REST.

### 24. Comment configurer un client Keycloak pour une SPA Angular et une API Spring ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Client public pour Angular : Standard Flow activé, PKCE obligatoire (S256), redirect URIs exactes, Web Origins pour CORS, pas de secret. Client bearer-only (ou sans flux) pour l'API, avec des rôles client et un mapper d'audience pour que `aud` contienne l'API. Spring : `issuer-uri` du realm ; Angular : keycloak-js ou angular-oauth2-oidc en code flow + PKCE.

### 25. Que sont les mappers et comment personnaliser les jetons ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Des règles (par client ou client scope) ajoutant des claims : attributs utilisateur, rôles (realm/client), groupes, audience, claims calculés (script deprecated, préférer les extensions Java). Les client scopes regroupent des mappers réutilisables, par défaut ou optionnels (demandés via `scope`). Limiter les claims aux besoins réels pour réduire la taille des jetons et l'exposition.

### 26. Comment gérer les rôles et les groupes dans Keycloak et côté application ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Rôles realm (globaux) et rôles client (par application), composés possibles ; groupes hiérarchiques portant des rôles et attributs, plus faciles à administrer que des rôles individuels. Côté Spring, mapper `realm_access.roles`/`resource_access.{client}.roles` vers des `GrantedAuthority`. Pour des règles fines, le moteur d'autorisation Keycloak (UMA, policies) ou une autorisation applicative.

### 27. Comment fédérer un annuaire LDAP/Active Directory et un IdP externe ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** User Federation LDAP : synchronisation ou lecture à la volée des utilisateurs et groupes, authentification déléguée (bind), mappers d'attributs, import périodique. Identity Brokering : Keycloak agit comme client d'un autre IdP (Google, Entra ID via OIDC/SAML), lie ou crée les comptes locaux (first login flow), et émet ses propres jetons uniformes aux applications.

### 28. Comment personnaliser les flux d'authentification (MFA, conditions) ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Les Authentication Flows sont des chaînes d'exécutions configurables (mot de passe, OTP, WebAuthn, conditions par rôle ou niveau) : dupliquer le flux « browser », rendre l'OTP obligatoire ou conditionnel (Conditional OTP), ajouter WebAuthn Passwordless, définir des « step-up » via ACR/LoA. Les Required Actions forcent la configuration de l'OTP ou le changement de mot de passe.

### 29. Comment déployer Keycloak en production ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Mode production avec TLS (ou reverse proxy en frontal avec `proxy-headers`), base PostgreSQL externe, plusieurs réplicas avec cache distribué (Infinispan/JGroups, `KUBERNETES` discovery), Keycloak Operator sur Kubernetes, ressources et limites adaptées, `hostname` fixé, thèmes et extensions dans l'image, sauvegardes de la base, et supervision via métriques Prometheus et health endpoints.

### 30. Comment automatiser la configuration de Keycloak (IaC) ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Provider Terraform Keycloak (realms, clients, rôles, mappers en code), export/import de realm JSON (`kc.sh export/import`) pour les environnements, Keycloak Config CLI (adorsys) pour appliquer des fichiers déclaratifs au démarrage, et l'Admin REST API pour les scripts. Éviter la configuration manuelle en console : non reproductible et non auditée.

### 31. Quelles alternatives à Keycloak et comment choisir ?
`🟠 Intermédiaire` · Sujet : **Keycloak**

**Réponse :** Managés : Auth0/Okta, Microsoft Entra ID (écosystème Microsoft), AWS Cognito, Google Identity Platform, Clerk/Descope (orientés développeurs). Open source : Keycloak, Authentik, Ory (Kratos/Hydra), ZITADEL. Critères : coût par utilisateur actif, hébergement et souveraineté des données, protocoles requis (SAML, SCIM, FAPI), personnalisation des flux, et compétences d'exploitation.

### 32. Qu'est-ce que SCIM et quel problème résout-il ?
`🟠 Intermédiaire` · Sujet : **SCIM**

**Réponse :** System for Cross-domain Identity Management (RFC 7643/7644) : une API REST standard pour provisionner et déprovisionner les utilisateurs et groupes entre un annuaire source (Entra ID, Okta) et des applications SaaS. Il automatise la création des comptes à l'arrivée, les mises à jour, et surtout la désactivation au départ, souvent oubliée manuellement (risque de sécurité).

### 33. Comment implémenter un endpoint SCIM dans une application ?
`🟠 Intermédiaire` · Sujet : **SCIM**

**Réponse :** Exposer `/Users` et `/Groups` avec les opérations GET (filtrage `filter=userName eq "x"`, pagination), POST, PUT, PATCH (opérations add/replace/remove), DELETE, le schéma SCIM (`schemas`, `id`, `externalId`, `meta`), et `/ServiceProviderConfig`. Authentifier l'IdP appelant par jeton Bearer dédié, journaliser toutes les modifications, et mapper `active=false` vers une désactivation (pas une suppression).

### 34. Différence entre provisionnement JIT et SCIM ?
`🟠 Intermédiaire` · Sujet : **SCIM**

**Réponse :** Just-In-Time : le compte est créé à la première connexion SSO à partir des claims du jeton ; simple, mais pas de déprovisionnement ni de mise à jour hors connexion, et les groupes ne sont synchronisés que partiellement. SCIM : synchronisation proactive complète, y compris désactivation et groupes, indispensable pour les clients entreprise. Souvent les deux : JIT pour démarrer, SCIM pour la gouvernance.

### 35. Qu'est-ce que WebAuthn / FIDO2 ?
`🟠 Intermédiaire` · Sujet : **Passkeys/WebAuthn**

**Réponse :** Un standard W3C/FIDO d'authentification par cryptographie asymétrique : lors de l'enregistrement, l'authentificateur (clé de sécurité, téléphone, Touch ID/Windows Hello) génère une paire de clés liée au site (origin) ; à la connexion, il signe un défi du serveur. Aucun secret partagé, résistance au phishing (la clé ne fonctionne que sur le bon domaine), et second facteur ou authentification sans mot de passe.

### 36. Qu'est-ce qu'une passkey et en quoi diffère-t-elle d'une clé de sécurité classique ?
`🟠 Intermédiaire` · Sujet : **Passkeys/WebAuthn**

**Réponse :** Une credential WebAuthn « découvrable » (resident key) synchronisée via le gestionnaire de l'utilisateur (iCloud Keychain, Google Password Manager, 1Password) entre ses appareils, utilisable sans saisir d'identifiant (l'authentificateur propose les comptes) et sans mot de passe, avec vérification utilisateur (biométrie, code). Les clés matérielles restent pour les besoins de non-synchronisation ou d'attestation stricte.

### 37. Comment fonctionne la cérémonie d'enregistrement et d'authentification côté serveur ?
`🟠 Intermédiaire` · Sujet : **Passkeys/WebAuthn**

**Réponse :** Enregistrement : le serveur génère un challenge et des options (rp id, user, algorithmes, `residentKey`, `userVerification`), le navigateur appelle `navigator.credentials.create()`, le serveur vérifie la réponse (origin, challenge, signature d'attestation optionnelle) et stocke la clé publique, l'id de credential et le compteur. Authentification : challenge, `navigator.credentials.get()`, vérification de la signature, du rp id, du flag UV et du compteur.

### 38. Comment ajouter les passkeys à une application Spring / Keycloak ?
`🟠 Intermédiaire` · Sujet : **Passkeys/WebAuthn**

**Réponse :** Spring Security 6.4+ intègre WebAuthn (`http.webAuthn(...)` avec `rpName`, `rpId`, `allowedOrigins`, endpoints d'enregistrement/login et stockage des credentials à implémenter en base). Keycloak propose les authenticators WebAuthn (second facteur) et WebAuthn Passwordless dans les flux, avec politiques (attestation, algorithmes, résident). Prévoir un parcours de récupération et la gestion de plusieurs passkeys par compte.

### 39. Quels pièges à anticiper avec les passkeys ?
`🟠 Intermédiaire` · Sujet : **Passkeys/WebAuthn**

**Réponse :** Perte d'appareil sans passkey synchronisée (prévoir des méthodes de secours sûres, pas seulement l'e-mail), rp id incorrect entre sous-domaines, environnements de test sans HTTPS (localhost autorisé), navigateurs/OS hétérogènes, entreprises interdisant la synchronisation cloud, et migration progressive : garder le mot de passe + MFA en parallèle, puis promouvoir la passkey comme méthode principale.

### 40. Quels facteurs d'authentification et comment les classer par sécurité ?
`🟠 Intermédiaire` · Sujet : **MFA**

**Réponse :** Du plus faible au plus fort : SMS/appel (SIM swap, interception), e-mail, TOTP (app d'authentification, phishable), push avec confirmation de numéro (contre le push bombing), WebAuthn/passkeys (résistant au phishing). Privilégier les facteurs résistants au phishing pour les comptes sensibles et administrateurs ; le SMS uniquement en dernier recours.

### 41. Qu'est-ce que l'authentification adaptative et le step-up ?
`🟠 Intermédiaire` · Sujet : **MFA**

**Réponse :** Adapter le niveau d'exigence au risque : nouvel appareil, géolocalisation inhabituelle, opération sensible (changement d'IBAN, export de données) déclenchent un facteur supplémentaire ou une réauthentification récente (`max_age`, `acr_values` en OIDC, claim `auth_time`). Cela équilibre sécurité et friction sans imposer le MFA à chaque action.

### 42. RBAC, ABAC, ReBAC : quelles différences et quand les utiliser ?
`🟠 Intermédiaire` · Sujet : **Autorisation**

**Réponse :** RBAC : permissions par rôles, simple et lisible, explosion de rôles pour les cas fins. ABAC : règles sur attributs (utilisateur, ressource, contexte : « le propriétaire du document ou son manager, pendant les heures ouvrées »), flexible mais plus complexe à auditer. ReBAC : autorisations par relations dans un graphe (Google Zanzibar, OpenFGA, SpiceDB) pour les partages et hiérarchies. Combiner : RBAC pour les rôles métier, ABAC/ReBAC pour la propriété des données.

### 43. Comment externaliser l'autorisation (OPA, Cedar, OpenFGA) ?
`🟠 Intermédiaire` · Sujet : **Autorisation**

**Réponse :** Un Policy Decision Point évalue des politiques déclaratives (Rego pour OPA, Cedar d'AWS, tuples de relations pour OpenFGA) à partir de l'identité, de la ressource et du contexte ; l'application (Policy Enforcement Point) interroge en local (sidecar, bibliothèque) pour une faible latence. Avantages : politiques versionnées et testables, cohérence entre services, audit ; attention à la fraîcheur des données de décision.

### 44. Qu'est-ce que le Broken Object Level Authorization (BOLA/IDOR) et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **Autorisation**

**Réponse :** La première vulnérabilité des APIs : un utilisateur authentifié accède à la ressource d'un autre en changeant un identifiant (`/orders/123`). L'authentification ne suffit pas : vérifier pour chaque accès que la ressource appartient à l'utilisateur ou que ses relations l'autorisent (filtrer par tenant/propriétaire dans la requête, `@PostAuthorize` ou vérification dans le service), utiliser des identifiants non prédictibles, et tester ces cas.

### 45. Comment gérer le multi-tenant dans l'authentification et l'autorisation ?
`🟠 Intermédiaire` · Sujet : **Autorisation**

**Réponse :** Claim `tenant_id` dans le jeton (ou realm/organisation par tenant dans l'IdP : Keycloak Organizations), isolation des données par filtre obligatoire (Hibernate `@TenantId`, row-level security PostgreSQL, ou base par tenant), vérification que l'utilisateur appartient au tenant ciblé par la requête, rôles scoppés par tenant, et tests d'isolation croisée automatisés.

### 46. Comment stocker les mots de passe et gérer leur politique ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Hachage lent et salé : Argon2id (recommandé), bcrypt ou scrypt, avec coût calibré (~250 ms), jamais SHA/MD5 même salés. Politique NIST moderne : longueur minimale (12+), vérification contre les listes de mots de passe compromis (Have I Been Pwned), pas de rotation forcée ni de règles de composition arbitraires, limitation des tentatives et verrouillage progressif, notification des connexions suspectes.

### 47. Comment concevoir des parcours de récupération de compte sûrs ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Le point faible classique : lien de réinitialisation à usage unique, courte durée, aléatoire et lié au compte, envoyé sans révéler si le compte existe ; invalidation des sessions et refresh tokens après changement ; MFA ou vérification supplémentaire pour les comptes sensibles ; codes de secours générés à l'activation du MFA ; jamais de questions secrètes. Journaliser et notifier l'utilisateur.

### 48. Comment auditer et surveiller l'authentification ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Journaliser (sans mot de passe ni jeton) les connexions réussies et échouées, réinitialisations, changements de MFA, émissions et révocations de jetons, actions administratives, avec IP, user agent et horodatage ; détecter les anomalies (credential stuffing, force brute distribuée, voyages impossibles) ; alimenter un SIEM ; conserver selon la réglementation. Keycloak émet des events configurables exploitables par webhooks/Kafka.

### 49. Comment tester et déboguer un flux OIDC ?
`🟠 Intermédiaire` · Sujet : **OAuth/OIDC**

**Réponse :** Vérifier la découverte (`/.well-known/openid-configuration`), décoder les jetons (jwt.io ou `jq` sur le payload base64, jamais coller des jetons de production dans des sites tiers), comparer `iss`/`aud`/`exp`, contrôler les redirect URIs exactes et le `state`, inspecter les échanges avec les outils réseau du navigateur, activer les logs debug de Spring Security (`org.springframework.security=DEBUG`), et utiliser un IdP de test (Keycloak en Testcontainers, mock OIDC server) dans les tests d'intégration.

### 50. Qu'est-ce que la gestion des identités machines et des workloads (SPIFFE, Workload Identity) ?
`🟠 Intermédiaire` · Sujet : **Concepts**

**Réponse :** Les services ont aussi une identité : plutôt que des secrets statiques, on émet des identités éphémères vérifiables : SPIFFE/SPIRE (SVID, certificats X.509 ou JWT par workload), Workload Identity Federation (un Pod Kubernetes obtient un jeton cloud via son ServiceAccount, sans clé), IAM Roles for Service Accounts (AWS), mTLS via service mesh. Objectif : zéro secret longue durée dans les déploiements.
