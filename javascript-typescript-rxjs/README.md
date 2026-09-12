# 📜 JavaScript, TypeScript & RxJS

> Closures, event loop, types, generics, Observables, operators

**20 questions**

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
