# 📜 JavaScript, TypeScript & RxJS

> Closures, event loop, types, generics, Observables, operators

**51 questions**

---

### 1. Quel est l'intérêt du typage statique en TypeScript par rapport à JavaScript ?
`🟢 Débutant` · Sujet : **TypeScript**

**Réponse :** Détecte les erreurs de type à la compilation plutôt qu'à l'exécution, améliore l'autocomplétion/documentation, facilite la maintenance de grands projets.

### 2. Différence entre `mergeMap` et `switchMap` ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** `mergeMap` traite toutes les émissions en parallèle. `switchMap` annule l'Observable interne précédent dès qu'une nouvelle valeur source arrive.

### 3. Différence entre `var`, `let` et `const` ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** `var` portée fonctionnelle, hoisting. `let`/`const` portée de bloc ; `let` réassignable, `const` non réassignable (mutation d'objet possible).

### 4. Qu'est-ce qu'un type générique ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Permet d'écrire des composants réutilisables pour plusieurs types en conservant la sécurité de typage (ex: `function identity<T>(arg: T): T`).

### 5. Qu'est-ce qu'un Observable ?
`🟢 Débutant` · Sujet : **RxJS**

**Réponse :** Source de données asynchrone émettant une séquence de valeurs dans le temps, à laquelle on s'abonne.

### 6. Différence arrow function / fonction classique pour `this` ?
`🟢 Débutant` · Sujet : **JavaScript**

**Réponse :** Arrow function hérite du `this` lexical englobant. Fonction classique définit son propre `this` selon l'appel.

### 7. À quoi sert une interface ?
`🟢 Débutant` · Sujet : **TypeScript**

**Réponse :** Définit la forme attendue d'un objet (propriétés/types) sans implémentation.

### 8. Différence `Subject` / `BehaviorSubject` ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Subject sans valeur initiale, pas de rediffusion. BehaviorSubject conserve et transmet la dernière valeur aux nouveaux abonnés.

### 9. Qu'est-ce qu'un type union ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Type composé permettant plusieurs types possibles, noté `|` (ex: `string | number`).

### 10. Qu'est-ce que l'event loop ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Mécanisme permettant à JS (mono-thread) de gérer l'asynchrone en déléguant les tâches longues puis traitant les callbacks via une file d'attente.

### 11. Mode `strict` ?
`🟢 Débutant` · Sujet : **TypeScript**

**Réponse :** Ensemble d'options de compilation (strictNullChecks, noImplicitAny) pour des vérifications plus rigoureuses.

### 12. `debounceTime` ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Retarde l'émission tant qu'une nouvelle valeur arrive avant expiration du délai, utile pour limiter les appels API.

### 13. Différence `null` / `undefined` ?
`🟢 Débutant` · Sujet : **JavaScript**

**Réponse :** undefined = non initialisé. null = absence volontaire de valeur.

### 14. Type intersection ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Combine plusieurs types via `&`, la valeur devant satisfaire toutes les propriétés combinées.

### 15. Différence `of()` / `from()` ?
`🟢 Débutant` · Sujet : **RxJS**

**Réponse :** of() émet les arguments tels quels. from() convertit une source itérable en Observable.

### 16. Qu'est-ce qu'une closure ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Fonction conservant l'accès aux variables de son scope lexical même après exécution de la fonction englobante.

### 17. Pourquoi éviter `any` ?
`🟢 Débutant` · Sujet : **TypeScript**

**Réponse :** Désactive la vérification de type, annulant les bénéfices de TypeScript ; préférer `unknown`.

### 18. Qu'est-ce que `catchError` ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Intercepte une erreur émise, permettant de la gérer plutôt que de laisser le flux s'interrompre.

### 19. Qu'est-ce qu'un mapped type ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Crée un nouveau type en transformant les propriétés d'un type existant (ex: Partial<T>, Readonly<T>).

### 20. Différence `Promise.all()` / `Promise.race()` ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** all() attend toutes les promesses. race() se résout/rejette dès la première terminée.

### 21. Différence entre `==` et `===` ?
`🟢 Débutant` · Sujet : **JavaScript**

**Réponse :** `==` effectue une coercition de type avant comparaison (`'1' == 1` est vrai, `null == undefined` est vrai), ce qui produit des résultats surprenants. `===` compare valeur et type sans conversion. Toujours utiliser `===` sauf le cas idiomatique `x == null` pour tester null ou undefined d'un coup.

### 22. Qu'est-ce que le hoisting ?
`🟢 Débutant` · Sujet : **JavaScript**

**Réponse :** Les déclarations `var` et `function` sont « remontées » en tête de leur scope à la compilation : une `var` vaut `undefined` avant son affectation. `let`/`const`/`class` sont aussi hoistées mais restent dans la Temporal Dead Zone jusqu'à leur ligne de déclaration, d'où une `ReferenceError` si on les utilise avant.

### 23. Qu'est-ce que la chaîne de prototypes ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Chaque objet possède un lien interne `[[Prototype]]` vers un autre objet. Lors de l'accès à une propriété absente, le moteur remonte la chaîne jusqu'à `Object.prototype` puis `null`. Les classes ES6 sont du sucre syntaxique sur ce mécanisme (`class A extends B` définit `A.prototype.__proto__ === B.prototype`).

### 24. Différence entre `call`, `apply` et `bind` ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Les trois fixent la valeur de `this`. `call(thisArg, a, b)` et `apply(thisArg, [a, b])` invoquent immédiatement la fonction (arguments individuels vs tableau). `bind(thisArg)` retourne une nouvelle fonction liée sans l'exécuter, utile pour les callbacks.

### 25. Différence entre microtâches et macrotâches dans l'event loop ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Après chaque macrotâche (setTimeout, I/O, événements), le moteur vide entièrement la file des microtâches (`Promise.then`, `queueMicrotask`, `MutationObserver`) avant de rendre la main. C'est pourquoi un `.then` s'exécute avant un `setTimeout(fn, 0)`, et pourquoi une boucle infinie de microtâches bloque le rendu.

### 26. Comment fonctionne `async/await` sous le capot ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Une fonction `async` retourne toujours une Promise. `await` suspend l'exécution de la fonction (sans bloquer le thread) et reprend dans une microtâche quand la Promise se résout ; un rejet devient une exception attrapable par `try/catch`. Attention aux `await` séquentiels inutiles : utiliser `Promise.all` pour paralléliser.

### 27. Différence entre `Promise.all`, `allSettled`, `any` ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** `all` rejette dès la première erreur. `allSettled` attend tout et renvoie un tableau `{status, value|reason}` sans jamais rejeter. `any` résout avec la première Promise réussie et ne rejette (`AggregateError`) que si toutes échouent. `race` prend la première terminée, succès ou échec.

### 28. Qu'est-ce que la déstructuration et le spread/rest ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** La déstructuration extrait des valeurs d'objets/tableaux : `const { id, name = 'x' } = user`. Le spread `...` étale un itérable ou copie superficiellement un objet (`{ ...a, b: 1 }`). Le rest regroupe le reste dans un tableau/objet (`(first, ...others) => ...`). Attention : le spread ne fait qu'une copie de premier niveau.

### 29. Comment réaliser une copie profonde d'un objet ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** `structuredClone(obj)` (natif, gère Date, Map, Set, références circulaires, mais pas les fonctions). `JSON.parse(JSON.stringify(obj))` est un raccourci qui perd `undefined`, les dates (deviennent des chaînes) et les fonctions. Pour des besoins avancés : `lodash.cloneDeep`.

### 30. Différence entre `Map`/`Set` et objets/tableaux ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** `Map` accepte n'importe quel type de clé (objets inclus), conserve l'ordre d'insertion, expose `size`, et évite les collisions avec le prototype. `Set` stocke des valeurs uniques avec `has` en O(1). `WeakMap`/`WeakSet` ne retiennent pas leurs clés objets, permettant le garbage collection (caches, métadonnées privées).

### 31. Qu'est-ce qu'un générateur et un itérateur ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Un itérateur est un objet avec une méthode `next()` renvoyant `{value, done}`. Un générateur (`function*`) produit un itérateur à la demande via `yield`, avec exécution suspendue entre chaque valeur : utile pour les séquences paresseuses/infinies. `async function*` et `for await` gèrent les flux asynchrones.

### 32. Différence entre modules ES (`import/export`) et CommonJS (`require`) ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** ESM est statique (analysable pour le tree-shaking, imports résolus à la compilation, `import()` dynamique retourne une Promise), asynchrone et strict par défaut. CommonJS est synchrone et dynamique, historique de Node. Node supporte les deux (`"type": "module"`, `.mjs`/`.cjs`) mais l'interop reste une source classique de bugs.

### 33. Qu'est-ce que le debounce et le throttle ?
`🟠 Intermédiaire` · Sujet : **JavaScript**

**Réponse :** Debounce retarde l'exécution jusqu'à ce qu'aucun appel n'ait eu lieu pendant N ms (recherche à la saisie). Throttle garantit au plus une exécution toutes les N ms (scroll, resize). Les deux limitent le nombre d'appels coûteux ; RxJS fournit `debounceTime` et `throttleTime`.

### 34. Différence entre `interface` et `type` ?
`🟢 Débutant` · Sujet : **TypeScript**

**Réponse :** Les deux décrivent des formes. `interface` supporte la fusion de déclarations et `extends`, idéale pour les objets et les APIs publiques. `type` est plus général : unions, tuples, types conditionnels, mapped types, alias de primitives. En pratique : interface pour les objets, type pour tout le reste.

### 35. Différence entre `unknown` et `any` ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** `any` désactive le typage : on peut tout faire dessus sans erreur. `unknown` est le type « top » sûr : on ne peut rien faire avec avant d'avoir affiné le type (typeof, instanceof, type guard). À utiliser pour les entrées externes (JSON, catch d'erreur).

### 36. Qu'est-ce qu'un type guard et un prédicat de type ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Un type guard est une expression qui affine un type dans une branche (`typeof x === 'string'`, `'id' in obj`, `x instanceof Date`). Un prédicat de type est une fonction retournant `x is Foo`, permettant de créer ses propres guards réutilisables, par exemple pour valider une réponse d'API.

### 37. À quoi servent les utility types `Partial`, `Pick`, `Omit`, `Record`, `Readonly` ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Ils dérivent de nouveaux types sans duplication : `Partial<T>` rend tout optionnel (patch), `Required<T>` l'inverse, `Pick<T, K>`/`Omit<T, K>` sélectionnent/excluent des clés (DTO), `Record<K, V>` crée un dictionnaire typé, `Readonly<T>` interdit la mutation, `ReturnType<F>` extrait le type de retour.

### 38. Qu'est-ce qu'un type conditionnel et le mot-clé `infer` ?
`🔴 Avancé` · Sujet : **TypeScript**

**Réponse :** `T extends U ? X : Y` choisit un type selon une condition, distribué sur les unions. `infer` capture un type dans la branche `extends` : `type Unwrap<T> = T extends Promise<infer U> ? U : T`. C'est la base des utility types avancés (`ReturnType`, `Parameters`, `Awaited`).

### 39. Qu'est-ce qu'une union discriminée et le narrowing exhaustif ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Une union d'objets partageant un champ littéral (`kind: 'circle' | 'square'`). Un `switch (shape.kind)` affine automatiquement le type dans chaque branche, et un `default` assignant à `never` fait échouer la compilation si un cas est oublié. C'est le pattern idéal pour modéliser des états (loading/success/error).

### 40. Différence entre `enum` et union de littéraux ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** `enum` génère du code à l'exécution (objet bidirectionnel pour les enums numériques) et n'est pas toujours tree-shakable ; `const enum` est inliné mais fragile avec certains bundlers. Une union de littéraux (`type Status = 'A' | 'B'`) ou un objet `as const` est plus léger, sûr et interopérable avec le JSON.

### 41. Que fait `as const` et le `satisfies` operator ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** `as const` fige un littéral en readonly avec ses types littéraux les plus précis (`['a','b'] as const` → `readonly ['a','b']`). `satisfies T` (TS 4.9) vérifie qu'une valeur respecte un type sans élargir son type inféré : on garde l'autocomplétion précise tout en validant la structure.

### 42. Qu'est-ce que la variance et pourquoi les paramètres de méthode sont-ils bivariants en TS ?
`🔴 Avancé` · Sujet : **TypeScript**

**Réponse :** La covariance permet d'utiliser un sous-type là où un supertype est attendu (retours), la contravariance l'inverse (paramètres). TypeScript vérifie les paramètres de fonctions de façon contravariante avec `strictFunctionTypes`, mais reste bivariant pour la syntaxe méthode, pour compatibilité avec le DOM. Cela peut laisser passer des affectations non sûres.

### 43. Que sont les décorateurs et quelle est la différence entre legacy et standard (TS 5) ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Un décorateur est une fonction appliquée à une classe, méthode ou propriété. Les décorateurs « experimental » (utilisés par Angular/NestJS, `experimentalDecorators`) reposent sur `reflect-metadata` ; les décorateurs standard TC39 (TS 5.0+) ont une signature différente, pas de métadonnées de paramètres et ne sont pas encore adoptés par Angular.

### 44. Que signifie `strictNullChecks` et comment gérer les valeurs optionnelles ?
`🟠 Intermédiaire` · Sujet : **TypeScript**

**Réponse :** Avec cette option, `null` et `undefined` ne sont plus assignables à tout type : `string | undefined` doit être affiné avant usage. Outils : optional chaining `a?.b`, nullish coalescing `a ?? 'x'`, assertion non-null `a!` (à éviter), et types utilitaires `NonNullable<T>`.

### 45. Différence entre observable froid et chaud ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Un observable froid crée une nouvelle source par abonné (chaque `subscribe` sur `http.get` relance la requête). Un observable chaud partage une source unique déjà active (`Subject`, `fromEvent`). `share()`/`shareReplay()` transforment un froid en chaud pour éviter les appels dupliqués.

### 46. Différence entre `concatMap`, `mergeMap`, `switchMap` et `exhaustMap` ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Tous aplatissent un observable interne. `mergeMap` exécute en parallèle sans ordre. `concatMap` met en file d'attente et préserve l'ordre (sauvegardes). `switchMap` annule l'interne précédent (autocomplete, navigation). `exhaustMap` ignore les nouvelles émissions tant que l'interne est en cours (anti double-clic sur un bouton de soumission).

### 47. Différence entre `combineLatest`, `forkJoin`, `zip` et `withLatestFrom` ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** `combineLatest` émet à chaque changement d'une source une fois que toutes ont émis. `forkJoin` attend la complétion de toutes et émet une seule fois (équivalent de `Promise.all`). `zip` apparie les émissions par index. `withLatestFrom` émet au rythme de la source principale en joignant la dernière valeur des autres.

### 48. Qu'est-ce que `shareReplay` et quel piège de fuite mémoire pose-t-il ?
`🔴 Avancé` · Sujet : **RxJS**

**Réponse :** `shareReplay(n)` multicaste et rejoue les n dernières valeurs aux nouveaux abonnés (cache d'un appel HTTP). Avec `refCount: false` (défaut), la source reste abonnée même sans consommateur, ce qui peut retenir des ressources indéfiniment. Utiliser `shareReplay({ bufferSize: 1, refCount: true })` ou `share({ resetOnRefCountZero })`.

### 49. Comment gérer les erreurs sans terminer le flux ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Une erreur termine l'observable. Pour survivre, placer `catchError` dans l'observable interne d'un `switchMap`/`mergeMap` (retourner `of(fallback)` ou `EMPTY`), plutôt qu'en bout de chaîne. `retry({ count, delay })` permet de relancer avec backoff. `finalize` exécute un nettoyage quel que soit l'issue.

### 50. Différence entre les Schedulers RxJS (`asyncScheduler`, `asapScheduler`, `queueScheduler`) ?
`🔴 Avancé` · Sujet : **RxJS**

**Réponse :** Un scheduler contrôle quand et où une émission s'exécute. `queueScheduler` est synchrone (file FIFO), `asapScheduler` utilise une microtâche, `asyncScheduler` un `setTimeout` (macrotâche), `animationFrameScheduler` `requestAnimationFrame`. On les injecte via `observeOn`/`subscribeOn` ou en paramètre d'opérateurs temporels, notamment pour rendre les tests déterministes.

### 51. Qu'est-ce que le marble testing ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Une technique de test décrivant les flux par des diagrammes textuels (`'-a-b-|'`) avec `TestScheduler`. Le temps est virtuel, ce qui rend les tests de `debounceTime`, `delay` ou `retry` instantanés et déterministes. `expectObservable(source$).toBe('--a--|', { a: 1 })` compare le flux attendu.
