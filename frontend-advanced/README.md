# 🖥️ Frontend Advanced

> PWA, Web Components, Core Web Vitals, a11y, micro-frontends, state mgmt

**51 questions**

---

### 1. Qu'est-ce que le Module Federation (Webpack 5) et quel problème résout-il ?
`🟠 Intermédiaire` · Sujet : **Micro-frontends**

**Réponse :** Une technique permettant à plusieurs applications JavaScript indépendantes de partager dynamiquement du code (composants, dépendances) à l'exécution, sans les regrouper au build, facilitant les architectures micro-frontend avec des équipes et des cycles de déploiement indépendants.

### 2. Qu'est-ce qu'un Web Component et en quoi diffère-t-il d'un composant React/Angular ?
`🟢 Débutant` · Sujet : **Web Components**

**Réponse :** Un Web Component est un standard natif du navigateur (Custom Elements, Shadow DOM, HTML Templates) permettant de créer des éléments HTML réutilisables indépendants de tout framework, contrairement aux composants React/Angular qui nécessitent leur runtime respectif pour fonctionner.

### 3. Quels sont les trois métriques principales des Core Web Vitals ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** LCP (Largest Contentful Paint), INP (Interaction to Next Paint, remplaçant FID), et CLS (Cumulative Layout Shift, stabilité visuelle).

### 4. Quelle est la différence philosophique entre Redux Toolkit et Zustand ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** Redux Toolkit impose une architecture stricte (actions, reducers, store unique, Immer) pour grandes applications. Zustand propose une API minimaliste par hooks, sans boilerplate, plus flexible pour besoins simples à modérés.

### 5. Qu'est-ce qu'un Service Worker et quel rôle joue-t-il dans une PWA ?
`🟢 Débutant` · Sujet : **PWA**

**Réponse :** Un script en arrière-plan interceptant les requêtes réseau pour permettre mise en cache, fonctionnement hors-ligne et notifications push.

### 6. Que signifie ARIA et quand doit-on l'utiliser ?
`🟢 Débutant` · Sujet : **Accessibilité (a11y)**

**Réponse :** Accessible Rich Internet Applications, attributs complétant la sémantique HTML pour les technologies d'assistance. À utiliser en complément des éléments natifs, jamais pour les remplacer quand un équivalent existe.

### 7. Que contient le fichier manifest.json d'une PWA ?
`🟠 Intermédiaire` · Sujet : **PWA**

**Réponse :** Métadonnées de l'application (nom, icônes, couleur de thème, mode d'affichage, écran de démarrage), permettant au navigateur de proposer l'installation comme application native.

### 8. Une alternative au Module Federation pour composer des micro-frontends ?
`🟢 Débutant` · Sujet : **Micro-frontends**

**Réponse :** Iframe (isolation forte), Server-Side Includes (assemblage côté serveur/edge), ou Web Components (chaque micro-frontend en custom element indépendant).

### 9. Qu'est-ce que l'INP et pourquoi a-t-il remplacé le FID ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Interaction to Next Paint mesure la latence de toutes les interactions d'une page (clic, touche, clavier) jusqu'au prochain rendu, en retenant la pire (approximativement). Le First Input Delay ne mesurait que le délai de la première interaction, ignorant les lenteurs ultérieures. Seuil « bon » : < 200 ms.

### 10. Comment améliorer le LCP ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Identifier l'élément LCP (image hero, titre), le charger en priorité (`fetchpriority="high"`, `<link rel="preload">`), éviter le lazy loading dessus, servir des images optimisées (WebP/AVIF, `srcset`), réduire le TTFB (CDN, cache, SSR), éliminer le CSS/JS bloquant le rendu et inliner le CSS critique.

### 11. Comment éviter le CLS ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Réserver l'espace des images et vidéos (`width`/`height` ou `aspect-ratio`), des publicités et embeds, éviter d'insérer du contenu au-dessus du contenu existant, précharger les polices avec `font-display: optional/swap` et `size-adjust`, et animer avec `transform` plutôt que des propriétés de layout.

### 12. Quelle est la différence entre données de laboratoire et données de terrain ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Lab (Lighthouse, WebPageTest) : mesures reproductibles dans un environnement contrôlé, idéales pour déboguer. Field (CrUX, RUM) : mesures réelles des utilisateurs, avec leurs appareils et réseaux, utilisées par Google pour le classement. Les deux peuvent diverger fortement ; optimiser d'après le terrain.

### 13. Qu'est-ce que le Total Blocking Time et les long tasks ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Une long task bloque le thread principal plus de 50 ms ; le TBT additionne les dépassements entre FCP et TTI. Réduire : découper les gros scripts (code splitting), différer le non-critique, utiliser Web Workers, `scheduler.yield()`/`requestIdleCallback`, et éviter le travail synchrone lourd au chargement.

### 14. Quelles stratégies de chargement des scripts (`async`, `defer`, `type="module"`) ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** `defer` télécharge en parallèle et exécute après le parsing, dans l'ordre. `async` exécute dès le téléchargement, sans ordre (analytics). `type="module"` est différé par défaut. Placer les scripts en fin de body est l'ancienne méthode. Les `<link rel="modulepreload">` accélèrent les graphes ESM.

### 15. Qu'est-ce que le resource hints (`preload`, `prefetch`, `preconnect`, `dns-prefetch`) ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** `preconnect` établit la connexion TCP/TLS à une origine tierce en avance. `dns-prefetch` résout juste le DNS. `preload` télécharge une ressource critique de la page courante en priorité. `prefetch` télécharge en basse priorité une ressource de la navigation suivante. Les speculation rules vont plus loin (prerender).

### 16. Comment optimiser les polices web ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Formats WOFF2, sous-ensembles de caractères (`unicode-range`), `font-display: swap` ou `optional`, préchargement de la police critique, polices variables pour réduire le nombre de fichiers, auto-hébergement plutôt que Google Fonts (connexion supplémentaire), et fallback avec `size-adjust` pour limiter le CLS.

### 17. Qu'est-ce que le code splitting et le tree shaking ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Tree shaking : suppression du code non importé (nécessite des modules ES et des packages sans effets de bord, `sideEffects: false`). Code splitting : découpage du bundle en chunks chargés à la demande (routes lazy, `import()` dynamique). Les deux réduisent le JS initial ; à vérifier avec un bundle analyzer.

### 18. Comment mettre en cache efficacement les assets d'une SPA ?
`🟠 Intermédiaire` · Sujet : **Core Web Vitals**

**Réponse :** Fichiers avec hash dans le nom (`main.abc123.js`) servis avec `Cache-Control: max-age=31536000, immutable` ; `index.html` avec `no-cache` (revalidation) pour pointer vers les nouveaux hashes. CDN devant, compression Brotli, et invalidation du cache CDN uniquement pour l'index au déploiement.

### 19. Quels sont les principes POUR de WCAG ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Perceptible (alternatives textuelles, contraste, contenu adaptable), Utilisable (navigation clavier, temps suffisant, pas de contenu déclenchant des crises), Compréhensible (lisible, prévisible, aide à la saisie), Robuste (compatible avec les technologies d'assistance). Les niveaux A, AA (cible légale courante) et AAA graduent les critères.

### 20. Quelles obligations légales en Europe et en France (RGAA, EAA) ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Le RGAA (Référentiel Général d'Amélioration de l'Accessibilité) impose aux services publics et grandes entreprises françaises une déclaration d'accessibilité et un niveau AA. L'European Accessibility Act, applicable depuis juin 2025, étend l'obligation à de nombreux produits et services privés (e-commerce, banque, transport).

### 21. Pourquoi le HTML sémantique est-il la première règle d'accessibilité ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Les éléments natifs (`<button>`, `<nav>`, `<main>`, `<label>`, `<table>`) portent déjà rôle, état, focus et interactions clavier ; un `<div onClick>` n'a rien de tout cela et exige ARIA, tabindex et gestionnaires clavier manuels. Première règle d'ARIA : ne pas utiliser ARIA si un élément natif fait le travail.

### 22. Comment gérer le focus dans une SPA (navigation, modales) ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** À chaque changement de route, déplacer le focus sur le titre ou le conteneur principal et mettre à jour `document.title`. Dans une modale : piéger le focus à l'intérieur, le rendre au déclencheur à la fermeture, fermer avec Échap, et masquer l'arrière-plan (`inert` ou `aria-hidden`). Angular CDK `FocusTrap` et `LiveAnnouncer` aident.

### 23. Qu'est-ce qu'une live region (`aria-live`) ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Une zone dont les changements sont annoncés par les lecteurs d'écran sans déplacer le focus : `aria-live="polite"` (attend une pause) ou `"assertive"` (interrompt), `role="status"`/`"alert"`. Utile pour les messages de succès, résultats de recherche, erreurs de formulaire.

### 24. Quelles règles de contraste et d'usage de la couleur ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Ratio minimal 4,5:1 pour le texte normal et 3:1 pour le texte large et les composants d'interface (AA). Ne jamais transmettre une information par la couleur seule (ajouter icône, texte, motif), penser aux daltoniens et au mode contraste élevé ; tester avec des outils (axe, Contrast Checker).

### 25. Comment rendre les formulaires accessibles ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** `<label for>` associé à chaque champ (ou `aria-labelledby`), instructions et formats avant la saisie, erreurs reliées par `aria-describedby` et `aria-invalid`, résumé des erreurs avec focus, pas de placeholder comme seul label, groupes avec `<fieldset>`/`<legend>`, et boutons explicites.

### 26. Comment tester l'accessibilité automatiquement et manuellement ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Automatique : axe-core (via Cypress/Playwright `injectAxe`, jest-axe, Lighthouse), eslint-plugin-jsx-a11y ou angular-eslint template rules ; ils ne détectent que ~30-40 % des problèmes. Manuel : navigation clavier seule, lecteur d'écran (NVDA, VoiceOver), zoom 200 %, mode contraste élevé, et tests utilisateurs.

### 27. Qu'est-ce que `prefers-reduced-motion` et `prefers-color-scheme` ?
`🟠 Intermédiaire` · Sujet : **Accessibilité (a11y)**

**Réponse :** Media queries reflétant les préférences système : réduire/désactiver les animations pour les utilisateurs sensibles au mouvement (`@media (prefers-reduced-motion: reduce)`), et proposer un thème sombre/clair automatique. Les respecter fait partie de l'accessibilité et du confort.

### 28. Quelles stratégies de cache un Service Worker peut-il appliquer ?
`🟠 Intermédiaire` · Sujet : **PWA**

**Réponse :** Cache First (assets versionnés), Network First (contenu frais avec fallback hors ligne), Stale-While-Revalidate (servir le cache puis rafraîchir), Network Only, Cache Only. Workbox (ou le Service Worker Angular via `ngsw-config.json`) déclare ces stratégies par route/type de ressource.

### 29. Comment gérer la mise à jour d'une PWA ?
`🟠 Intermédiaire` · Sujet : **PWA**

**Réponse :** Le nouveau Service Worker s'installe en arrière-plan et attend que tous les onglets soient fermés (`waiting`). Pour proposer la mise à jour : détecter l'événement (Angular `SwUpdate.versionUpdates`), afficher un bandeau « Nouvelle version », puis `skipWaiting` + rechargement. Éviter le mélange de versions d'assets.

### 30. Qu'est-ce que l'installabilité et les critères d'un « Add to Home Screen » ?
`🟠 Intermédiaire` · Sujet : **PWA**

**Réponse :** HTTPS, manifest avec `name`, `icons` (192 et 512 px), `start_url`, `display: standalone`, et un Service Worker enregistré. Le navigateur émet `beforeinstallprompt` que l'on peut intercepter pour afficher son propre bouton d'installation. iOS impose des limitations (pas de prompt, splash via meta).

### 31. Quelles APIs web avancées une PWA peut-elle utiliser ?
`🟠 Intermédiaire` · Sujet : **PWA**

**Réponse :** Push Notifications (Push API + Notification API, VAPID), Background Sync (rejouer des requêtes hors ligne), Periodic Sync, Web Share, File System Access, Badging, Web Bluetooth/USB (Chromium), Payment Request. Le support varie beaucoup selon les navigateurs, surtout Safari.

### 32. Comment concevoir une expérience hors ligne (offline-first) ?
`🟠 Intermédiaire` · Sujet : **PWA**

**Réponse :** Stocker les données dans IndexedDB (Dexie, localForage), mettre en file les mutations et les synchroniser au retour du réseau (Background Sync ou logique applicative), gérer les conflits (last-write-wins, versions, CRDT), indiquer clairement l'état hors ligne et ce qui est synchronisé.

### 33. Quelles sont les approches d'intégration des micro-frontends ?
`🟠 Intermédiaire` · Sujet : **Micro-frontends**

**Réponse :** Build-time (packages npm : simple mais couplé), run-time côté client (Module Federation, Native Federation, Web Components, single-spa), run-time côté serveur (SSI, edge-side includes, composition dans un BFF), et iframes (isolation maximale, UX limitée). Le choix dépend du besoin d'autonomie de déploiement.

### 34. Qu'est-ce que Native Federation et pourquoi est-il pertinent pour Angular ?
`🟠 Intermédiaire` · Sujet : **Micro-frontends**

**Réponse :** Une implémentation du concept Module Federation indépendante du bundler, basée sur les import maps et les modules ES, compatible avec esbuild (le builder par défaut d'Angular 17+). Elle permet de charger à l'exécution des remotes Angular avec partage des dépendances (`@angular/core` en singleton).

### 35. Comment partager l'état et communiquer entre micro-frontends ?
`🟠 Intermédiaire` · Sujet : **Micro-frontends**

**Réponse :** Éviter un store global partagé (couplage). Préférer : événements DOM personnalisés (`CustomEvent`), un event bus léger, l'URL comme état partagé, des Web Components avec propriétés/événements, et un partage minimal (authentification via le shell). Chaque micro-frontend garde son état interne.

### 36. Quels problèmes posent les micro-frontends (dépendances, CSS, versions) ?
`🟠 Intermédiaire` · Sujet : **Micro-frontends**

**Réponse :** Duplication de frameworks si les versions divergent (bundle plus lourd), fuites CSS (à isoler par Shadow DOM, préfixes, CSS Modules), incohérences UX sans design system partagé, complexité d'observabilité et de tests E2E, et coûts d'infrastructure. Ils se justifient surtout pour plusieurs équipes autonomes.

### 37. Qu'est-ce que le Shadow DOM et ses implications CSS ?
`🟠 Intermédiaire` · Sujet : **Web Components**

**Réponse :** Un sous-arbre DOM encapsulé attaché à un élément : les styles extérieurs ne s'appliquent pas dedans et inversement. Personnalisation via CSS custom properties (traversent la frontière), `::part()` et `::slotted()`. Angular `ViewEncapsulation.ShadowDom` l'utilise ; le défaut `Emulated` simule via des attributs.

### 38. Comment exposer un composant Angular en Web Component (Angular Elements) ?
`🟠 Intermédiaire` · Sujet : **Web Components**

**Réponse :** `@angular/elements` transforme un composant en custom element via `createCustomElement(MyComp, { injector })` puis `customElements.define('my-comp', el)`. Les `@Input` deviennent des propriétés/attributs et les `@Output` des `CustomEvent`. Utile pour intégrer dans un CMS ou un autre framework ; le bundle inclut le runtime Angular.

### 39. Que sont Lit et Stencil ?
`🟠 Intermédiaire` · Sujet : **Web Components**

**Réponse :** Des librairies légères pour écrire des Web Components : Lit (Google) avec templates tagués et réactivité minimale ; Stencil (Ionic) est un compilateur générant des composants standard avec TypeScript/JSX, plus des wrappers React/Angular/Vue. Ils conviennent aux design systems partagés entre frameworks.

### 40. Comment gérer les formulaires et l'accessibilité dans les Web Components ?
`🟠 Intermédiaire` · Sujet : **Web Components**

**Réponse :** Les éléments custom ne participent pas nativement aux formulaires : utiliser `ElementInternals` (`formAssociated = true`, `setFormValue`, `setValidity`) pour être soumis et validés. Pour l'accessibilité, `ElementInternals` permet aussi de définir rôle et états ARIA ; le Shadow DOM complique le référencement d'ids entre l'intérieur et l'extérieur.

### 41. Quand a-t-on besoin d'une librairie de state management ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** Quand l'état est partagé par de nombreux composants non liés, modifié depuis plusieurs endroits, doit être débogué (time travel, devtools) ou persisté/synchronisé. Pour la plupart des applications, des Signals/hooks locaux, l'état serveur via TanStack Query et l'URL suffisent. Commencer simple, ajouter un store sur douleur avérée.

### 42. Qu'est-ce que NgRx et ses concepts (Store, Actions, Reducers, Effects, Selectors) ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** Implémentation Redux pour Angular : le Store contient l'état immuable, les Actions décrivent des événements, les Reducers calculent le nouvel état, les Effects gèrent les effets de bord (HTTP), les Selectors dérivent et mémoïsent des vues. Verbeux mais prévisible, avec DevTools et time travel.

### 43. Qu'est-ce que NgRx SignalStore ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** Une API moderne et légère de NgRx basée sur les Signals : `signalStore({ providedIn: 'root' }, withState(...), withComputed(...), withMethods(...))`, avec des extensions (`withEntities`, `rxMethod` pour les flux RxJS). Bien moins de boilerplate que Store/Effects, adapté aux features locales ou globales.

### 44. Différence entre état client et état serveur (TanStack Query) ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** L'état serveur (données distantes) a des propriétés spécifiques : asynchrone, partagé, potentiellement périmé, à invalider. TanStack Query (React, Angular expérimental) gère cache, déduplication, refetch en arrière-plan, retries et mutations optimistes, retirant ce fardeau du store client, qui ne garde que l'état UI.

### 45. Qu'est-ce que la normalisation d'état et pourquoi la pratiquer ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** Stocker les entités dans des dictionnaires par id (`{ ids: [], entities: {} }`) plutôt qu'en tableaux imbriqués : mises à jour O(1), pas de duplication, sélecteurs simples. NgRx Entity et Redux Toolkit `createEntityAdapter` fournissent ces structures et les opérations CRUD.

### 46. Comment gérer les mises à jour optimistes ?
`🟠 Intermédiaire` · Sujet : **State Management**

**Réponse :** Appliquer le changement dans l'état local immédiatement, envoyer la requête, puis confirmer ou annuler (rollback) selon la réponse, avec message d'erreur. Améliore la perception de réactivité ; exige de conserver l'état précédent et de gérer les conflits avec les données serveur rafraîchies.

### 47. Qu'est-ce que le rendu hybride (SSR + SSG + CSR + streaming) et comment choisir ?
`🟠 Intermédiaire` · Sujet : **Frontend Advanced**

**Réponse :** SSG pour le contenu statique (marketing, docs), SSR pour le contenu dynamique nécessitant SEO ou LCP rapide, CSR pour les zones authentifiées et interactives, streaming SSR pour envoyer le shell puis les blocs lents. Angular (RenderMode par route) et Next.js permettent de mixer par route ou par composant.

### 48. Qu'est-ce que le Design System et un composant de design tokens ?
`🟠 Intermédiaire` · Sujet : **Frontend Advanced**

**Réponse :** Un design system est un ensemble de principes, composants UI et guidelines partagés. Les design tokens sont les valeurs atomiques (couleurs, espacements, typographies) définies dans un format neutre (JSON, Style Dictionary) et compilées en CSS custom properties, SCSS, ou thèmes Angular Material/Tailwind, garantissant la cohérence multi-plateforme.

### 49. Comment sécuriser une SPA côté client ?
`🟠 Intermédiaire` · Sujet : **Frontend Advanced**

**Réponse :** Pas de secrets dans le bundle (tout est public), tokens hors `localStorage` ou pattern BFF, CSP stricte avec nonces, sanitisation des contenus HTML (Angular `DomSanitizer` avec parcimonie), dépendances auditées (`npm audit`, Snyk), SRI pour les scripts tiers, et validation systématique côté serveur.

### 50. Qu'est-ce que l'internationalisation et la localisation, et quels pièges ?
`🟠 Intermédiaire` · Sujet : **Frontend Advanced**

**Réponse :** i18n prépare l'application (extraction des chaînes, formats), l10n l'adapte à une locale. Pièges : concaténation de chaînes (ordre des mots différent), pluriels et genres (ICU MessageFormat), dates/nombres/devises (`Intl`), sens de lecture (RTL avec propriétés logiques CSS), longueur des textes (allemand +30 %), et fuseaux horaires.

### 51. Comment gérer les images de façon performante et responsive ?
`🟠 Intermédiaire` · Sujet : **Frontend Advanced**

**Réponse :** Formats modernes (AVIF, WebP) avec `<picture>` fallback, `srcset`/`sizes` pour servir la bonne résolution, `loading="lazy"` hors viewport, `decoding="async"`, dimensions explicites, CDN d'images avec transformation à la volée (Cloudinary, imgix, Cloudflare Images), et `NgOptimizedImage`/`next/image` qui automatisent ces règles.
