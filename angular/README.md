# 🅰️ Angular

> Signals, standalone components, control flow, SSR, Zoneless, RxJS integration

**51 questions**

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
