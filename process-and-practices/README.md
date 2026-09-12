# 📋 Engineering Process & Practices

> Feature flags, trunk-based development, canary releases

**50 questions**

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

### 4. Qu'est-ce que la méthode Agile et quelles sont ses valeurs fondamentales ?
`🟢 Débutant` · Sujet : **Agile**

**Réponse :** Un ensemble d'approches itératives et incrémentales issues du Manifeste Agile (2001) : les individus et interactions plutôt que les processus, un logiciel qui fonctionne plutôt qu'une documentation exhaustive, la collaboration avec le client plutôt que la négociation contractuelle, l'adaptation au changement plutôt que le suivi d'un plan. Scrum, Kanban et XP en sont des déclinaisons.

### 5. Quels sont les rôles, événements et artefacts de Scrum ?
`🟢 Débutant` · Sujet : **Agile**

**Réponse :** Rôles : Product Owner (valeur, backlog), Scrum Master (processus, obstacles), Développeurs. Événements : Sprint (1-4 semaines), Sprint Planning, Daily, Sprint Review, Rétrospective. Artefacts : Product Backlog, Sprint Backlog, Incrément, avec leurs engagements (objectif produit, objectif de sprint, Definition of Done).

### 6. Différence entre Scrum et Kanban ?
`🟢 Débutant` · Sujet : **Agile**

**Réponse :** Scrum fonctionne par itérations fixes avec engagement sur un objectif de sprint et rôles définis. Kanban est un flux continu : visualiser le travail, limiter le travail en cours (WIP), mesurer le lead time et améliorer en continu, sans sprints ni rôles imposés. Beaucoup d'équipes combinent les deux (Scrumban).

### 7. Qu'est-ce qu'une user story et le format INVEST ?
`🟢 Débutant` · Sujet : **Agile**

**Réponse :** Une description courte d'un besoin du point de vue utilisateur (« En tant que…, je veux…, afin de… ») avec critères d'acceptation. INVEST : Indépendante, Négociable, Valuable (apporte de la valeur), Estimable, Small (petite), Testable. Une story trop grosse est un epic à découper.

### 8. Qu'est-ce que la Definition of Done et la Definition of Ready ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** DoD : liste de critères qu'un incrément doit remplir pour être terminé (code revu, tests passés, documentation, déployé en recette, critères de sécurité). DoR : conditions pour qu'une story entre en sprint (critères d'acceptation clairs, dépendances identifiées, estimée). Elles rendent explicite la qualité attendue et évitent les « presque fini ».

### 9. Comment estimer (story points, Planning Poker, #NoEstimates) ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Les story points mesurent l'effort relatif (complexité, incertitude, volume) sur une échelle de Fibonacci, estimés collectivement par Planning Poker pour faire émerger les divergences de compréhension. La vélocité sert à la prévision, jamais à comparer des équipes. L'approche #NoEstimates découpe en petits éléments homogènes et prévoit par le débit.

### 10. Qu'est-ce qu'une rétrospective efficace ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Un temps régulier où l'équipe examine sa manière de travailler et décide d'actions concrètes, dans un cadre de sécurité psychologique (directive première : chacun a fait de son mieux). Varier les formats (Start/Stop/Continue, 4L, Sailboat), limiter à 1-3 actions suivies au sprint suivant, et traiter les problèmes systémiques plutôt que les personnes.

### 11. Comment gérer la dette technique dans un backlog produit ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** La rendre visible (tickets étiquetés, cartographie), l'expliquer en termes d'impact métier (lenteur des livraisons, incidents), réserver une capacité régulière (15-20 %) ou la traiter au fil des stories touchant la zone concernée (règle du boy scout), et prioriser par risque et coût d'intérêt. La dette n'est pas mauvaise en soi si elle est choisie et remboursée.

### 12. Qu'est-ce qu'un MVP et comment éviter ses dérives ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Le produit minimal permettant d'apprendre du marché avec le moins d'effort possible, pas une version bâclée du produit final. Dérives : accumulation de « minimum » sans « viable », prototype passé en production sans consolidation, absence de mesure de l'apprentissage. Définir l'hypothèse à valider et les métriques avant de construire.

### 13. Qu'est-ce que SAFe, LeSS et le scaling agile, et quelles critiques ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Des cadres pour coordonner plusieurs équipes : SAFe (Agile Release Trains, PI Planning, rôles nombreux), LeSS (Scrum étendu avec un backlog commun), Spotify model (squads, tribes). Critiques : lourdeur, retour de la planification à long terme, perte d'autonomie. Préférer réduire les dépendances entre équipes (Team Topologies) plutôt que d'ajouter de la coordination.

### 14. Qu'est-ce que Team Topologies ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Un modèle d'organisation en quatre types d'équipes : stream-aligned (alignée sur un flux de valeur), platform (fournit des services internes en self-service), enabling (aide temporairement à monter en compétence), complicated-subsystem (expertise pointue). Et trois modes d'interaction : collaboration, X-as-a-service, facilitation. Objectif : limiter la charge cognitive.

### 15. Qu'est-ce que le Continuous Delivery vs le Continuous Deployment ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Continuous Delivery : chaque changement validé par le pipeline est déployable en production à tout moment, le déploiement restant une décision (souvent un clic). Continuous Deployment : chaque changement validé est déployé automatiquement en production sans intervention. Les deux exigent tests automatisés fiables, feature flags et observabilité.

### 16. Que sont les métriques DORA ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Quatre indicateurs de performance de livraison : fréquence de déploiement, lead time des changements (commit → production), taux d'échec des changements, temps de restauration après incident (plus récemment : temps de restauration et fiabilité). Les équipes « élite » déploient à la demande avec un lead time inférieur à un jour. Ils mesurent le flux, pas la productivité individuelle.

### 17. Qu'est-ce que le framework SPACE et pourquoi ne pas mesurer les lignes de code ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** SPACE mesure la productivité des développeurs sur cinq dimensions : Satisfaction, Performance, Activité, Communication/collaboration, Efficience/flux. Les lignes de code, commits ou story points individuels sont des métriques manipulables qui poussent aux mauvais comportements (loi de Goodhart). Combiner métriques système et perception des développeurs.

### 18. Qu'est-ce qu'une stratégie de branches et laquelle choisir ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Trunk-based (branches courtes < 1-2 jours, intégration continue, flags) favorise le flux et est corrélé à la performance DORA. GitFlow (develop, release, hotfix) convient aux produits versionnés livrés périodiquement. GitHub Flow (branche → PR → main déployé) est un compromis courant. Le choix dépend du rythme de livraison et de la maturité des tests.

### 19. Qu'est-ce que le versioning sémantique et le Conventional Commits ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** SemVer `MAJOR.MINOR.PATCH` : incompatibilité / fonctionnalité compatible / correctif. Conventional Commits normalise les messages (`feat:`, `fix:`, `feat!:` pour breaking) pour générer automatiquement changelog et version (semantic-release, release-please). Utile pour les librairies et APIs ; les applications déployées en continu utilisent souvent des versions calendaires ou le SHA.

### 20. Comment gérer les migrations de base de données sans interruption ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Pattern expand/contract : ajouter la nouvelle colonne/table (compatible avec l'ancien code), déployer le code qui écrit dans les deux, migrer les données, basculer les lectures, puis supprimer l'ancien schéma dans une version ultérieure. Migrations versionnées (Flyway/Liquibase), jamais de changement destructif dans la même version que le code qui en dépend.

### 21. Qu'est-ce qu'un déploiement canary et comment décider de la promotion ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Exposer la nouvelle version à une petite fraction du trafic (1-5 %), comparer ses métriques (erreurs, latence, métriques métier) avec la version stable, puis augmenter progressivement ou revenir en arrière automatiquement. Argo Rollouts/Flagger automatisent l'analyse. Nécessite des métriques par version et du trafic suffisant pour être significatif.

### 22. Différence entre blue/green, canary et rolling update ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Rolling : remplacement progressif des instances, simple, versions mixtes temporairement. Blue/green : deux environnements complets, bascule instantanée du trafic, rollback immédiat, coût doublé. Canary : fraction de trafic sur la nouvelle version avec analyse, minimise le rayon d'impact. Tous exigent la compatibilité ascendante des APIs et schémas.

### 23. Comment gérer la dette des feature flags ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Les flags temporaires doivent avoir un propriétaire et une date d'expiration ; les supprimer dès que la fonctionnalité est généralisée (ticket créé à la création du flag). Outils : linters détectant les flags anciens, rapports de la plateforme (LaunchDarkly, Unleash). Distinguer les flags permanents (kill switch, entitlements) des flags de release.

### 24. Qu'est-ce qu'un kill switch et pourquoi en prévoir ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Un flag opérationnel permettant de désactiver instantanément une fonctionnalité ou une intégration (fournisseur externe, calcul coûteux) en production sans déploiement. Il réduit le temps de restauration lors d'un incident. Il doit être testé régulièrement et le comportement dégradé défini (message, fallback).

### 25. Qu'est-ce que le testing in production et comment le faire de façon sûre ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Vérifier le comportement réel après déploiement : déploiements canary, flags par utilisateur interne (dogfooding), shadow traffic (dupliquer les requêtes vers la nouvelle version sans effet), synthetic monitoring, et chaos engineering. Conditions : observabilité, isolation des effets de bord, rollback rapide, données de test identifiées.

### 26. Comment organiser un environnement de recette/staging utile ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Le plus proche possible de la production (même infrastructure via IaC, mêmes versions, données anonymisées représentatives), environnements éphémères par PR pour tester isolément, et ne pas en faire un goulot d'étranglement (file d'attente de validation). Beaucoup d'équipes remplacent un staging partagé par flags + canary en production.

### 27. Comment mener une revue de code efficace ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Petites PR (< 400 lignes), description claire (quoi, pourquoi, comment tester), relecture rapide (< 1 jour) pour ne pas bloquer, commentaires sur le code et non la personne, distinguer bloquant / suggestion / nit, automatiser le style (linters, formatage) pour se concentrer sur la conception, la sécurité et la lisibilité. Approuver n'est pas cautionner chaque ligne mais juger l'ensemble acceptable.

### 28. Qu'est-ce que le pair programming et le mob programming ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Pair : deux développeurs sur une tâche (driver/navigator, rotation), améliore la qualité, diffuse la connaissance, réduit le besoin de revue. Mob/ensemble : toute l'équipe sur un même écran, utile pour les sujets complexes ou l'intégration d'un nouveau. Coût apparent plus élevé mais moins de reprise et de silos ; à doser selon les tâches.

### 29. Qu'est-ce qu'un ADR (Architecture Decision Record) ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Un document court versionné avec le code décrivant une décision d'architecture : contexte, options envisagées, décision, conséquences. Immuable une fois accepté (une nouvelle décision le remplace). Il conserve le « pourquoi » pour les futurs membres et évite de rejouer les mêmes débats.

### 30. Qu'est-ce que la documentation as code et le modèle Diátaxis ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Écrire la documentation en Markdown/AsciiDoc versionnée avec le code, revue en PR et publiée automatiquement (MkDocs, Docusaurus, Antora). Diátaxis structure la documentation en quatre types selon le besoin : tutoriels (apprendre), guides pratiques (résoudre), référence (consulter), explications (comprendre). Mélanger ces types nuit à la lisibilité.

### 31. Qu'est-ce que l'Inner Source ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Appliquer les pratiques open source à l'intérieur de l'entreprise : dépôts visibles par tous, contributions d'autres équipes via PR, mainteneurs identifiés, documentation de contribution (CONTRIBUTING.md). Il réduit les dépendances bloquantes entre équipes et la duplication de composants.

### 32. Comment gérer les conventions de code dans une équipe ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Les automatiser plutôt que les discuter : formatteur imposé (Prettier, Spotless/google-java-format), linters (ESLint, Checkstyle, Error Prone), EditorConfig, hooks pre-commit ou vérification en CI, et un guide court pour ce qui ne s'automatise pas (nommage, structure). Le formatage automatique élimine une catégorie entière de commentaires de revue.

### 33. Qu'est-ce qu'un postmortem sans blâme (blameless) ?
`🟠 Intermédiaire` · Sujet : **Incident**

**Réponse :** Une analyse d'incident centrée sur les causes systémiques (processus, outillage, information manquante) plutôt que sur les erreurs individuelles, partant du principe que les personnes ont agi rationnellement avec les informations disponibles. Contenu : chronologie, impact, causes contributives, ce qui a bien fonctionné, actions correctives avec propriétaires et dates.

### 34. Comment organiser la gestion d'incident (rôles, communication) ?
`🟠 Intermédiaire` · Sujet : **Incident**

**Réponse :** Rôles clairs : commandant d'incident (coordonne, décide), responsable communication (mises à jour régulières aux parties prenantes), responsables techniques (investiguent). Canal dédié, chronologie tenue en temps réel, niveaux de sévérité définissant l'urgence et l'escalade, page de statut. Résoudre d'abord (mitiger), analyser ensuite.

### 35. Qu'est-ce que l'astreinte (on-call) et comment la rendre soutenable ?
`🟠 Intermédiaire` · Sujet : **Incident**

**Réponse :** Une rotation où un développeur est joignable pour les incidents hors heures ouvrées. Soutenabilité : rotations courtes et équitables, compensation, alertes actionnables uniquement (revue régulière du bruit), runbooks à jour, escalade claire, et temps dédié après une astreinte chargée pour corriger les causes. Une charge d'astreinte élevée est un signal de dette de fiabilité.

### 36. Qu'est-ce qu'un runbook et que doit-il contenir ?
`🟠 Intermédiaire` · Sujet : **Incident**

**Réponse :** Une procédure opérationnelle pour une alerte ou une tâche : symptômes, vérifications à faire (requêtes, dashboards), actions de mitigation étape par étape, critères d'escalade, contacts. Versionné, lié directement depuis l'alerte, testé et mis à jour après chaque incident. Les étapes répétées doivent être automatisées à terme.

### 37. Qu'est-ce que le chaos engineering ?
`🟠 Intermédiaire` · Sujet : **Incident**

**Réponse :** Injecter volontairement des défaillances (arrêt de Pods, latence réseau, panne de dépendance) en environnement contrôlé pour vérifier la résilience du système et des procédures. Démarche : définir l'état stable, formuler une hypothèse, expérimenter avec rayon d'impact limité, mesurer, corriger. Outils : Chaos Monkey, Litmus, Gremlin, AWS FIS.

### 38. Qu'est-ce que le Software Supply Chain et quelles pratiques la sécurisent ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** L'ensemble des dépendances, outils et pipelines produisant le logiciel. Pratiques : verrouillage des versions (lockfiles), scan des vulnérabilités (Dependabot, Renovate, Trivy), SBOM, signature des artefacts et images (Sigstore/cosign), niveaux SLSA, pipelines à privilèges minimaux, revue des nouvelles dépendances. Les attaques récentes (xz, npm) visent cette chaîne.

### 39. Comment gérer les mises à jour de dépendances de façon durable ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Automatiser les PR de mise à jour (Renovate, Dependabot) regroupées et planifiées, avec CI complète pour valider, fusion automatique des correctifs mineurs quand les tests sont fiables, revue manuelle des majeures, et suivi des versions en fin de vie (Spring Boot, Angular, Node). Les petites mises à jour fréquentes sont moins risquées qu'une grosse migration annuelle.

### 40. Comment travailler efficacement avec le Product Owner et le métier ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Impliquer les développeurs tôt dans l'affinage (backlog refinement) pour challenger le besoin et proposer des alternatives, exprimer les contraintes techniques en impact métier, utiliser des exemples concrets (Example Mapping, BDD) pour lever les ambiguïtés, et livrer souvent pour obtenir du feedback réel plutôt que des spécifications exhaustives.

### 41. Qu'est-ce que le BDD et l'Example Mapping ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Behavior-Driven Development : formuler le comportement attendu en exemples concrets (Given/When/Then) partagés entre métier, développeurs et testeurs, éventuellement automatisés (Cucumber). Example Mapping : atelier court où l'on décompose une story en règles, exemples et questions avec des cartes de couleur, pour découvrir les incompréhensions avant de coder.

### 42. Comment gérer les interruptions et le travail non planifié ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Mesurer leur part (souvent 20-40 %), réserver une capacité explicite, désigner un « goalkeeper » tournant qui absorbe les demandes pour protéger le reste de l'équipe, canaliser les demandes dans le backlog plutôt qu'en messages directs, et traiter les causes récurrentes (bugs, questions de support) par des corrections ou de la documentation.

### 43. Qu'est-ce que le WIP limit et pourquoi limiter le travail en cours ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Un plafond sur le nombre d'éléments simultanément en cours par colonne ou par personne. Le multitâche augmente le lead time (loi de Little), le changement de contexte et les éléments bloqués oubliés. Limiter le WIP force à terminer avant de commencer, à s'entraider sur les blocages et rend visibles les goulots d'étranglement.

### 44. Quels sont les signes d'une équipe en difficulté et comment y répondre ?
`🟠 Intermédiaire` · Sujet : **Agile**

**Réponse :** Sprints jamais terminés, rétrospectives sans actions, bugs récurrents, dépendances externes bloquantes, turnover, daily transformé en rapport au manager, absence de tests. Réponses : réduire la taille des lots, stabiliser la qualité (arrêter d'ajouter des fonctionnalités le temps de corriger), clarifier les priorités, protéger le temps de focus, et rendre les problèmes visibles au management.

### 45. Qu'est-ce que la Developer Experience (DevEx) et la Platform Engineering ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** DevEx : la qualité perçue du travail quotidien des développeurs (temps de feedback, charge cognitive, état de flow). Platform Engineering : une équipe plateforme fournit en self-service (portail type Backstage, templates, pipelines, environnements) ce dont les équipes ont besoin pour livrer sans expertise infra profonde. Objectif : réduire la friction mesurable (temps d'onboarding, de build, de déploiement).

### 46. Comment onboarder efficacement un nouveau développeur ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** README à jour avec démarrage en une commande (Docker Compose, devcontainer), buddy désigné, première contribution réelle dès la première semaine, documentation d'architecture (C4, ADR), accès préparés avant l'arrivée, points réguliers, et recueil de son feedback pour améliorer l'onboarding suivant. Le temps jusqu'au premier déploiement en production est une bonne métrique.

### 47. Qu'est-ce que la « boy scout rule » et le refactoring opportuniste ?
`🟠 Intermédiaire` · Sujet : **Code Quality**

**Réponse :** Laisser le code un peu plus propre qu'on l'a trouvé : petits refactorings sur la zone touchée par une story (renommage, extraction, suppression de code mort), couverts par les tests existants, dans des commits séparés pour faciliter la revue. Il évite l'accumulation sans exiger de gros projets de refonte, mais ne remplace pas les décisions structurelles.

### 48. Comment communiquer une échéance à risque ou un retard ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Tôt, avec des faits (avancement, obstacles, incertitudes) et des options (réduire le périmètre, décaler, ajouter du soutien) plutôt qu'un simple constat, en évitant les heures supplémentaires chroniques comme solution. La transparence continue (démos, burn-up, indicateurs) évite l'effet de surprise. Un retard annoncé tard est un problème de confiance, pas seulement de planning.

### 49. Qu'est-ce que le Working Agreement d'une équipe ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Un ensemble de règles explicites décidées par l'équipe : horaires de présence commune, délai de revue de PR, gestion du daily, DoD, canal et étiquette de communication, règles de télétravail, rotation d'astreinte. Il est révisé en rétrospective et sert de référence lors des tensions.

### 50. Comment mesurer et améliorer le lead time ?
`🟠 Intermédiaire` · Sujet : **Delivery**

**Réponse :** Cartographier le flux (value stream mapping) du besoin à la production, mesurer le temps passé dans chaque étape et surtout en attente (revue, validation, déploiement), puis attaquer la plus grande file d'attente : automatiser les tests, réduire la taille des PR, supprimer les validations manuelles à faible valeur, déployer plus souvent. Le lead time d'une équipe est dominé par les attentes, pas par le codage.
