# 🖥️ Frontend Advanced

> PWA, Web Components, Core Web Vitals, a11y, micro-frontends, state mgmt

**8 questions**

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
