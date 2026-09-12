# ⚛️ React

> Hooks, Virtual DOM, reconciliation, state management

**6 questions**

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
