# 📋 Engineering Process & Practices

> Feature flags, trunk-based development, canary releases

**3 questions**

---

### 1. Qu'est-ce qu'un feature flag et quels problèmes résout-il en développement ?
`🟠 Intermédiaire` · Sujet : **Feature Flags**

**Réponse :** Un mécanisme permettant d'activer/désactiver une fonctionnalité en production sans redéployer le code, facilitant le déploiement progressif (canary), les tests A/B, le découplage entre déploiement et mise en visibilité d'une feature, et un rollback instantané en cas de problème.

### 2. Qu'est-ce que le trunk-based development et en quoi diffère-t-il du GitFlow ?
`🟢 Débutant` · Sujet : **Trunk-based development**

**Réponse :** Une pratique où les développeurs intègrent fréquemment leurs changements (souvent quotidiennement) directement sur une branche principale unique via des commits courts, contrairement à GitFlow qui utilise des branches de fonctionnalités longues, de release et de développement séparées.

### 3. Différence entre un "release flag" et un "experiment flag" (A/B test) ?
`🔴 Avancé` · Sujet : **Feature Flags**

**Réponse :** Release flag est temporaire pour un déploiement progressif puis supprimé. Experiment flag reste actif pour comparer deux variantes avec collecte de métriques.
