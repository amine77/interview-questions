# 🅰️ Angular

> Signals, standalone components, control flow, SSR, Zoneless, RxJS integration

**151 questions**

---

### 1. Que sont les `Guards` en Angular et à quoi servent-ils ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Interfaces (`CanActivate`, `CanDeactivate`, `Resolve`, etc.) permettant de contrôler l'accès à une route, par exemple pour vérifier une authentification avant de charger un composant.

### 2. Détection de changement OnPush ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Limite la vérification aux cas où une référence @Input change, un événement est déclenché, ou un Observable async émet, améliorant les performances.

### 3. Qu'est-ce qu'un service Angular ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Classe `@Injectable()` encapsulant une logique réutilisable, injectée via le DI Angular.

### 4. À quoi sert un Resolver ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Pré-charge des données avant l'activation d'une route, évitant un état de chargement intermédiaire.

### 5. Formes du data binding en Angular ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Interpolation `{{ }}`, property binding `[prop]`, event binding `(event)`, two-way binding `[(ngModel)]`.

### 6. Pipe personnalisé ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Classe `@Pipe` implémentant `PipeTransform` pour transformer une donnée dans le template.

### 7. NgModule vs standalone components ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** NgModule regroupe composants/directives/pipes liés. Standalone (Angular 14+) simplifie en déclarant directement les imports.

### 8. Rôle de HttpClientModule / provideHttpClient ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Fournit le service HttpClient pour requêtes HTTP retournant des Observables.

### 9. Qu'est-ce que les Signals en Angular et quel problème résolvent-ils ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** Les Signals sont un système réactif de gestion d'état introduit progressivement depuis Angular 16 et stabilisé dans les versions récentes. Ils permettent une détection de changement fine (granulaire) sans dépendre de Zone.js, réduisant le nombre de vérifications inutiles et améliorant les performances.

### 10. Qu'est-ce que le nouveau contrôle de flux natif (@if, @for, @switch) en Angular ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** Introduit dans Angular 17+, il remplace les directives structurelles *ngIf, *ngFor, *ngSwitch par une syntaxe intégrée au template compilée directement par Angular, améliorant les performances (pas besoin d'importer CommonModule) et la lisibilité du code.

### 11. Comment optimiser le temps de chargement initial d'une application Angular ?
`🟠 Intermédiaire` · Sujet : **Optimisation Angular**

**Réponse :** Via le lazy loading des modules/routes, le tree-shaking pour éliminer le code mort, la compilation AOT (Ahead-of-Time), et la réduction de la taille des bundles (code splitting, compression).

### 12. Qu'est-ce que inject() et pourquoi remplace-t-il progressivement l'injection par constructeur ?
`🟢 Débutant` · Sujet : **Angular 21**

**Réponse :** Fonction permettant de récupérer une dépendance directement dans le corps d'une classe ou fonction (hors constructeur), utile pour les composants standalone, guards fonctionnels ou factory functions.

### 13. Qu'est-ce que le "Deferred Loading" (@defer) en Angular ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** Bloc de template différant le chargement d'une partie de l'UI jusqu'à une condition (viewport, interaction, idle), réduisant le bundle initial et améliorant le LCP.

### 14. Host binding et host listener ?
`🟢 Débutant` · Sujet : **Angular 21**

**Réponse :** @HostBinding lie une propriété de l'élément hôte. @HostListener écoute un événement DOM sur cet hôte depuis la classe du composant.

### 15. Zoneless Change Detection ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** Mode permettant de faire fonctionner Angular sans Zone.js, en s'appuyant sur les Signals, réduisant le bundle et améliorant les performances.

### 16. linkedSignal() et son usage ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** Signal dérivé d'un autre signal mais dont la valeur peut être réinitialisée localement, utile pour synchroniser un état de formulaire avec des données externes.

### 17. Composant standalone et son avantage ?
`🟢 Débutant` · Sujet : **Angular 21**

**Réponse :** Composant déclarant ses propres imports sans NgModule, simplifiant l'arborescence et facilitant tree-shaking/lazy loading.

### 18. Hydration Angular Universal et interaction avec @defer ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** L'hydration réutilise le DOM serveur. Les blocs @defer nécessitent une stratégie de placeholder cohérente en SSR pour éviter le CLS.

### 19. resource() dans les Signals Angular ?
`🟠 Intermédiaire` · Sujet : **Angular 21**

**Réponse :** API gérant des données asynchrones directement dans le modèle Signals, exposant chargement/erreur/valeur automatiquement.

### 20. Quel est le cycle de vie d'un composant Angular et quels hooks sont les plus utilisés ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Ordre principal : `constructor` → `ngOnChanges` (à chaque changement d'`@Input`) → `ngOnInit` (initialisation, appels HTTP) → `ngDoCheck` → `ngAfterContentInit/Checked` → `ngAfterViewInit/Checked` (accès aux `@ViewChild`) → `ngOnDestroy` (désabonnement, nettoyage). Avec les Signals, `effect()` et `computed()` remplacent une partie de ces hooks.

### 21. Différence entre `@Input()` / `@Output()` et les nouvelles fonctions `input()` / `output()` ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Les décorateurs classiques exposent des propriétés mutables et un `EventEmitter`. Les fonctions `input()` (Angular 17.1+) créent des Signals en lecture seule (`input.required<T>()` pour rendre obligatoire), et `output()` produit un émetteur typé sans dépendance RxJS. Avantage : réactivité fine et typage strict à la compilation.

### 22. Qu'est-ce que `model()` et comment implémenter un two-way binding sur un composant custom ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `model<T>()` crée un Signal modifiable partagé entre parent et enfant : le parent écrit `[(value)]="x"` et l'enfant appelle `value.set(...)`. Avant Angular 17.2, il fallait un `@Input() value` associé à un `@Output() valueChange` respectant la convention de nommage.

### 23. Différence entre `ngIf` / `*ngFor` et le contrôle de flux `@if` / `@for` ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Les directives structurelles reposent sur des modules importés et une syntaxe micro-template. `@if`/`@for`/`@switch` sont intégrés au compilateur : pas d'import, meilleure performance, `@for` exige un `track` (évite les re-rendus complets) et propose un bloc `@empty`. Une migration automatique existe (`ng g @angular/core:control-flow`).

### 24. Différence entre Reactive Forms et Template-driven Forms ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Template-driven : logique dans le template via `ngModel`, simple pour les petits formulaires, validation asynchrone moins pratique. Reactive Forms : modèle explicite en TypeScript (`FormGroup`, `FormControl`, `FormBuilder`), typés depuis Angular 14, testables, validateurs composables et flux `valueChanges` observable. Recommandés pour les formulaires complexes.

### 25. Comment écrire un validateur personnalisé pour un Reactive Form ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un validateur est une fonction `(control: AbstractControl) => ValidationErrors | null`. Pour un validateur paramétré, on écrit une factory qui retourne cette fonction. Les validateurs asynchrones retournent un `Observable`/`Promise` et passent en troisième argument du `FormControl`. Un validateur cross-field se place sur le `FormGroup`.

### 26. Qu'est-ce qu'un `HttpInterceptor` et quels sont ses cas d'usage typiques ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un intercepteur (fonctionnel avec `HttpInterceptorFn` depuis Angular 15) s'insère dans la chaîne des requêtes HTTP pour les modifier ou réagir aux réponses. Cas d'usage : ajout du token `Authorization`, gestion centralisée des erreurs 401/500, spinner de chargement, retry, cache, journalisation.

### 27. Différence entre `providedIn: 'root'` et un provider déclaré dans un composant ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `providedIn: 'root'` crée un singleton applicatif tree-shakable. Un provider dans `providers` d'un composant crée une instance par composant (et ses enfants), détruite avec lui : utile pour un état local isolé. Les providers de routes (`providers` dans `Routes`) créent un scope par feature lazy-loaded.

### 28. Comment fonctionne la résolution hiérarchique de l'injection de dépendances ?
`🔴 Avancé` · Sujet : **Angular**

**Réponse :** Angular parcourt l'arbre des injecteurs de l'élément (ElementInjector) vers l'environnement (EnvironmentInjector : route, puis root, puis platform). Les décorateurs `@Optional()`, `@Self()`, `@SkipSelf()` et `@Host()` (ou les options de `inject()`) permettent de contrôler cette recherche.

### 29. Qu'est-ce qu'un `InjectionToken` et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un `InjectionToken<T>` permet d'injecter une valeur qui n'est pas une classe (configuration, chaîne, fonction, interface). Exemple : `new InjectionToken<AppConfig>('APP_CONFIG')` fourni via `useValue`/`useFactory`. Il évite les collisions de chaînes et conserve le typage.

### 30. Comment fonctionne le lazy loading des routes et quel gain apporte-t-il ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `loadComponent: () => import('./x.component')` (ou `loadChildren` pour un ensemble de routes) génère un chunk séparé chargé à la première navigation. Le bundle initial est réduit, donc LCP/TTI améliorés. On peut combiner avec une `PreloadingStrategy` (`PreloadAllModules` ou personnalisée) pour précharger en arrière-plan.

### 31. Qu'est-ce qu'un guard fonctionnel `CanActivateFn` et comment gérer une redirection ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Depuis Angular 15, un guard est une fonction utilisant `inject()` : `const authGuard: CanActivateFn = () => inject(AuthService).isLoggedIn() || inject(Router).createUrlTree(['/login'])`. Retourner un `UrlTree` redirige proprement. Il existe aussi `CanMatchFn` (évite même le chargement du chunk) et `CanDeactivateFn` (formulaire non sauvegardé).

### 32. Comment partager de l'état entre composants non liés ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Via un service singleton exposant un état réactif : Signals (`signal()` + `computed()` + méthodes de mutation), ou `BehaviorSubject` exposé en `asObservable()`. Pour les applications complexes : NgRx (Store/Effects), NgRx SignalStore, ou des bibliothèques légères comme Elf. Éviter les `@Input` en cascade sur plusieurs niveaux.

### 33. Qu'est-ce que la projection de contenu (`ng-content`) et les slots multiples ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `<ng-content>` insère le contenu passé entre les balises du composant. Avec `select="[header]"` on définit plusieurs slots nommés ; `ngProjectAs` permet de projeter un élément sous un autre sélecteur. Depuis Angular 18, `<ng-content>` peut avoir un contenu par défaut (fallback).

### 34. Différence entre `ng-template`, `ng-container` et `ngTemplateOutlet` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `ng-template` définit un bloc non rendu par défaut (référençable par `#tpl`). `ng-container` groupe des éléments sans ajouter de nœud DOM. `ngTemplateOutlet` rend un `TemplateRef` à la demande, avec un contexte (`{ $implicit, ... }`), base des composants « headless » et des tableaux configurables.

### 35. Qu'est-ce qu'une directive d'attribut et comment en créer une ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Une directive modifie le comportement/apparence d'un élément existant (ex : `[appHighlight]`). On la déclare avec `@Directive({ selector: '[appHighlight]', standalone: true })`, on injecte `ElementRef`/`Renderer2`, et on réagit via `host: { '(mouseenter)': 'onEnter()' }` ou `@HostListener`. La composition de directives (`hostDirectives`) permet de les réutiliser sur un composant.

### 36. Qu'est-ce que `effect()` et quelles précautions faut-il prendre ?
`🔴 Avancé` · Sujet : **Angular**

**Réponse :** `effect()` exécute une fonction chaque fois qu'un Signal lu à l'intérieur change, avec nettoyage via `onCleanup`. À utiliser pour les effets de bord (logging, localStorage, synchro avec une lib externe), pas pour dériver de l'état (préférer `computed()`). Écrire dans un Signal dans un effect est déconseillé (`allowSignalWrites` était nécessaire avant v19).

### 37. Comment interopérer entre Signals et RxJS ?
`🔴 Avancé` · Sujet : **Angular**

**Réponse :** `toSignal(obs$, { initialValue })` convertit un Observable en Signal (se désabonne automatiquement à la destruction) ; `toObservable(sig)` fait l'inverse. Pour les appels HTTP dépendant d'un Signal, `rxResource()` ou `httpResource()` (Angular 19/20) gèrent chargement, erreur et annulation.

### 38. Comment gérer les désabonnements et éviter les fuites mémoire ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Utiliser le pipe `async` dans le template (désabonnement automatique), `takeUntilDestroyed()` (avec `DestroyRef`), `toSignal()`, ou `take(1)`/`first()` pour les flux ponctuels. Les requêtes `HttpClient` complètent d'elles-mêmes, mais les `Subject`, `interval` et `fromEvent` doivent être fermés explicitement.

### 39. Différence entre `ViewChild` et `ContentChild`, et leurs équivalents Signals ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `@ViewChild` référence un élément du template du composant (disponible dans `ngAfterViewInit`), `@ContentChild` un élément projeté via `ng-content` (disponible dans `ngAfterContentInit`). Les versions Signals `viewChild()`, `viewChildren()`, `contentChild()` (Angular 17.2+) évitent les problèmes de timing et se composent avec `computed()`.

### 40. Qu'est-ce que le SSR avec Angular et à quoi sert `@angular/ssr` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Le rendu côté serveur génère le HTML initial sur Node/Express, améliorant le SEO et le First Contentful Paint. `@angular/ssr` (ex-Universal) s'ajoute via `ng add`, gère l'hydration non destructive, le `TransferState` pour éviter de rejouer les appels HTTP, et depuis Angular 19 le rendu hybride par route (`RenderMode.Server | Client | Prerender`).

### 41. Qu'est-ce que le rendu incrémental (Incremental Hydration) ?
`🔴 Avancé` · Sujet : **Angular**

**Réponse :** Introduit en Angular 19, il permet de ne pas hydrater immédiatement un bloc `@defer (hydrate on viewport)` : le HTML SSR reste affiché et le JavaScript n'est téléchargé/exécuté que lorsque le trigger se déclenche. Cela réduit drastiquement le JS initial et améliore le TTI sur les pages longues.

### 42. Comment configurer plusieurs environnements (dev, staging, prod) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Via `fileReplacements` dans `angular.json` (remplacer `environment.ts` par `environment.prod.ts` au build), ou, pour éviter de rebuilder par environnement, en chargeant une configuration runtime (`config.json` servi par le serveur, chargé dans un `provideAppInitializer`). La seconde approche respecte le principe « build once, deploy anywhere ».

### 43. Qu'est-ce qu'un `APP_INITIALIZER` / `provideAppInitializer` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un mécanisme exécutant une ou plusieurs fonctions (retournant `Promise`/`Observable`) avant le démarrage de l'application, par exemple pour charger la configuration ou initialiser l'authentification (Keycloak). Angular 19 le remplace par la fonction `provideAppInitializer(() => ...)`.

### 44. Quelles techniques pour réduire la taille du bundle Angular ?
`🟠 Intermédiaire` · Sujet : **Optimisation Angular**

**Réponse :** Build de production (tree-shaking, minification via esbuild), composants standalone, lazy loading, `@defer`, analyse avec `source-map-explorer`, budgets dans `angular.json`, éviter d'importer des librairies entières (lodash, moment → date-fns), images optimisées avec `NgOptimizedImage`, et suppression des polyfills inutiles.

### 45. À quoi sert la directive `NgOptimizedImage` ?
`🟠 Intermédiaire` · Sujet : **Optimisation Angular**

**Réponse :** `<img ngSrc>` impose les attributs `width`/`height` (évite le CLS), ajoute le `loading="lazy"` par défaut, `fetchpriority="high"` sur l'image marquée `priority` (LCP), génère `srcset` automatiquement et s'intègre à des CDN d'images via des loaders (Cloudinary, Imgix…).

### 46. Comment profiler la détection de changement et repérer un composant coûteux ?
`🔴 Avancé` · Sujet : **Optimisation Angular**

**Réponse :** Avec Angular DevTools (onglet Profiler) qui affiche le temps de rendu par composant à chaque cycle. Signaux d'alerte : fonctions appelées dans le template (recalculées à chaque cycle), pipes impurs, gros `@for` sans `track`, composants sans `OnPush`. Le passage en zoneless rend ces problèmes plus visibles car seuls les Signals/événements déclenchent un rendu.

### 47. Comment tester un composant Angular avec `TestBed` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `TestBed.configureTestingModule({ imports: [MyComponent], providers: [...] })`, puis `createComponent()` retourne un `ComponentFixture`. On interagit via `fixture.componentInstance`, on rafraîchit avec `fixture.detectChanges()`, et on interroge le DOM avec `fixture.debugElement.query(By.css(...))`. Pour HTTP : `provideHttpClientTesting()` et `HttpTestingController`.

### 48. Comment tester un service dépendant d'`HttpClient` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Fournir `provideHttpClient()` et `provideHttpClientTesting()`, injecter `HttpTestingController`, appeler la méthode du service, puis `httpMock.expectOne(url)` pour vérifier la requête et `.flush(data)` pour simuler la réponse. Terminer par `httpMock.verify()` pour s'assurer qu'aucune requête inattendue ne reste.

### 49. Qu'est-ce que Signal Forms (expérimental) et en quoi diffèrent-ils des Reactive Forms ?
`🔴 Avancé` · Sujet : **Angular 21**

**Réponse :** Signal Forms modélisent le formulaire comme un arbre de Signals : la valeur, la validité et l'état « touched » sont des Signals dérivés, les validateurs s'écrivent dans un schéma déclaratif, et le rendu se met à jour de façon granulaire sans `valueChanges`. L'objectif est d'unifier formulaires et Signals et de supprimer la dépendance RxJS pour les cas simples.

### 50. Comment internationaliser (i18n) une application Angular ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Deux approches : `@angular/localize` (attributs `i18n`, extraction en XLIFF, un build par locale, très performant), ou une librairie runtime comme `ngx-translate`/`transloco` (changement de langue sans rechargement, fichiers JSON). Les pipes `date`, `number` et `currency` respectent la `LOCALE_ID` fournie.

### 51. Comment migrer une application NgModule vers des composants standalone et des Signals ?
`🔴 Avancé` · Sujet : **Angular**

**Réponse :** Par étapes avec les schematics officiels : `ng g @angular/core:standalone` (3 étapes : convertir les déclarations, supprimer les modules inutiles, basculer le bootstrap), puis `control-flow`, `inject`, `signal-input-migration` et `output-migration`. Migrer feature par feature, garder les tests verts, et introduire `OnPush` avant d'envisager le zoneless.

### 52. Qu'est-ce qu'Angular et comment est structurée une application moderne (v17-21) ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Un framework TypeScript complet (routing, formulaires, HTTP, DI, tests, CLI). Une application moderne est composée de composants standalone, d'un `app.config.ts` avec des `provide*` fonctionnels, de `app.routes.ts` avec lazy loading, de services injectables, de Signals pour l'état, et du build esbuild/Vite via `@angular/build`. Les NgModules ne sont plus nécessaires.

### 53. Quel est le rôle de la CLI Angular et quelles commandes clés ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** `ng new`, `ng generate component|service|directive|pipe`, `ng serve` (dev server Vite, HMR), `ng build` (esbuild, budgets), `ng test` (Karma historique, Vitest/Jest via `@angular/build:unit-test`), `ng lint`, `ng update` (migrations automatiques de version), `ng add` (schematics d'intégration). Les schematics personnalisés standardisent la structure d'une équipe.

### 54. Différence entre composant, directive et pipe ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** Composant : directive avec template, unité d'UI. Directive d'attribut : modifie le comportement/l'apparence d'un élément (`[appHighlight]`) ; directive structurelle : modifie le DOM (`*ngIf` historique, remplacée par `@if`). Pipe : transforme une valeur dans le template (`| date`, `| async`, pipes purs mis en cache). Tous sont des classes décorées et standalone par défaut.

### 55. Comment fonctionne la communication parent-enfant avec les Signals (`input`, `output`, `model`) ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** `name = input.required<string>()` déclare une entrée typée lue comme un signal ; `changed = output<string>()` émet vers le parent (`(changed)="..."`) ; `value = model<number>()` crée un two-way binding `[(value)]`. Ils remplacent `@Input`/`@Output`, s'intègrent aux `computed`/`effect` et supportent les transformations (`input(0, { transform: numberAttribute })`).

### 56. Qu'est-ce que le template syntax : interpolation, bindings, événements, référence de template ?
`🟢 Débutant` · Sujet : **Angular**

**Réponse :** `{{ expr }}` interpolation, `[prop]="expr"` property binding, `(event)="handler($event)"`, `[(ngModel)]` two-way, `#ref` référence locale, `@if/@for/@switch` contrôle de flux, `@let` (v18.1) pour déclarer une variable locale dans le template. Les expressions doivent rester simples et pures (pas d'appels coûteux : utiliser `computed`).

### 57. Comment fonctionne le `@for` et pourquoi `track` est-il obligatoire ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `@for (item of items(); track item.id) { ... } @empty { ... }` : `track` identifie chaque élément pour que le DOM soit réutilisé plutôt que recréé lors des changements (performance, état des composants conservé). Utiliser un identifiant stable, `$index` uniquement pour les listes statiques. Variables contextuelles : `$index`, `$first`, `$last`, `$count`.

### 58. Différence entre `computed`, `effect` et `linkedSignal`, et quand utiliser chacun ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `computed` : valeur dérivée pure, mise en cache, recalculée paresseusement (à privilégier). `effect` : effet de bord réagissant aux signaux lus (log, synchronisation localStorage, appel impératif), sans écrire dans d'autres signaux par défaut. `linkedSignal` : signal écrivable dont la valeur par défaut se réinitialise quand une source change (sélection dans une liste rechargée).

### 59. Qu'est-ce que `httpResource` et `resource` et comment les utiliser pour charger des données ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `resource({ params: () => ({ id: this.id() }), loader: ({ params, abortSignal }) => fetch(...) })` recharge automatiquement quand ses paramètres signal changent, expose `value()`, `isLoading()`, `error()`, `reload()`, et annule les requêtes obsolètes. `httpResource` (v19.2+) fait de même au-dessus de `HttpClient` (`httpResource(() => `/api/users/${id()}`)`). Ils remplacent les `switchMap` + `subscribe` pour les lectures.

### 60. Comment structurer l'état d'une application Angular : services à Signals, NgRx SignalStore, ou NgRx Store ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Petite/moyenne application : services `providedIn: 'root'` exposant des signaux (`private _items = signal([])`, `items = this._items.asReadonly()`, `computed`). Besoins structurés : NgRx SignalStore (`signalStore`, `withState`, `withComputed`, `withMethods`, `rxMethod`) léger et typé. Grande équipe avec traçabilité : NgRx Store (actions, reducers, effects, devtools) au prix du boilerplate. Éviter les états dupliqués entre composants.

### 61. Qu'est-ce que NgRx SignalStore et ses concepts (`withState`, `withMethods`, `rxMethod`, `patchState`) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un store fonctionnel basé sur les signaux : `signalStore({ providedIn: 'root' }, withState({ users: [], loading: false }), withComputed(...), withMethods((store, api = inject(Api)) => ({ load: rxMethod<void>(pipe(switchMap(() => api.list()), tap(u => patchState(store, { users: u }))) })), withHooks({ onInit }))`. Extensible par des « features » personnalisées (`withEntities`, `withDevtools`). Bien moins verbeux que le Store classique.

### 62. Comment fonctionne l'injection de dépendances dans les templates et les routes (`inject`, `providers` de route, `EnvironmentInjector`) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `inject()` fonctionne dans les constructeurs, initialisateurs de champs, guards/resolvers fonctionnels et `runInInjectionContext`. Une route peut déclarer `providers: [...]` créant un `EnvironmentInjector` enfant : le service vit tant que la route est active (état par fonctionnalité). Les composants fournissent des services locaux via `providers` (une instance par composant).

### 63. Qu'est-ce que le `DestroyRef` et `takeUntilDestroyed` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `DestroyRef` (v16) permet d'enregistrer un callback à la destruction du composant/service/injecteur (`inject(DestroyRef).onDestroy(...)`) sans implémenter `OnDestroy`. `takeUntilDestroyed()` (dans un contexte d'injection, ou avec `destroyRef` en paramètre) complète automatiquement un observable à la destruction : la façon idiomatique de gérer les abonnements.

### 64. Comment fonctionnent les Route Guards, Resolvers et les `withComponentInputBinding` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Guards fonctionnels (`canActivate: [() => inject(Auth).isLoggedIn() || inject(Router).createUrlTree(['/login'])]`), `canMatch` pour choisir des routes selon le rôle ou lazy-loader conditionnellement, `canDeactivate` pour les formulaires non sauvegardés, resolvers pour précharger (attention à l'attente perçue : préférer `resource` dans le composant + skeleton). `withComponentInputBinding()` mappe params, query params et data de route directement sur les `input()` du composant.

### 65. Comment implémenter des routes imbriquées, des `outlet` nommés et des layouts ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Routes `children` rendues dans le `<router-outlet>` du composant parent (layout avec header/sidebar), routes sans composant (`path: 'admin', canActivate, children`) pour grouper, `outlet: 'modal'` pour des outlets secondaires (dialogues avec URL), `loadChildren` pour lazy-loader une branche entière, et `title` de route (statique ou `TitleStrategy`) pour l'onglet du navigateur.

### 66. Comment fonctionnent les stratégies de preloading et `PreloadAllModules` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Après le chargement initial, le router peut précharger les routes lazy en arrière-plan : `withPreloading(PreloadAllModules)` ou une stratégie personnalisée (par `data: { preload: true }`, selon la connexion réseau ou le rôle). Cela accélère les navigations suivantes sans alourdir le premier chargement. Combinable avec `@defer (on idle)` pour les composants lourds.

### 67. Quels déclencheurs et blocs offre `@defer` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Déclencheurs : `on idle` (défaut), `on viewport`, `on interaction`, `on hover`, `on timer(2s)`, `on immediate`, `when condition()`, et `prefetch on ...` pour charger le code avant de l'afficher. Blocs : `@placeholder (minimum 500ms)`, `@loading (after 100ms; minimum 1s)`, `@error`. Le contenu différé est extrait en chunk séparé automatiquement.

### 68. Comment gérer les formulaires réactifs typés (Typed Forms) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Depuis v14, `FormGroup`/`FormControl` sont typés : `new FormGroup({ email: new FormControl('', { nonNullable: true, validators: [Validators.required, Validators.email] }) })`, `FormBuilder.nonNullable`, `form.getRawValue()` typé, `form.controls.email.value` sans `any`. Les groupes dynamiques utilisent `FormRecord`. Cela détecte les erreurs de nom de champ à la compilation.

### 69. Comment implémenter des validateurs asynchrones et des validations croisées ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Validateur asynchrone : fonction retournant `Observable<ValidationErrors | null>` (vérifier la disponibilité d'un e-mail), avec `debounceTime`/`switchMap` et `updateOn: 'blur'` pour limiter les appels ; état `pending`. Validation croisée : validateur sur le `FormGroup` comparant deux champs (mot de passe/confirmation), erreur affichée au niveau groupe. Toujours revalider côté serveur.

### 70. Comment créer un composant de formulaire personnalisé avec `ControlValueAccessor` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Implémenter `writeValue`, `registerOnChange`, `registerOnTouched`, `setDisabledState`, et déclarer `providers: [{ provide: NG_VALUE_ACCESSOR, useExisting: forwardRef(() => MyInput), multi: true }]`. Le composant devient utilisable avec `formControlName`/`ngModel`. Pour accéder aussi aux validateurs, injecter `NgControl` (`@Self() @Optional()`) et s'y attacher comme accessor.

### 71. Comment fonctionne `HttpClient` avec les Signals et les intercepteurs fonctionnels ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `provideHttpClient(withInterceptors([authInterceptor, loggingInterceptor]), withFetch())` ; un intercepteur est une fonction `(req, next) => next(req.clone({ setHeaders }))` pouvant utiliser `inject()`. Consommer avec `toSignal(http.get(...))`, `httpResource`, ou `rxResource`. `withFetch` active l'API Fetch (nécessaire pour SSR et le streaming).

### 72. Comment gérer l'authentification (jeton, refresh, 401) côté Angular ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un intercepteur ajoute `Authorization` ; sur 401, rafraîchir le jeton (une seule fois, file d'attente des requêtes concurrentes) puis rejouer, sinon rediriger vers le login. Préférer un flux OIDC code + PKCE (angular-oauth2-oidc, oidc-client-ts) avec jetons en mémoire, ou un BFF avec cookies `HttpOnly` et `withXsrfConfiguration`. Guards `canMatch` pour les routes protégées ; ne jamais faire confiance au front pour l'autorisation.

### 73. Comment gérer les erreurs globalement (`ErrorHandler`, intercepteur, notifications) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Un `ErrorHandler` personnalisé (`provide: ErrorHandler`) capture les erreurs non gérées (log, Sentry) ; un intercepteur HTTP convertit les erreurs réseau/API en messages utilisateur (toast) et gère les cas transverses (401, 503, maintenance) ; les composants gèrent localement ce qui a du sens (retry, formulaire). Éviter de masquer les erreurs et journaliser avec contexte (route, utilisateur anonymisé).

### 74. Comment fonctionne la détection de changement et que change le mode zoneless ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Historiquement, Zone.js intercepte les événements asynchrones et déclenche une vérification de tout l'arbre (ou des composants OnPush marqués). En zoneless (stable v20+ via `provideZonelessChangeDetection()`), Angular ne se déclenche que sur les signaux modifiés, les événements de template, `markForCheck`/`AsyncPipe`, et les `input` changés : moins de travail, bundle plus léger, mais le code doit passer par les signaux ou notifier explicitement.

### 75. Comment migrer une application vers OnPush + Signals + zoneless ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Étapes : activer OnPush sur tous les composants (schematic), remplacer `@Input/@Output` par `input()/output()` (migration `ng generate @angular/core:signal-inputs`), convertir les états locaux en `signal`, les observables affichés en `toSignal` ou `AsyncPipe`, remplacer `setTimeout` de contournement par des signaux, tester avec `provideZonelessChangeDetection` puis retirer Zone.js des polyfills.

### 76. Qu'est-ce que `afterRender`, `afterNextRender` et `afterRenderEffect` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Des hooks (v17+) exécutés après le rendu du DOM, côté navigateur uniquement (ignorés en SSR) : pour mesurer des éléments, initialiser une bibliothèque tierce (charts, cartes) ou manipuler le DOM. `afterNextRender` s'exécute une fois ; `afterRenderEffect` (v19) réagit aux signaux avec des phases (`earlyRead`, `write`, `mixedReadWrite`, `read`) pour éviter le layout thrashing.

### 77. Comment intégrer une bibliothèque JavaScript tierce (chart, carte) dans un composant ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Injecter `ElementRef` ou utiliser `viewChild`, initialiser dans `afterNextRender` (compatibilité SSR), détruire dans `DestroyRef.onDestroy`, réagir aux données via `effect`/`afterRenderEffect`, encapsuler dans un composant dédié avec `input()`s, lazy-loader la bibliothèque (`import()` dynamique ou `@defer`), et sortir des mises à jour fréquentes de la zone (`NgZone.runOutsideAngular`) si Zone.js est encore actif.

### 78. Comment fonctionnent `viewChild`, `contentChildren` en version signal ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `chart = viewChild.required<ElementRef>('chart')`, `items = contentChildren(ItemComponent)` retournent des signaux mis à jour par Angular : disponibles dans `computed`/`effect`, sans `static` ni `ngAfterViewInit`. `viewChild` renvoie `undefined` avant le rendu ; `required` lève une erreur s'il manque. Ils remplacent `@ViewChild`/`@ContentChildren`.

### 79. Comment créer une directive réutilisable avec `hostDirectives` (composition de directives) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `@Component({ hostDirectives: [{ directive: CdkMenuTrigger, inputs: ['cdkMenuTriggerFor: menu'] }, DisabledDirective] })` applique automatiquement des directives à l'hôte du composant et expose leurs inputs/outputs sous un alias. Cela compose des comportements (tooltip, tracking, a11y) sans héritage et sans que l'utilisateur du composant ait à les ajouter.

### 80. Comment fonctionne le `host` metadata et pourquoi le préférer à `@HostBinding`/`@HostListener` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `host: { '[class.active]': 'active()', '(click)': 'toggle()', 'role': 'button' }` déclare bindings et écouteurs sur l'élément hôte dans le décorateur ; le style guide moderne le recommande car plus lisible, groupé, et compatible avec les signaux. Les décorateurs restent supportés.

### 81. Comment fonctionnent les styles : encapsulation, `:host`, `::ng-deep`, et les variables CSS ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Par défaut `ViewEncapsulation.Emulated` ajoute des attributs pour isoler les styles du composant ; `:host` cible l'élément hôte, `:host-context` le contexte parent. `::ng-deep` perce l'encapsulation (déprécié, à éviter). Pour thématiser des enfants, utiliser des variables CSS (`--primary`), des `@Input` de classes, ou les APIs de thème (Angular Material `mat.theme`). `ShadowDom` utilise le vrai Shadow DOM.

### 82. Comment utiliser Angular Material et le CDK efficacement ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Material fournit les composants Material Design 3 (v18+ avec thème via `@use '@angular/material' as mat; mat.theme(...)`) ; le CDK fournit des briques sans style : overlay (menus, dialogues), drag-drop, virtual scroll, a11y (focus trap, live announcer), tables, layout. Importer par composant (standalone), personnaliser via tokens de thème plutôt que `::ng-deep`, et tester avec les component harnesses.

### 83. Qu'est-ce que les component harnesses (`@angular/cdk/testing`) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Une API de test qui interagit avec un composant comme un utilisateur via une abstraction stable (`MatButtonHarness.with({ text: 'Save' })`, `harness.click()`), indépendante du DOM interne de la bibliothèque et utilisable en tests unitaires et E2E (Protractor historique, Playwright/WebdriverIO). On écrit des harnesses pour ses propres composants partagés.

### 84. Comment tester avec Vitest/Jest et l'API `TestBed` moderne (`inputs`, `bindings`) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `ng test` supporte Vitest via le builder `@angular/build:unit-test` (v20+, plus rapide que Karma). `TestBed.configureTestingModule({ imports: [MyComponent], providers })`, `TestBed.createComponent(MyComponent, { bindings: [inputBinding('name', signal('x'))] })` (v20), `fixture.componentRef.setInput`, `await fixture.whenStable()`, `provideHttpClientTesting` + `HttpTestingController`, `TestBed.inject`. Préférer les tests via le DOM (Testing Library for Angular) aux tests d'implémentation.

### 85. Comment écrire des tests E2E d'une application Angular (Playwright, Cypress) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Playwright ou Cypress lancés contre `ng serve` ou un build servi ; sélecteurs par rôle/texte/`data-testid` plutôt que par classes ; mocks réseau (`page.route`, `cy.intercept`) pour les cas d'erreur ; authentification par état sauvegardé ; tests des parcours critiques uniquement (la pyramide reste unitaire/intégration en majorité) ; exécution parallèle en CI avec traces et vidéos sur échec.

### 86. Comment configurer le SSR moderne (`@angular/ssr`) et le rendu par route (`RenderMode`) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `ng add @angular/ssr` crée `server.ts` (Express ou `AngularNodeAppEngine`) et `app.config.server.ts`. Le `serverRoutes` (v19+) définit par route `RenderMode.Prerender` (statique au build, avec `getPrerenderParams`), `Server` (SSR à chaque requête) ou `Client` (CSR). L'hydration (`provideClientHydration(withEventReplay(), withIncrementalHydration())`) réutilise le DOM serveur.

### 87. Quels sont les pièges du SSR Angular (APIs navigateur, HTTP, état) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Accès à `window`/`document`/`localStorage` côté serveur (protéger par `isPlatformBrowser`, `afterNextRender`, ou abstractions), appels HTTP relatifs sans base URL, double appel HTTP (le `TransferState` via `withHttpTransferCacheOptions` évite de refaire côté client), fuites d'état entre requêtes (services `providedIn: 'root'` sont par requête côté serveur, mais attention aux variables globales), et temps de rendu serveur à surveiller.

### 88. Comment fonctionnent les budgets de build et l'analyse du bundle ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `angular.json` définit `budgets` (`initial`, `anyComponentStyle`) faisant échouer le build au-delà d'un seuil. Analyser avec `ng build --stats-json` + `esbuild-visualizer`/`source-map-explorer` pour repérer les grosses dépendances (moment → date-fns/Temporal, lodash complet → imports ciblés, icônes), et vérifier que le lazy loading découpe bien les routes.

### 89. Comment gérer les images, polices et assets pour la performance ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `NgOptimizedImage` (`ngSrc`, `priority` pour le LCP, `fill`, loaders CDN, `sizes`), formats modernes (AVIF/WebP), préchargement des polices critiques (`<link rel="preload">`, `font-display: swap`), dossier `public/` (v18+) pour les assets, hachage des noms de fichiers par le build pour le cache long, et lazy loading des composants lourds avec `@defer (on viewport)`.

### 90. Comment implémenter le virtual scrolling et les listes performantes ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `cdk-virtual-scroll-viewport` avec `*cdkVirtualFor` (ou `@for` dans les versions récentes) ne rend que les éléments visibles (`itemSize` fixe, ou `autosize` expérimental). Combiner avec `track` stables, OnPush, `computed` pour le filtrage, et pagination côté serveur au-delà de quelques milliers d'éléments.

### 91. Comment gérer l'accessibilité dans Angular (a11y) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** HTML sémantique, `aria-*` bindings (`[attr.aria-expanded]`), gestion du focus lors des navigations (`FocusMonitor`, `cdkTrapFocus` dans les dialogues, focus sur le titre après changement de route), `LiveAnnouncer` pour les messages dynamiques, contraste et tailles cibles, tests avec `@angular-eslint/template/accessibility` rules et axe (Playwright/Storybook). Angular Material et le CDK intègrent la plupart des patterns ARIA.

### 92. Qu'est-ce que l'internationalisation runtime (Transloco, ngx-translate) vs `@angular/localize` ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `@angular/localize` : traductions extraites (`ng extract-i18n`), compilées par locale au build (un bundle par langue, très performant, changement de langue par rechargement). Transloco/ngx-translate : fichiers JSON chargés à l'exécution, changement de langue à chaud, plus souple pour les traductions gérées par le métier. Choisir selon la nécessité du changement dynamique.

### 93. Comment créer et publier une bibliothèque Angular (ng-packagr, monorepo Nx) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `ng generate library` produit un projet compilé par ng-packagr au format Angular Package Format (ESM, `d.ts`, partial compilation) ; `public-api.ts` définit l'API publique ; dépendances en `peerDependencies` ; versionner en SemVer ; tests et Storybook. Dans un monorepo Nx, les bibliothèques sont importées par alias TypeScript et les builds affectés sont calculés par graphe.

### 94. Qu'est-ce que le pattern « smart/dumb components » et comment l'appliquer avec les signaux ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Composants « smart » (containers) : injectent les services/stores, orchestrent les données et les actions. Composants « dumb » (presentational) : `input()`/`output()` uniquement, OnPush, réutilisables et faciles à tester/Storybook. Avec les signaux, les containers passent des signaux ou valeurs aux inputs, et les enfants émettent des événements ; l'état reste centralisé.

### 95. Comment organiser un projet Angular de grande taille (feature-based, barrels, ESLint boundaries) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Dossiers par fonctionnalité (`features/orders/` avec routes, composants, store, api), `shared/` (UI pure), `core/` (services transverses, intercepteurs), routes lazy par feature, règles ESLint (`@nx/enforce-module-boundaries` ou `eslint-plugin-boundaries`) interdisant les imports entre features, barrels avec parcimonie (cycles, tree shaking), et ADR pour les conventions d'état.

### 96. Comment fonctionne le style guide Angular 2025 et quelles conventions ont changé ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Fichiers sans suffixe de type obligatoire (`user-profile.ts` au lieu de `.component.ts`, `ng g` v20+), classes sans suffixe (`UserProfile`), `protected` pour les membres utilisés uniquement par le template, `readonly` sur les `input()`/`viewChild()`, `host` au lieu des décorateurs, `inject()` au lieu de l'injection constructeur, standalone implicite, préférence pour `class`/`style` bindings plutôt que `ngClass`/`ngStyle`.

### 97. Comment gérer les mises à jour de version Angular (`ng update`) et les breaking changes ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Mettre à jour une version majeure à la fois (`ng update @angular/core@20 @angular/cli@20`), lire le guide update.angular.dev, appliquer les migrations automatiques (control flow, standalone, signal inputs), mettre à jour Material/CDK/NgRx en parallèle, vérifier TypeScript et Node compatibles, exécuter tests et build avec budgets, et traiter les dépréciations avant la version suivante. Rester au plus N-1 des LTS.

### 98. Comment fonctionne l'hydration avec event replay et incremental hydration ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `withEventReplay()` enregistre les interactions utilisateur survenues avant l'hydration et les rejoue ensuite (aucun clic perdu). `withIncrementalHydration()` (v19) n'hydrate les blocs `@defer (hydrate on viewport|interaction|idle)` que lorsque nécessaire, en gardant le HTML serveur visible : moins de JavaScript exécuté au chargement, TTI amélioré sur les grandes pages.

### 99. Comment sécuriser une application Angular (XSS, sanitization, CSP, Trusted Types) ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Angular échappe les interpolations et sanitize `innerHTML`, `href`, `style` ; `bypassSecurityTrust*` est un point d'audit (uniquement sur du contenu contrôlé). Déployer une CSP stricte (nonce pour les styles inline générés via `ngCspNonce`), Trusted Types supportés, éviter `eval`/templates dynamiques, `withXsrfConfiguration` pour le CSRF, dépendances auditées (`npm audit`), et ne jamais stocker de secrets dans le bundle (`environment.ts` est public).

### 100. Comment implémenter le mode hors ligne et une PWA avec Angular ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** `ng add @angular/pwa` ajoute le service worker Angular (`ngsw-config.json` : stratégies de cache des assets et des appels API `performance`/`freshness`), le manifeste et les icônes. `SwUpdate` détecte les nouvelles versions et propose le rechargement ; `SwPush` gère les notifications push. Tester en build de production (le SW est inactif en `ng serve`), et gérer la synchronisation différée des écritures (IndexedDB + Background Sync).

### 101. Quelles sont les nouveautés d'Angular 20 et 21 à connaître ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** v20 : signaux stables (`effect`, `linkedSignal`, `toSignal`), zoneless en developer preview → stable, `httpResource`, style guide révisé, Vitest expérimental, `TestBed` bindings, support TypeScript 5.8, Chrome DevTools intégration. v21 (nov. 2025) : zoneless par défaut pour les nouveaux projets, Vitest par défaut, Signal Forms expérimentaux, Angular Aria (composants headless accessibles), MCP server pour les assistants IA, et `Angular CLI` sur esbuild uniquement. Vérifier le blog officiel pour les détails.

### 102. Quels opérateurs RxJS restent indispensables dans une application Angular à base de Signals ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** `switchMap`/`exhaustMap`/`concatMap`/`mergeMap` pour orchestrer les appels (annulation, sérialisation), `debounceTime`+`distinctUntilChanged` pour les saisies, `catchError` avec valeur de repli, `retry` avec backoff, `takeUntilDestroyed`, `combineLatest`/`forkJoin` pour agréger, `shareReplay(1)` pour partager. Les signaux gèrent l'état synchrone ; RxJS reste pour les flux asynchrones et temporels.

### 103. Différence entre `switchMap`, `mergeMap`, `concatMap`, `exhaustMap` avec des exemples Angular ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** `switchMap` : annule le précédent (recherche en saisie, chargement selon route). `mergeMap` : tout en parallèle (uploads indépendants). `concatMap` : en file, ordonné (sauvegardes successives). `exhaustMap` : ignore les nouveaux tant que l'actuel n'est pas fini (bouton de soumission anti double-clic). Le mauvais choix crée des courses ou des doublons.

### 104. Comment gérer le partage d'un observable HTTP (`shareReplay`) sans fuite ni requêtes multiples ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** Un `HttpClient.get` est froid : chaque abonné relance la requête (`| async` deux fois = deux appels). `shareReplay({ bufferSize: 1, refCount: true })` partage et rejoue la dernière valeur, se désabonnant quand plus personne n'écoute. Alternative moderne : `toSignal(obs)` dans un service (un seul abonnement) ou `httpResource`.

### 105. Comment implémenter un retry avec backoff et une gestion d'erreurs propre dans un service Angular ?
`🟠 Intermédiaire` · Sujet : **RxJS**

**Réponse :** `retry({ count: 3, delay: (err, n) => timer(Math.min(1000 * 2 ** n, 10000)) })` uniquement pour les erreurs transitoires (5xx, réseau), puis `catchError` transformant l'erreur en objet métier (`throwError(() => new ApiError(...))`) ou en valeur de repli, et un intercepteur pour les cas globaux. Ne pas réessayer les erreurs 4xx ni les requêtes non idempotentes.

### 106. Comment fonctionne l'égalité des signaux (`equal`) et pourquoi les objets ne déclenchent-ils pas toujours de mise à jour ?
`🟠 Intermédiaire` · Sujet : **Signals**

**Réponse :** `signal(obj)` compare par `Object.is` : `set` avec le même objet muté ne notifie pas ; il faut créer un nouvel objet (`update(s => ({ ...s, x }))`) ou fournir `equal: (a, b) => deepEqual(a, b)` pour éviter des recalculs inutiles sur des valeurs structurellement égales. Les tableaux suivent la même règle : `update(arr => [...arr, item])`.

### 107. Qu'est-ce que `untracked` et quand l'utiliser dans `effect` et `computed` ?
`🟠 Intermédiaire` · Sujet : **Signals**

**Réponse :** `untracked(() => sig())` lit un signal sans créer de dépendance : dans un `effect`, pour lire des valeurs contextuelles sans que leur changement ne relance l'effet, ou pour appeler des fonctions qui lisent des signaux en interne. Dans un `computed`, il limite les recalculs. À utiliser avec parcimonie : une dépendance manquante est aussi une source de bugs.

### 108. Pourquoi ne faut-il pas écrire dans un signal depuis un `effect`, et quelles alternatives ?
`🟠 Intermédiaire` · Sujet : **Signals**

**Réponse :** Écrire dans un signal pendant un effet crée des chaînes de mise à jour difficiles à suivre et des risques de boucles ; Angular le permettait avec `allowSignalWrites` (devenu défaut en v19) mais recommande `computed` pour les valeurs dérivées, `linkedSignal` pour un état réinitialisable, et les événements/`resource` pour les chargements. Les effets restent pour la synchronisation vers l'extérieur (DOM, stockage, logs).

### 109. Comment convertir entre observables et signaux dans les deux sens et quels pièges ?
`🟠 Intermédiaire` · Sujet : **Signals**

**Réponse :** `toSignal(obs, { initialValue })` s'abonne dans un contexte d'injection et se désabonne à la destruction ; sans `initialValue` le type inclut `undefined` (ou `requireSync: true` pour un `BehaviorSubject`). `toObservable(sig)` émet lors des changements (via un `effect`, donc asynchrone, pas immédiat). Ne pas appeler `toSignal` dans une méthode appelée plusieurs fois (fuite d'abonnements).

### 110. Comment concevoir un service d'état avec Signals (pattern store léger) ?
`🟠 Intermédiaire` · Sujet : **Signals**

**Réponse :** État privé `#state = signal<State>(initial)`, sélecteurs `computed` exposés en lecture seule, méthodes de mise à jour immuables via `update`, effets de chargement via `resource` ou `rxMethod`-like, et `readonly` sur les signaux exposés. Découper par feature, fournir au niveau de la route (`providers`) pour un cycle de vie lié à la fonctionnalité, et tester le service sans TestBed quand possible.

### 111. Qu'est-ce que Signal Forms (Angular 21, expérimental) et en quoi diffèrent-ils des Reactive Forms ?
`🟠 Intermédiaire` · Sujet : **Signals**

**Réponse :** Un nouveau modèle de formulaires où le modèle est un signal (`form(model, schema)`) et où validation, état et désactivation sont dérivés de façon réactive via un schéma déclaratif (`required`, `email`, règles dépendantes) ; la directive `[field]` lie les champs. Objectif : typage complet, moins de boilerplate que `FormGroup` et intégration native aux signaux. À suivre jusqu'à la stabilisation.

### 112. Comment implémenter des micro-frontends avec Angular (Module Federation, Native Federation, web components) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Native Federation (esbuild) ou Module Federation (webpack) chargent à l'exécution des remotes Angular exposés, partageant Angular/RxJS en singleton avec des versions compatibles ; ou encapsuler chaque application en web component (`@angular/elements`) pour une indépendance totale (au prix de duplication). Coûts : versions alignées, routing distribué, design system partagé, et observabilité. À réserver aux organisations multi-équipes.

### 113. Comment intégrer un design system et Storybook dans un projet Angular ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Bibliothèque de composants UI (workspace ou monorepo Nx) avec tokens de design (CSS variables), composants standalone documentés dans Storybook (`@storybook/angular`, stories avec `argTypes`, contrôles, tests d'interaction, tests visuels via Chromatic ou Playwright), a11y addon, et versionnement SemVer. Les applications consomment le package ; les changements passent par revue de design et de code.

### 114. Comment gérer la configuration runtime (URL d'API par environnement) sans rebuild ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** `environment.ts` est compilé : pour un « build once, deploy anywhere », charger un `config.json` servi par le déploiement (ConfigMap Kubernetes monté dans l'image Nginx) via `provideAppInitializer` + `HttpClient`, ou injecter les valeurs dans `index.html` (`window.__env`) à l'exécution. Ne jamais y placer de secrets ; valider le schéma au démarrage.

### 115. Comment déployer une SPA Angular en production (Nginx, Docker, S3/CloudFront, cache) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Build de production avec hachage des fichiers ; `index.html` en `no-cache` et les assets hachés en `immutable, max-age=1y` ; fallback vers `index.html` pour le routing (Nginx `try_files`, CloudFront error page 403/404 → 200 `index.html`, ou mieux une fonction de réécriture) ; compression Brotli/gzip ; headers de sécurité (CSP, HSTS) ; image Docker Nginx non-root ; SSR via un serveur Node ou des fonctions edge si SEO requis.

### 116. Comment intégrer Angular avec un backend Spring Boot (proxy dev, CORS, CSRF, cookies) ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** En développement, `proxy.conf.json` route `/api` vers Spring pour éviter CORS. En production, servir sous le même domaine (reverse proxy) pour utiliser les cookies `SameSite` et éviter CORS, ou configurer CORS côté Spring avec origines explicites. CSRF : cookie `XSRF-TOKEN` lu par `withXsrfConfiguration`. Typage partagé via OpenAPI (génération de clients TypeScript avec openapi-generator ou `ng-openapi-gen`).

### 117. Comment générer un client TypeScript typé depuis OpenAPI et l'intégrer proprement ?
`🟠 Intermédiaire` · Sujet : **Architecture**

**Réponse :** Générer (`openapi-generator-cli generate -g typescript-angular` ou `ng-openapi-gen`, `orval`, `openapi-typescript` + fetch) dans un package ou dossier non édité manuellement, en CI à partir de la spécification du backend (contract-first), envelopper les services générés dans des façades applicatives (mapping vers le modèle front, gestion d'erreurs), et faire échouer la CI si le contrat change de façon incompatible.

### 118. Comment diagnostiquer et corriger des re-rendus excessifs ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Angular DevTools (profiler des cycles de détection, composants les plus coûteux), `ChangeDetectionStrategy.OnPush` généralisé, pipes purs ou `computed` au lieu de méthodes appelées dans le template, `track` stable dans `@for`, éviter les objets/fonctions créés dans le template, découper les gros composants, `@defer` pour les zones non visibles, et zoneless pour éliminer les déclenchements inutiles (timers, événements globaux).

### 119. Comment gérer les gros tableaux de données (data grids) efficacement ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Pagination et tri côté serveur, virtual scroll (CDK) ou grilles spécialisées (AG Grid, Angular Material table avec `MatTableDataSource` pour les petits volumes), colonnes `track`, cellules en OnPush, formatage précalculé (`computed`) plutôt que pipes lourds par cellule, `@defer` pour les panneaux annexes, et Web Workers pour les calculs (agrégations, exports) afin de garder l'UI fluide.

### 120. Comment utiliser les Web Workers et le streaming dans Angular ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** `ng generate web-worker` crée un worker (bundle séparé) ; communication par `postMessage`, encapsulée dans un service exposant un observable ou un signal ; pour les calculs lourds, le parsing de fichiers, la cryptographie. Streaming HTTP : `fetch` avec `ReadableStream` ou `HttpClient` avec `observe: 'events'` et `reportProgress`, ou SSE (`EventSource`) pour les flux serveur (progression, chat IA) affichés progressivement via signaux.

### 121. Comment mesurer les Core Web Vitals d'une application Angular et les améliorer ?
`🟠 Intermédiaire` · Sujet : **Performance**

**Réponse :** Lighthouse/PageSpeed et le CrUX pour les données terrain, `web-vitals` envoyé à l'analytics. LCP : SSR/prerender, `NgOptimizedImage` avec `priority`, polices préchargées, `@defer` pour le hors-écran. INP : OnPush/zoneless, gestionnaires d'événements légers, éviter le travail synchrone long. CLS : dimensions d'images, skeletons de tailles fixes, polices avec `size-adjust`. Budgets en CI pour éviter les régressions.

### 122. Comment tester un composant à Signals et `input.required` avec TestBed ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** `TestBed.createComponent(Comp, { bindings: [inputBinding('user', signal(user))] })` (v20) ou `fixture.componentRef.setInput('user', user)` ; `fixture.detectChanges()` (ou `await fixture.whenStable()` en zoneless) ; assertions sur le DOM (`fixture.nativeElement.querySelector`, Testing Library `screen.getByRole`) ; tester les `output` via `subscribe` ou `outputBinding` ; `TestBed.tick()`/`flushEffects` pour les effets.

### 123. Comment tester un service utilisant `resource`/`httpResource` et `HttpClient` ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** `provideHttpClient()` + `provideHttpClientTesting()`, `TestBed.inject(HttpTestingController)`, déclencher le chargement (créer le service dans un contexte d'injection, `TestBed.runInInjectionContext`), `expectOne(url).flush(data)`, puis `await fixture.whenStable()`/`TestBed.tick()` et vérifier `resource.value()`/`isLoading()`. `httpTesting.verify()` en `afterEach` détecte les requêtes inattendues.

### 124. Comment tester le routing, les guards et les resolvers ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** `provideRouter(routes)` dans le TestBed, `RouterTestingHarness` (v15+) : `harness.navigateByUrl('/orders/1', OrderComponent)` retourne l'instance du composant activé et permet d'asserter le DOM ; guards fonctionnels testés via `TestBed.runInInjectionContext(() => guard(route, state))` avec des services mockés ; vérifier les redirections avec `TestBed.inject(Router).url` et les `UrlTree`.

### 125. Comment organiser mocks, fixtures et données de test en Angular (factories, MSW, harnesses) ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Factories typées (`buildUser({ role: 'admin' })`) plutôt que des JSON figés, MSW pour mocker l'API de façon réaliste en tests et en Storybook, component harnesses pour les composants complexes, `provide*` de test (`provideMockStore`, `provideHttpClientTesting`), et un dossier `testing/` par feature exportant ces utilitaires. Éviter les `spyOn` en cascade : préférer des fakes simples.

### 126. Comment mettre en place les tests visuels et de contrat côté front ?
`🟠 Intermédiaire` · Sujet : **Tests**

**Réponse :** Visuels : Storybook + Chromatic ou Playwright `toHaveScreenshot` sur les composants du design system, seuils de tolérance, exécution en CI sur PR. Contrat : Pact (consumer-driven) où le front définit ses attentes vérifiées contre le backend Spring, ou validation du client généré contre la spécification OpenAPI courante ; les deux détectent les ruptures avant le déploiement.

### 127. Comment gérer les rôles et permissions dans l'UI (directives, guards, menus) sans dupliquer la logique serveur ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Un service d'autorisation (signaux dérivés des claims du jeton ou d'un endpoint `/me/permissions`), une directive structurelle `*appHasPermission="'orders:write'"` (ou `@if (auth.can('orders:write'))`), guards `canMatch` pour les routes, et menus filtrés par `computed`. L'UI ne fait que masquer : chaque action reste vérifiée côté API. Centraliser les noms de permissions dans des constantes partagées avec le backend.

### 128. Comment sécuriser l'utilisation de contenu HTML riche (éditeur, Markdown) dans Angular ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** Angular sanitize automatiquement `[innerHTML]` (suppression des scripts, événements) ; pour du HTML de confiance produit par un éditeur, sanitizer côté serveur (OWASP Java HTML Sanitizer, DOMPurify côté client) avec une allow-list stricte avant `bypassSecurityTrustHtml` ; CSP interdisant les scripts inline ; liens externes avec `rel="noopener noreferrer"` ; et tests XSS automatisés sur les champs riches.

### 129. Comment gérer les dépendances npm et la supply chain d'un projet Angular ?
`🟠 Intermédiaire` · Sujet : **Sécurité**

**Réponse :** `package-lock.json` versionné et `npm ci` en CI, `npm audit`/Dependabot/Renovate pour les mises à jour groupées, vérification des licences, `overrides` pour forcer des correctifs transitifs, limiter les dépendances (préférer le CDK et les APIs natives), scanner en CI (Snyk, OSV), et surveiller les incidents npm (typosquatting, packages compromis) : privilégier les packages maintenus et signés (provenance npm).

### 130. Comment rendre un composant personnalisé (menu, combobox, dialogue) accessible avec le CDK ?
`🟠 Intermédiaire` · Sujet : **Accessibilité**

**Réponse :** Utiliser les primitives CDK : `cdkMenu`/`cdkMenuTrigger` (navigation clavier, ARIA), `cdkListbox`, `cdkTrapFocus` et `Dialog` du CDK (focus initial, restauration, `aria-modal`), `FocusKeyManager` pour les listes personnalisées, `LiveAnnouncer`, et Angular Aria (v21) pour des composants headless conformes aux patterns WAI-ARIA. Tester au clavier et avec un lecteur d'écran, plus axe en CI.

### 131. Comment gérer les annonces, le focus et les titres lors des navigations de route ?
`🟠 Intermédiaire` · Sujet : **Accessibilité**

**Réponse :** `TitleStrategy` pour un titre de page significatif, focus déplacé sur le `h1` ou le conteneur principal après navigation (`Router.events` `NavigationEnd` + `afterNextRender`), `LiveAnnouncer` pour les messages de statut (chargement, erreurs), skip links, `withInMemoryScrolling({ scrollPositionRestoration: 'enabled' })`, et respect de `prefers-reduced-motion` pour les animations de transition.

### 132. Comment gérer les animations en Angular moderne (`@angular/animations` déprécié, `animate.enter/leave`, View Transitions) ?
`🟠 Intermédiaire` · Sujet : **Animations**

**Réponse :** Le module `@angular/animations` est déprécié (v20.2) au profit du CSS natif : `animate.enter="fade-in"` et `animate.leave="fade-out"` (v20.2+) appliquent des classes CSS lors de l'entrée/sortie, ou Web Animations API ; transitions de route via `withViewTransitions()` (View Transitions API du navigateur, `view-transition-name`). Respecter `prefers-reduced-motion` et garder les animations légères.

### 133. Comment configurer ESLint pour Angular (`angular-eslint`) et quelles règles adopter ?
`🟠 Intermédiaire` · Sujet : **Outils**

**Réponse :** `ng add angular-eslint` installe les règles TypeScript et de templates : nommage des sélecteurs, interdiction de `any`, `prefer-standalone`, `prefer-signals` (v20+), règles d'accessibilité de templates, ordre des membres, pas de `subscribe` imbriqués (`rxjs-x`), boundaries entre features. Exécuter en pre-commit (lint-staged) et en CI ; corriger progressivement avec des règles en `warn` puis `error`.

### 134. Comment utiliser Nx ou les workspaces Angular pour un monorepo, et quels bénéfices ?
`🟠 Intermédiaire` · Sujet : **Outils**

**Réponse :** Nx ajoute au workspace Angular un graphe de projets, le cache local/distant des builds et tests, l'exécution uniquement des projets affectés (`nx affected`), les générateurs et règles de frontières entre bibliothèques (`type:feature`, `scope:orders`), et l'intégration de Vite/Vitest/Playwright. Les workspaces Angular natifs (`projects` multiples) suffisent pour quelques applications et bibliothèques sans cache distribué.

### 135. Comment intégrer les assistants IA au développement Angular (Angular MCP, `llms.txt`, bonnes pratiques) ?
`🟠 Intermédiaire` · Sujet : **Outils**

**Réponse :** Angular fournit un serveur MCP (`ng mcp`, v20.1+) donnant à l'assistant la documentation à jour, les bonnes pratiques (`get_best_practices`), la liste des projets et les migrations, et un `llms.txt`/`llms-full.txt` sur angular.dev. Compléter par un fichier d'instructions projet (conventions, structure, versions) et relire les propositions : les modèles produisent encore souvent du code NgModule/`@Input` obsolète.

### 136. Comment fonctionne le HMR et le dev server Vite dans Angular et que faire en cas de comportement étrange ?
`🟠 Intermédiaire` · Sujet : **Outils**

**Réponse :** Le builder `@angular/build:dev-server` utilise Vite : HMR des styles et templates (v19+ pour les templates de composants) sans rechargement complet, conservation de l'état. En cas d'état incohérent (services singleton conservés, effets dupliqués), recharger la page ; désactiver avec `--no-hmr` pour isoler un bug ; vider `.angular/cache` si le build est corrompu.

### 137. Comment implémenter une gestion de dialogues/modales réutilisable et typée ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** CDK `Dialog` (ou `MatDialog`) via un service `DialogService.open<TResult>(Component, { data })` retournant un observable/promise typé ; composants de dialogue standalone recevant `DIALOG_DATA` via `inject`, résultats via `DialogRef.close(result)` ; gestion du focus et de l'échappement fournies ; routes avec outlet nommé si l'URL doit refléter le dialogue ; et tests via harness `MatDialogHarness`.

### 138. Comment gérer les notifications (toasts) et le feedback utilisateur de façon centralisée ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Un `NotificationService` (signal d'une liste de messages) rendu par un composant global (aria-live, empilement, auto-dismiss configurable), alimenté par l'intercepteur HTTP pour les erreurs, par les stores après les actions, et par les guards ; variantes succès/erreur/info accessibles (contraste, icône + texte), et pas de toast pour les erreurs de formulaire (inline). Snackbar Material en option.

### 139. Comment implémenter un système de permissions de fonctionnalités (feature flags) côté Angular ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Un service chargé à l'initialisation (ou en flux temps réel via SSE/SDK LaunchDarkly/Unleash) exposant `isEnabled(flag)` en signal, une directive `*appFeature="'new-checkout'"`, des guards `canMatch` pour router vers l'ancienne ou la nouvelle route, et `@defer (when flag())` pour ne pas charger le code inactif. Les flags ne remplacent pas l'autorisation et doivent être nettoyés une fois généralisés.

### 140. Comment gérer l'état des formulaires longs : brouillons, sauvegarde automatique, navigation ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Sauvegarde automatique avec `valueChanges` + `debounceTime` + `distinctUntilChanged` (ou effet sur un signal de formulaire) vers l'API ou le stockage local, indicateur d'état (enregistré/en cours/erreur), `canDeactivate` pour avertir avant de quitter avec des changements non sauvegardés, restauration du brouillon au retour, versionnement pour éviter d'écraser des modifications concurrentes (ETag/`If-Match`).

### 141. Comment implémenter un système de recherche avec filtres synchronisés à l'URL ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Les filtres vivent dans les query params (source de vérité partageable, retour arrière fonctionnel) : `withComponentInputBinding` les injecte en `input()`, un `computed` construit la requête, `resource` charge les résultats, et les changements de filtre naviguent (`router.navigate([], { queryParams, queryParamsHandling: 'merge' })`) avec `debounce` pour la saisie. Valider/normaliser les params (zod) et gérer les états vide/erreur/chargement.

### 142. Comment gérer les fichiers (upload avec progression, drag & drop, prévisualisation) ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** `<input type="file">` ou CDK drag-drop, validation côté client (type, taille) puis serveur, `HttpClient.post(url, formData, { reportProgress: true, observe: 'events' })` pour la progression (`HttpEventType.UploadProgress`), signal de progression par fichier, annulation via désabonnement, upload direct vers S3 par URL présignée pour les gros fichiers, prévisualisation via `URL.createObjectURL` (révoquée à la destruction).

### 143. Comment implémenter le temps réel (WebSocket, SSE, STOMP) dans Angular proprement ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Un service encapsulant la connexion (`webSocket` de RxJS ou `@stomp/rx-stomp`, `EventSource` pour SSE) avec reconnexion exponentielle, heartbeat, file des messages sortants pendant la déconnexion, conversion en signaux pour l'affichage, et fermeture à la destruction. Authentifier via cookie/jeton au handshake, gérer le multi-onglets (BroadcastChannel) et tester avec un serveur mock.

### 144. Comment gérer les thèmes (clair/sombre) et les préférences utilisateur ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Variables CSS définies par un attribut sur `html` (`data-theme`) ou `color-scheme` avec `prefers-color-scheme` par défaut, un service à signal persistant le choix (localStorage, ou profil serveur), `light-dark()` CSS, thèmes Material via `mat.theme` avec `color-scheme`, et transitions douces. Éviter le flash au chargement (script inline dans `index.html` appliquant le thème avant le rendu, compatible SSR).

### 145. Comment gérer les erreurs de chunk loading (`ChunkLoadError`) après un déploiement ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Après un déploiement, les anciens chunks hachés disparaissent et les navigations lazy échouent. Solutions : intercepter `ChunkLoadError` dans le `ErrorHandler` ou `router.events` (`NavigationError`) et recharger la page une fois, `SwUpdate` pour détecter les nouvelles versions et proposer le rechargement, conserver les anciens assets quelques heures côté serveur/CDN, et versionner `index.html` en `no-cache`.

### 146. Comment implémenter un « undo/redo » ou une historisation d'état avec Signals ?
`🟠 Intermédiaire` · Sujet : **Patterns**

**Réponse :** Un store où chaque modification pousse l'état précédent (immuable) dans une pile `past` et vide `future` ; `undo` déplace vers `future`, `redo` l'inverse ; signaux `canUndo`/`canRedo` en `computed` ; limiter la taille de l'historique ; regrouper les modifications rapides (debounce) ; et sérialiser si persistance nécessaire. L'immuabilité des mises à jour de signaux rend ce pattern trivial.

### 147. Comment migrer une application AngularJS (1.x) ou Angular ancien (v8-12) vers Angular moderne ?
`🟠 Intermédiaire` · Sujet : **Migration**

**Réponse :** AngularJS : hybride via `@angular/upgrade` (ngUpgrade) composant par composant, ou réécriture par feature derrière un routage partagé (strangler). Angular ancien : mises à jour majeures successives avec `ng update` (chaque étape testée), puis migrations automatiques (standalone, control flow, `inject`, signal inputs), suppression des dépendances abandonnées, adoption progressive des signaux et de OnPush. Prioriser une suite de tests E2E avant de commencer.

### 148. Comment migrer de NgRx Store classique vers SignalStore progressivement ?
`🟠 Intermédiaire` · Sujet : **Migration**

**Réponse :** Cohabiter : conserver le Store global pour les états transverses et créer des SignalStores par feature pour les nouveaux écrans ; exposer les sélecteurs du Store en signaux (`store.selectSignal`) pour uniformiser la consommation ; remplacer les effets par `rxMethod` ou `resource` ; migrer feature par feature avec tests ; supprimer les actions/reducers devenus inutiles. Éviter la double source de vérité pendant la transition.

### 149. Comment fonctionne le rendu côté serveur avec des données préchargées et le `TransferState` en détail ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Pendant le SSR, les réponses `HttpClient` (GET/HEAD par défaut, configurable via `withHttpTransferCacheOptions`) sont sérialisées dans le HTML ; au démarrage client, `HttpClient` les sert depuis ce cache au lieu de refaire l'appel, puis le cache est vidé. Pour des données non HTTP, `TransferState` avec `makeStateKey` permet d'injecter manuellement. Attention à la taille du HTML et aux données sensibles (ne pas transférer ce que l'utilisateur ne doit pas voir).

### 150. Comment gérer le multi-application et le partage de code entre une app publique SSR et un back-office SPA ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Workspace ou monorepo avec bibliothèques partagées (modèle, client API généré, UI), deux applications aux configurations distinctes (SSR + prerender pour le site public ; SPA CSR pour le back-office), pipelines séparés, design system commun, et règles de frontières pour que le back-office n'importe pas de code SSR-spécifique et inversement.

### 151. Quelles sont les erreurs de conception les plus fréquentes dans les projets Angular et comment les éviter ?
`🟠 Intermédiaire` · Sujet : **Angular**

**Réponse :** Logique métier dans les composants (déplacer dans des services/stores), `subscribe` sans désabonnement, `any` généralisé, composants géants, `providedIn: 'root'` pour de l'état de feature, `ngOnChanges` complexes au lieu de `computed`, `setTimeout` pour « attendre » le rendu, `::ng-deep` partout, appels HTTP dans les constructeurs, absence de OnPush, et tests qui vérifient l'implémentation. Des revues avec checklist et des règles ESLint préviennent la plupart.
