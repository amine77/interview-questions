# ▲ Next.js

> SSR, SSG, ISR, API routes, middleware, hydration

**6 questions**

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
