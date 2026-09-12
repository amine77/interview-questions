# 🅰️ Angular

> Signals, standalone components, control flow, SSR, Zoneless, RxJS integration

**19 questions**

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
