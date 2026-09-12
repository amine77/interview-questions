# ▲ Next.js

> SSR, SSG, ISR, API routes, middleware, hydration

**50 questions**

---

### 1. Différence entre SSR et SSG ?
`🟢 Débutant` · Sujet : **Next.js**

**Réponse :** SSR génère la page à chaque requête côté serveur. SSG génère la page une fois au build, servie comme fichier statique.

### 2. Qu'est-ce que l'ISR ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Régénère une page statique en arrière-plan après un délai (`revalidate`), combinant performance SSG et contenu à jour.

### 3. Utilité de `_app.js` / `app/layout.tsx` ?
`🟢 Débutant` · Sujet : **Next.js**

**Réponse :** Définit une structure commune (layout, providers, styles globaux) appliquée à toutes les pages.

### 4. Qu'est-ce qu'une API Route ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Endpoint backend défini dans le projet Next.js (pages/api ou app/api), exécuté côté serveur.

### 5. Qu'est-ce que `middleware.ts` ?
`🟢 Débutant` · Sujet : **Next.js**

**Réponse :** Exécute du code avant qu'une requête soit complétée (redirection, auth check), à l'edge.

### 6. Qu'est-ce que l'hydration ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Processus attachant les gestionnaires d'événements/état au HTML statique généré côté serveur.

### 7. Qu'est-ce que Next.js et quels problèmes résout-il par rapport à une SPA React ?
`🟢 Débutant` · Sujet : **Next.js**

**Réponse :** Un framework React full-stack (Vercel) : routage par fichiers, rendu serveur (SSR/SSG/ISR/streaming), Server Components, API/Route Handlers, optimisation des images et polices, middleware edge. Il apporte SEO, performance initiale et backend léger sans configuration Webpack/Vite manuelle.

### 8. Comment fonctionne le routage par fichiers dans l'App Router ?
`🟢 Débutant` · Sujet : **Next.js**

**Réponse :** Chaque dossier sous `app/` définit un segment d'URL ; `page.tsx` rend la page, `layout.tsx` l'enveloppe (persistant entre navigations), `loading.tsx` un fallback Suspense, `error.tsx` une Error Boundary, `not-found.tsx` le 404. `[id]` crée un segment dynamique, `[...slug]` catch-all, `(group)` un groupe sans URL.

### 9. Différence entre un layout et un template ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Un `layout.tsx` persiste entre navigations frères : son état est conservé et il ne se re-rend pas. Un `template.tsx` est remonté à chaque navigation (nouvelle instance, effets rejoués), utile pour des animations d'entrée ou un état à réinitialiser par page.

### 10. Comment fonctionne le cache de `fetch` et la revalidation dans l'App Router ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Depuis Next 15, `fetch` n'est plus mis en cache par défaut. On active le cache par `{ cache: 'force-cache' }` ou `{ next: { revalidate: 60 } }` (ISR par requête), avec des tags (`next: { tags: ['posts'] }`) invalidables via `revalidateTag('posts')` ou `revalidatePath('/posts')` depuis une Server Action ou un Route Handler.

### 11. Différence entre rendu statique et dynamique d'une route ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Statique : rendu au build (ou revalidé par ISR), servi depuis le CDN. Dynamique : rendu à chaque requête, déclenché automatiquement par l'usage de `cookies()`, `headers()`, `searchParams`, `fetch` sans cache, ou `export const dynamic = 'force-dynamic'`. `next build` affiche pour chaque route si elle est statique (○) ou dynamique (ƒ).

### 12. Qu'est-ce que le Partial Prerendering (PPR) ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Un mode expérimental combinant statique et dynamique dans une même route : le shell statique est servi instantanément depuis le CDN, et les parties dynamiques (entourées de `<Suspense>`) sont streamées à la requête. Il vise à supprimer le choix binaire statique/dynamique par route.

### 13. Comment fonctionne le streaming avec `loading.tsx` et Suspense ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Le serveur envoie immédiatement le HTML du layout et des fallbacks, puis stream le contenu de chaque frontière Suspense quand ses données sont prêtes. `loading.tsx` crée automatiquement une frontière autour de la page. Cela améliore le TTFB et le LCP perçu pour les pages à données lentes.

### 14. Quand utiliser `'use client'` et quelles sont les limites des Client Components ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** `'use client'` marque la frontière : le composant et ses imports sont envoyés au navigateur. Nécessaire pour état, effets, événements, APIs navigateur. Limites : ne peut pas importer un Server Component (mais peut le recevoir en `children`), et les props reçues du serveur doivent être sérialisables (pas de fonctions, sauf Server Actions).

### 15. Comment passer des données d'un Server Component à un Client Component ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Par props sérialisables (JSON, Date supporté par le format RSC). Pattern : le Server Component charge les données et les passe à un Client Component interactif ; ou il rend des Server Components à l'intérieur d'un Client Component via `children` (composition), pour garder le maximum côté serveur.

### 16. Qu'est-ce qu'un Route Handler et en quoi diffère-t-il des API Routes ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Dans l'App Router, `app/api/x/route.ts` exporte des fonctions `GET`, `POST`… basées sur les objets Web `Request`/`Response` (au lieu de `req`/`res` Node des API Routes du Pages Router). Ils servent aux webhooks, APIs publiques, ou proxys ; pour les mutations depuis l'UI, les Server Actions sont plus simples.

### 17. Comment implémenter une Server Action et gérer ses états ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Fonction `async` avec `'use server'` (en tête de fichier ou de fonction), passée à `<form action={fn}>` ou appelée dans un événement. Côté client, `useActionState` fournit état et pending, `useFormStatus` le pending d'un bouton, `useOptimistic` les mises à jour optimistes. Valider les entrées (Zod) et vérifier l'authentification à l'intérieur.

### 18. Comment gérer les erreurs (`error.tsx`, `global-error.tsx`, `notFound()`) ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** `error.tsx` (Client Component) capture les erreurs de son segment et propose `reset()`. `global-error.tsx` couvre le layout racine. `notFound()` déclenche `not-found.tsx` avec un statut 404 ; `redirect()` renvoie une redirection. Les erreurs de Server Actions se retournent comme valeurs plutôt que lancées, pour être affichées.

### 19. Que peut faire le `middleware.ts` et quelles sont ses limites ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Il s'exécute avant la requête (runtime Edge) : redirections, réécritures, vérification de cookie de session, géolocalisation, A/B testing, headers de sécurité. Limites : pas d'accès à Node complet (pas de base de données lourde), doit rester rapide, et la vérification d'authentification complète doit être refaite dans les pages/actions.

### 20. Différence entre runtime Node.js et Edge ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Node : accès complet aux APIs Node et aux librairies natives, cold start plus long. Edge : sous-ensemble Web APIs, exécution proche des utilisateurs, démarrage instantané, limité en taille et en APIs (pas de `fs`, drivers de base restreints). Configurable par route (`export const runtime = 'edge'`).

### 21. Comment fonctionne `next/image` ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Il génère des `srcset` responsive, convertit en WebP/AVIF à la volée (ou via un loader CDN), impose les dimensions (pas de CLS), lazy-load par défaut, et `priority` pour l'image LCP. Les domaines distants doivent être déclarés dans `next.config` (`images.remotePatterns`).

### 22. Comment fonctionne `next/font` ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Il télécharge et auto-héberge les polices (Google ou locales) au build, génère les `@font-face` avec `size-adjust` pour éviter le CLS, et évite les requêtes vers des tiers. La police est exposée comme une classe/variable CSS à appliquer au layout.

### 23. Comment gérer les métadonnées et le SEO ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Exporter un objet `metadata` ou une fonction `generateMetadata` (asynchrone, par page) pour `title`, `description`, Open Graph, canonical, robots. Fichiers spéciaux : `sitemap.ts`, `robots.ts`, `opengraph-image.tsx` (génération d'images OG). Les Server Components garantissent que le HTML est complet pour les crawlers.

### 24. Comment générer les routes statiques dynamiques avec `generateStaticParams` ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Pour une route `[slug]`, `generateStaticParams` retourne la liste des paramètres à prérendre au build. Les slugs non listés sont rendus à la demande puis mis en cache (ISR) ou renvoient 404 selon `dynamicParams`. C'est le successeur de `getStaticPaths`.

### 25. Comment accéder aux cookies, headers et paramètres de recherche côté serveur ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** `cookies()` et `headers()` de `next/headers` (asynchrones depuis Next 15), et `searchParams`/`params` reçus en props des pages (également des Promises). Leur usage rend la route dynamique. Les cookies se modifient dans Server Actions ou Route Handlers uniquement.

### 26. Comment implémenter l'authentification dans Next.js ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Auth.js (NextAuth) v5 ou une solution comme Clerk/Auth0/Keycloak : session par cookie `HttpOnly`, vérification légère dans le middleware, vérification complète dans les Server Components/Actions via un helper (`auth()`), et Data Access Layer centralisant les contrôles. Ne jamais se fier au middleware seul.

### 27. Qu'est-ce qu'un Data Access Layer et pourquoi Next.js le recommande-t-il ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Un module serveur centralisant les requêtes de données et les vérifications d'autorisation (`server-only` importé pour empêcher son usage côté client), appelé par les Server Components et Actions. Il évite d'exposer accidentellement des données sensibles via des props et uniformise la sécurité.

### 28. Comment éviter d'exposer du code serveur au client (`server-only`, variables d'environnement) ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Importer le package `server-only` dans les modules sensibles fait échouer le build s'ils sont importés par un Client Component. Seules les variables préfixées `NEXT_PUBLIC_` sont exposées au navigateur ; les autres restent serveur. Les objets passés en props aux Client Components sont sérialisés dans le HTML : ne passer que le nécessaire.

### 29. Comment gérer l'état client et les mutations dans l'App Router ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** État UI local (`useState`) ou stores légers (Zustand) dans les Client Components ; état serveur via Server Components + revalidation après Server Action (`revalidatePath`) plutôt qu'un cache client, ou TanStack Query si l'interactivité l'exige. Le pattern « Server Action + revalidation » remplace beaucoup de code de synchronisation.

### 30. Comment fonctionnent les Route Groups et les Parallel/Intercepting Routes ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Route groups `(marketing)` organisent sans affecter l'URL et permettent plusieurs layouts racines. Parallel routes `@modal` rendent plusieurs pages simultanément dans un layout (dashboards). Intercepting routes `(.)photo/[id]` affichent une route dans un modal lors d'une navigation client tout en gardant l'URL partageable.

### 31. Comment internationaliser une application Next.js ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Pas de solution native dans l'App Router : segment `[locale]` en racine, détection de langue dans le middleware (header `Accept-Language`, cookie) avec redirection, et une librairie (next-intl, next-i18next) pour les messages, formats et routes localisées. `generateStaticParams` prérend chaque locale.

### 32. Comment tester une application Next.js ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Tests unitaires/composants avec Vitest ou Jest + RTL (les Server Components asynchrones se testent en les appelant comme des fonctions ou via E2E), MSW pour les APIs, Playwright/Cypress pour les parcours E2E contre `next dev` ou un build. Les Server Actions se testent comme des fonctions serveur avec des mocks de `cookies()`.

### 33. Quelles options de déploiement pour Next.js ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Vercel (support natif, ISR, Edge). Ailleurs : conteneur Docker avec `output: 'standalone'` (serveur Node minimal), adaptateurs communautaires (OpenNext pour AWS Lambda/CloudFront, Cloudflare), ou export statique (`output: 'export'`) si aucune fonctionnalité serveur n'est utilisée. Prévoir un cache ISR partagé (Redis) en multi-instances.

### 34. Comment fonctionne l'ISR en environnement auto-hébergé multi-instances ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Par défaut le cache ISR est sur le système de fichiers de chaque instance, donc incohérent entre Pods. Il faut un `cacheHandler` personnalisé (Redis, S3) déclaré dans `next.config` pour partager le cache, et propager `revalidateTag` à toutes les instances.

### 35. Qu'est-ce que Turbopack ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Le bundler Rust de Vercel, successeur de Webpack dans Next.js : stable pour `next dev` depuis Next 15 (démarrage et HMR beaucoup plus rapides) et en cours de stabilisation pour `next build`. Il est incrémental et met en cache à grain fin.

### 36. Comment optimiser le bundle client dans Next.js ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Garder un maximum de composants côté serveur, `'use client'` le plus bas possible dans l'arbre, `next/dynamic` pour le lazy loading de composants lourds (`ssr: false` pour ceux dépendant du navigateur), `optimizePackageImports`, analyse avec `@next/bundle-analyzer`, et éviter d'importer des librairies entières dans les Client Components.

### 37. Différence entre `next/link` et `<a>`, et qu'est-ce que le prefetching ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** `<Link>` effectue une navigation client (sans rechargement) en conservant les layouts, et précharge automatiquement les routes visibles dans le viewport (en production) : le segment statique ou le `loading.tsx` de la cible. `prefetch={false}` désactive ; `useRouter` permet la navigation programmatique.

### 38. Comment gérer le cache du Router côté client ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Le Router Cache mémorise en mémoire les segments visités et préchargés pour des navigations instantanées. Depuis Next 15, les pages dynamiques ne sont plus réutilisées par défaut (`staleTimes` configurable). `router.refresh()` et les Server Actions avec `revalidatePath` invalident ce cache.

### 39. Comment sécuriser une application Next.js (CSP, headers, Server Actions) ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Headers de sécurité via `headers()` dans `next.config` ou le middleware (CSP avec nonce généré par requête, HSTS, frame-ancestors), validation des entrées de Server Actions (elles sont des endpoints publics), vérification d'autorisation dans chaque action, `server-only`, `allowedOrigins` pour les actions, et mise à jour rapide (CVE du middleware en 2025).

### 40. Comment gérer les variables d'environnement et la configuration par environnement ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** `.env.local`, `.env.development`, `.env.production` chargés automatiquement ; `NEXT_PUBLIC_` inline au build (donc figé par image Docker), les autres lues au runtime côté serveur. Pour un « build once » avec configuration runtime côté client, exposer la configuration via un Server Component ou un endpoint.

### 41. Comment connecter Next.js à une base de données ou un backend Java ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Depuis les Server Components/Actions/Route Handlers : ORM (Prisma, Drizzle) pour un accès direct, ou appels HTTP vers l'API Spring Boot avec `fetch` (cache/revalidation) et propagation du token/cookie de l'utilisateur. Next.js joue alors le rôle de BFF ; les clés d'API restent côté serveur.

### 42. Comment gérer les uploads de fichiers ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Via un Route Handler ou une Server Action lisant `FormData` (`request.formData()`), avec limite de taille (`serverActions.bodySizeLimit`), validation du type, puis stockage sur S3/Blob storage. Pour les gros fichiers, générer une URL présignée et uploader directement depuis le navigateur vers le stockage.

### 43. Qu'est-ce que le fichier `instrumentation.ts` ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Un hook exécuté une fois au démarrage du serveur pour initialiser l'observabilité (OpenTelemetry via `@vercel/otel`, Sentry) et enregistrer des ressources globales. Il expose aussi `onRequestError` pour capturer les erreurs serveur.

### 44. Comment migrer du Pages Router vers l'App Router ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Progressivement : les deux routeurs coexistent, l'App Router ayant priorité sur les mêmes chemins. Migrer page par page : `getServerSideProps` → `fetch` dans un Server Component, `_app`/`_document` → `layout.tsx`, `useRouter` de `next/router` → `next/navigation`, API Routes → Route Handlers. Tester le SEO et le cache à chaque étape.

### 45. Différence entre Next.js, Remix/React Router v7 et Astro ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Next.js : le plus complet et le plus lié à Vercel, RSC en tête. React Router v7 (fusion avec Remix) : centré sur les standards web (loaders/actions, formulaires), simple à auto-héberger. Astro : orienté contenu, îlots d'interactivité multi-frameworks, JS minimal. Choisir selon le type de site et l'hébergement.

### 46. Quels sont les pièges courants de l'App Router ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Mettre `'use client'` trop haut (tout le sous-arbre passe côté client), oublier que Server Actions sont publiques, compter sur le middleware pour l'auth, `fetch` en cascade au lieu de `Promise.all`, confusion entre les différents caches, `searchParams` rendant la page dynamique involontairement, et hydration mismatch sur les dates.

### 47. Comment gérer les erreurs et le logging côté serveur ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Logger structuré (pino) dans les Server Components/Actions, `onRequestError` d'`instrumentation.ts` pour centraliser, intégration Sentry (côté serveur, edge et client), et ne jamais renvoyer les détails d'erreur au client (Next masque déjà les messages en production sauf `digest`).

### 48. Comment gérer le rendu conditionnel selon l'appareil ou le navigateur ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Côté serveur, lire `User-Agent` via `headers()` ou `userAgent()` du middleware pour adapter le rendu (ou rediriger), avec prudence car cela empêche la mise en cache statique. Côté client, préférer le CSS responsive ; pour les composants purement client, `next/dynamic` avec `ssr: false`.

### 49. Comment optimiser les Core Web Vitals spécifiquement dans Next.js ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** `next/image` avec `priority` sur le LCP, `next/font`, Server Components pour réduire le JS, streaming avec Suspense pour le TTFB, routes statiques/ISR sur CDN, `next/script` avec `strategy="lazyOnload"` pour les scripts tiers, et `useReportWebVitals` pour envoyer les métriques réelles.

### 50. Comment gérer les formulaires progressivement améliorés ?
`🟠 Intermédiaire` · Sujet : **Next.js**

**Réponse :** Un `<form action={serverAction}>` fonctionne même sans JavaScript (soumission HTML classique traitée par l'action), puis React améliore l'expérience (pending, validation, optimiste) une fois hydraté. Cette approche « progressive enhancement » est un avantage des Server Actions sur les formulaires en `onSubmit` + fetch.
