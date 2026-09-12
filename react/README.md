# ⚛️ React

> Hooks, Virtual DOM, reconciliation, state management

**50 questions**

---

### 1. Qu'est-ce que le Virtual DOM et pourquoi React l'utilise-t-il ?
`🟢 Débutant` · Sujet : **React**

**Réponse :** Représentation légère en mémoire du DOM réel. React compare (diffing) le Virtual DOM avant/après un changement d'état pour calculer le minimum de mises à jour nécessaires.

### 2. Différence `useMemo` / `useCallback` ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `useMemo` mémorise un résultat de calcul. `useCallback` mémorise une référence de fonction, évitant re-rendus inutiles.

### 3. Qu'est-ce que le props drilling ?
`🟢 Débutant` · Sujet : **React**

**Réponse :** Passer des props à travers plusieurs niveaux intermédiaires inutiles. Évité via Context API ou state management global.

### 4. Qu'est-ce que la reconciliation ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Algorithme de diffing comparant le Virtual DOM avant/après changement d'état.

### 5. Pourquoi une "key" dans une liste ?
`🟢 Débutant` · Sujet : **React**

**Réponse :** Identifie chaque élément pour le diffing, évitant re-rendus incorrects ou pertes d'état.

### 6. Qu'est-ce qu'un custom hook ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Fonction `use...` encapsulant une logique réutilisable basée sur les hooks natifs.

### 7. Qu'est-ce que JSX et comment est-il transformé ?
`🟢 Débutant` · Sujet : **React**

**Réponse :** Une extension de syntaxe permettant d'écrire du balisage dans du JavaScript. Babel/TypeScript/SWC le compilent en appels `jsx()` (runtime automatique depuis React 17, plus besoin d'importer React) produisant des objets « éléments React ». Les expressions se placent entre accolades ; `className` remplace `class`.

### 8. Différence entre composant fonctionnel et composant classe ?
`🟢 Débutant` · Sujet : **React**

**Réponse :** Les composants classe étendent `React.Component` avec `this.state`, `setState` et des méthodes de cycle de vie (`componentDidMount`…). Les composants fonctionnels sont des fonctions qui utilisent les hooks (`useState`, `useEffect`) ; ils sont le standard depuis React 16.8, plus concis, composables et mieux optimisés. Les classes restent pour les Error Boundaries.

### 9. Quelles sont les règles des hooks ?
`🟢 Débutant` · Sujet : **React**

**Réponse :** Les appeler uniquement au niveau supérieur d'un composant fonctionnel ou d'un custom hook (jamais dans une condition, boucle ou fonction imbriquée), pour que l'ordre d'appel soit stable entre rendus. Le plugin ESLint `react-hooks` (et le React Compiler) vérifient ces règles et les dépendances des effets.

### 10. Comment fonctionne `useState` et pourquoi les mises à jour sont-elles asynchrones et batchées ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `useState` retourne la valeur courante et un setter. Les appels de setter sont mis en file et appliqués au prochain rendu (batching automatique partout depuis React 18). Pour dépendre de la valeur précédente, utiliser la forme fonctionnelle `setCount(c => c + 1)` ; lire `count` juste après le `set` donne l'ancienne valeur.

### 11. Comment fonctionne `useEffect` et quel est le rôle du tableau de dépendances ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `useEffect(fn, deps)` exécute `fn` après le rendu quand une dépendance change (tableau vide : au montage seulement ; absent : à chaque rendu). La fonction retournée nettoie (abonnement, timer) avant la prochaine exécution et au démontage. Omettre une dépendance utilisée produit des valeurs périmées (stale closures).

### 12. Différence entre `useEffect` et `useLayoutEffect` ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `useLayoutEffect` s'exécute synchronement après les mutations du DOM mais avant que le navigateur ne peigne : utile pour mesurer ou ajuster le layout sans flash visuel. `useEffect` s'exécute après le paint, sans bloquer le rendu, et convient à la quasi-totalité des cas (données, abonnements).

### 13. Pourquoi ne faut-il plus utiliser `useEffect` pour charger des données, et quelles alternatives ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Le fetch dans `useEffect` pose des problèmes de courses (réponses hors ordre), de doubles appels en StrictMode, de cache et de chargement en cascade. Alternatives : TanStack Query ou SWR (cache, déduplication, refetch), les loaders de React Router, ou les Server Components/`use()` dans les frameworks.

### 14. Qu'est-ce que `useRef` et ses deux usages ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un conteneur mutable `{ current }` persistant entre rendus sans déclencher de re-rendu. Usage 1 : référencer un élément DOM (`ref={inputRef}`, focus, mesure). Usage 2 : stocker une valeur mutable (timer id, valeur précédente, flag) qui ne doit pas participer au rendu.

### 15. Qu'est-ce que `useReducer` et quand le préférer à `useState` ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un hook gérant l'état via un reducer `(state, action) => newState`, comme Redux en local. À préférer quand l'état a plusieurs sous-valeurs liées, des transitions complexes ou dépendantes de l'état précédent : la logique est centralisée, testable et les actions documentent les intentions.

### 16. Qu'est-ce que le Context API et ses limites de performance ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `createContext`/`useContext` partagent une valeur avec tout un sous-arbre sans props drilling (thème, utilisateur, locale). Limite : tout consommateur se re-rend à chaque changement de la valeur, même partiel. Solutions : découper en plusieurs contextes, mémoïser la valeur, ou utiliser un store avec sélecteurs (Zustand, Jotai) pour l'état fréquemment modifié.

### 17. Qu'est-ce que `React.memo` et quand est-il utile ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un HOC qui évite le re-rendu d'un composant si ses props sont identiques (comparaison superficielle). Utile pour les composants coûteux recevant des props stables ; inutile (voire contre-productif) si les props changent à chaque rendu (objets/fonctions non mémoïsés). Le React Compiler automatise progressivement cette mémoïsation.

### 18. Qu'est-ce que le React Compiler ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un compilateur (stable en 2025 avec React 19) qui analyse les composants et insère automatiquement la mémoïsation (`useMemo`, `useCallback`, `memo`) là où c'est sûr, à condition que le code respecte les règles de React (pureté, immutabilité). Il réduit les re-rendus inutiles sans optimisation manuelle.

### 19. Qu'est-ce que le StrictMode et pourquoi les effets s'exécutent-ils deux fois en développement ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `<StrictMode>` active des vérifications de développement : double invocation des rendus et des effets (montage → nettoyage → montage) pour détecter les effets non idempotents ou sans nettoyage, avertissements sur les APIs dépréciées. Aucun impact en production.

### 20. Qu'est-ce qu'une Error Boundary ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un composant classe implémentant `static getDerivedStateFromError`/`componentDidCatch` qui capture les erreurs de rendu de ses enfants et affiche une UI de repli au lieu de démonter toute l'application. Elle ne capture pas les erreurs dans les gestionnaires d'événements ni le code asynchrone. `react-error-boundary` fournit une version pratique.

### 21. Qu'est-ce que Suspense et comment fonctionne-t-il avec le lazy loading et les données ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `<Suspense fallback={<Spinner/>}>` affiche un fallback tant qu'un enfant « suspend » (promesse en cours) : `React.lazy` pour le code splitting, et les sources de données compatibles (frameworks, TanStack Query avec `useSuspenseQuery`, hook `use()` de React 19). Les frontières Suspense structurent le streaming SSR.

### 22. Que sont les transitions (`useTransition`, `startTransition`) et `useDeferredValue` ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Elles marquent une mise à jour comme non urgente : React garde l'UI réactive (saisie) et peut interrompre le rendu coûteux (filtrage d'une grande liste). `useTransition` fournit `isPending` ; `useDeferredValue` retarde une valeur dérivée. Elles reposent sur le rendu concurrent de React 18.

### 23. Qu'est-ce que le rendu concurrent (Concurrent Rendering) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Depuis React 18 (`createRoot`), React peut préparer plusieurs versions de l'UI, interrompre et reprendre un rendu, prioriser les mises à jour urgentes. Cela rend possible Suspense pour les données, les transitions, le streaming SSR et l'hydration sélective. Le code doit être pur car un rendu peut être abandonné.

### 24. Différence entre composant contrôlé et non contrôlé ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Contrôlé : la valeur du champ vient de l'état React (`value` + `onChange`), source de vérité unique, validation immédiate. Non contrôlé : le DOM garde la valeur, lue via `ref` ou `FormData` à la soumission ; plus simple et performant pour les gros formulaires (React Hook Form s'appuie dessus).

### 25. Quelles librairies de formulaires et pourquoi ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** React Hook Form (non contrôlé, performant, API hooks, validation via Zod/Yup avec resolvers), Formik (contrôlé, plus ancien), TanStack Form. Elles gèrent état, validation, erreurs, champs dynamiques. React 19 ajoute les Actions et `useActionState`/`useFormStatus` pour les soumissions natives.

### 26. Qu'est-ce que React 19 apporte (Actions, `use`, ref as prop, Server Components) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Actions : fonctions asynchrones passées à `<form action>` avec état de pending/erreur (`useActionState`, `useOptimistic`). Hook `use()` pour lire une promesse ou un contexte conditionnellement. `ref` devient une prop normale (fin de `forwardRef`). Support stable des Server Components et du React Compiler, métadonnées `<title>` dans les composants.

### 27. Qu'est-ce qu'un React Server Component (RSC) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un composant exécuté uniquement côté serveur (au build ou à la requête), qui peut accéder directement aux données (base, fichiers) et n'envoie pas son code au client, réduisant le bundle. Il ne peut pas utiliser d'état ni d'effets ; les parties interactives sont des Client Components (`'use client'`). Next.js App Router les implémente.

### 28. Différence entre Server Components et SSR classique ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Le SSR rend des composants clients en HTML sur le serveur puis les hydrate (tout le JS est envoyé). Les RSC ne sont jamais hydratés : leur sortie est un format sérialisé (RSC payload) fusionné côté client, et leur code n'existe pas dans le bundle. Les deux se combinent : les RSC contiennent des Client Components rendus en SSR.

### 29. Qu'est-ce que les Server Actions / Server Functions ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Des fonctions marquées `'use server'` appelables depuis des composants clients (formulaires, événements) et exécutées sur le serveur comme un endpoint RPC généré automatiquement. Elles simplifient les mutations sans écrire d'API, mais exigent validation des entrées et contrôle d'autorisation comme tout endpoint public.

### 30. Comment gérer le routage dans une application React ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** React Router (déclaratif, loaders/actions pour les données, routes imbriquées, `lazy`), TanStack Router (typage complet des routes et paramètres), ou le routage par fichiers des frameworks (Next.js, Remix). Points d'attention : code splitting par route, gestion du scroll, focus pour l'accessibilité, routes protégées.

### 31. Qu'est-ce que Zustand, Jotai et Redux Toolkit, et comment choisir ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Redux Toolkit : store global unique, actions/reducers, devtools puissants, verbeux mais structurant pour les grosses équipes. Zustand : store minimaliste par hook, sélecteurs, peu de boilerplate. Jotai : état atomique bottom-up (atomes composables). Choisir selon la taille de l'équipe et la complexité ; TanStack Query pour l'état serveur dans tous les cas.

### 32. Comment tester des composants React (React Testing Library) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** RTL rend le composant dans jsdom et interroge le DOM comme un utilisateur (`getByRole`, `getByLabelText`, `findByText`) plutôt que par implémentation ; `userEvent` simule les interactions réelles. Avec Vitest/Jest et MSW pour simuler l'API. Principe : tester le comportement observable, pas l'état interne.

### 33. Qu'est-ce que MSW (Mock Service Worker) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Une librairie qui intercepte les requêtes réseau au niveau du navigateur (Service Worker) ou de Node, pour renvoyer des réponses simulées définies par handlers. Les mêmes mocks servent aux tests unitaires, Storybook et développement local, sans modifier le code de l'application.

### 34. Comment styliser une application React (CSS Modules, Tailwind, CSS-in-JS) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** CSS Modules : classes locales générées, simple et performant. Tailwind : classes utilitaires, rapidité de développement, cohérence via configuration. CSS-in-JS (styled-components, Emotion) : styles dynamiques dans le JS, mais coût runtime et incompatibilité avec les Server Components ; les solutions zéro-runtime (vanilla-extract, Panda, StyleX) corrigent cela.

### 35. Qu'est-ce que le props drilling et les alternatives (composition, contexte) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Passer une prop à travers plusieurs niveaux intermédiaires qui ne l'utilisent pas. Alternatives : composition (passer des composants en `children` ou props pour que le parent assemble directement), Context pour les valeurs transverses stables, store pour l'état partagé fréquemment modifié.

### 36. Qu'est-ce que le pattern Compound Components ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un ensemble de composants conçus pour fonctionner ensemble en partageant un état implicite via contexte (`<Tabs><Tabs.List/><Tabs.Panel/></Tabs>`), offrant une API déclarative flexible. Très utilisé dans les librairies UI headless (Radix, Headless UI, React Aria).

### 37. Que sont les composants « headless » (Radix, React Aria, Headless UI) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Des composants fournissant comportement, accessibilité (ARIA, clavier, focus) et état, sans style imposé. On les habille avec ses propres styles (souvent Tailwind, comme shadcn/ui). Ils évitent de réimplémenter la logique complexe d'accessibilité des menus, dialogues, combobox.

### 38. Comment gérer les listes longues efficacement (virtualisation) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Ne rendre que les éléments visibles avec une librairie de virtualisation (TanStack Virtual, react-window), fournir des `key` stables (id, jamais l'index si la liste change), mémoïser les items, et paginer/charger à la demande côté serveur. Des milliers de nœuds DOM dégradent rendu et mémoire.

### 39. Comment profiler et optimiser les performances d'une application React ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** React DevTools Profiler (temps de rendu, causes de re-rendu, « Highlight updates »), `why-did-you-render`, Chrome Performance. Leviers : éviter les re-rendus (structure de l'état, `memo`, sélecteurs), code splitting, virtualisation, transitions, Web Workers pour les calculs, et éviter les objets/fonctions recréés dans les props.

### 40. Qu'est-ce qu'un portail (`createPortal`) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Un moyen de rendre des enfants dans un nœud DOM situé hors de la hiérarchie du parent (modales, tooltips, toasts attachés à `body`) tout en conservant le contexte React et la propagation des événements dans l'arbre React. Il évite les problèmes de `z-index` et `overflow: hidden`.

### 41. Comment gérer les effets de bord asynchrones proprement (annulation, courses) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Dans un effet : `AbortController` passé au fetch et `abort()` dans le nettoyage, ou un flag `ignore` pour ignorer les réponses obsolètes. Mieux : déléguer à TanStack Query/SWR qui gèrent annulation, déduplication et états. Les hooks custom (`useFetch`) sans ces précautions sont une source classique de bugs.

### 42. Qu'est-ce que l'hydration mismatch et comment l'éviter ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Une différence entre le HTML rendu par le serveur et le premier rendu client (date, `window`, contenu aléatoire, extensions navigateur) provoque un avertissement et un re-rendu complet. Éviter : rendre le contenu dépendant du client après montage (`useEffect` + état), `suppressHydrationWarning` ponctuel, et garder les données identiques.

### 43. Comment intégrer TypeScript avec React (typage des props, événements, génériques) ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Typer les props par interface, `React.FC` optionnel (préférer une fonction avec props typées), `children: React.ReactNode`, événements `React.ChangeEvent<HTMLInputElement>`, composants génériques (`<T,>(props: Props<T>)`), `ComponentProps<typeof X>` pour étendre des props, et `satisfies` pour les objets de configuration.

### 44. Qu'est-ce que Next.js App Router vs Pages Router ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Pages Router (historique) : routage par fichiers avec `getServerSideProps`/`getStaticProps`, composants clients. App Router (Next 13+) : dossier `app/`, Server Components par défaut, layouts imbriqués, streaming, Server Actions, `fetch` avec cache et revalidation intégrés. Les deux coexistent ; les nouveaux projets utilisent App Router.

### 45. Comment gérer l'authentification dans une application React/Next ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Côté SPA : Authorization Code + PKCE avec une librairie (oidc-client-ts, Auth0/Keycloak SDK), tokens en mémoire, refresh silencieux. Côté Next.js : sessions par cookie `HttpOnly` via Auth.js/NextAuth ou un BFF, vérification dans le middleware et les Server Components. Toujours protéger aussi les endpoints et Server Actions.

### 46. Comment structurer un projet React de grande taille ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Organisation par feature (dossier `features/orders` avec composants, hooks, api, tests) plutôt que par type, un dossier `shared`/`ui` pour les composants génériques, règles d'import (ESLint boundaries), barrel files avec parcimonie (impact tree shaking), et éventuellement un monorepo (Nx, Turborepo) pour partager le design system.

### 47. Qu'est-ce que Vite et pourquoi a-t-il remplacé Create React App ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Vite sert les modules ES natifs en développement (démarrage instantané, HMR rapide) et utilise Rollup/Rolldown pour le build. CRA (Webpack, non maintenu) est officiellement déprécié ; la documentation React recommande un framework (Next.js, React Router en mode framework) ou Vite pour une SPA.

### 48. Comment gérer l'accessibilité dans React ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** HTML sémantique, `htmlFor` sur les labels, gestion du focus (refs, `autoFocus` avec prudence), composants headless pour les widgets complexes, `eslint-plugin-jsx-a11y`, tests avec `jest-axe`/RTL par rôle, annonces via live regions, et respect des préférences utilisateur. Les fragments (`<>`) évitent les `div` inutiles qui cassent la sémantique des listes/tableaux.

### 49. Différence entre `key` et `ref`, et pourquoi changer la `key` réinitialise-t-il un composant ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** `key` identifie un élément dans une liste pour la réconciliation ; `ref` donne accès à une instance/DOM. Changer la `key` d'un composant force React à le démonter et remonter (état réinitialisé), technique utile pour réinitialiser un formulaire quand l'entité éditée change.

### 50. Comment partager de la logique entre composants sans HOC ?
`🟠 Intermédiaire` · Sujet : **React**

**Réponse :** Custom hooks (`useDebounce`, `useLocalStorage`, `useAuth`) qui encapsulent état et effets réutilisables, composition via `children`/render props pour la structure, et utilitaires purs. Les hooks se testent avec `renderHook` de RTL. Un hook ne rend rien : la logique est séparée de la présentation.
