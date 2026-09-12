# 🤖 AI/LLM for Developers

> MCP, RAG, AI-assisted coding best practices

**4 questions**

---

### 1. Qu'est-ce que le RAG (Retrieval-Augmented Generation) et pourquoi l'utiliser avec un LLM ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Une technique qui récupère des documents pertinents (via une recherche vectorielle sur des embeddings) et les injecte dans le contexte du prompt avant de générer une réponse, permettant au LLM de répondre avec des informations à jour ou spécifiques à un domaine sans avoir à le ré-entraîner.

### 2. Qu'est-ce que le Model Context Protocol (MCP) ?
`🟠 Intermédiaire` · Sujet : **MCP**

**Réponse :** Un protocole ouvert standardisant la façon dont les applications LLM se connectent à des sources de données et outils externes, permettant une interaction uniforme plutôt que des intégrations propriétaires ad-hoc.

### 3. Bonnes pratiques pour utiliser un assistant de code IA comme Copilot ou Claude Code ?
`🟢 Débutant` · Sujet : **AI-assisted coding**

**Réponse :** Fournir un contexte clair, toujours relire le code généré, utiliser l'IA pour les tâches répétitives plutôt que la conception critique, vérifier les dépendances/API suggérées qui peuvent être obsolètes.

### 4. Différence entre un "MCP server" et un "MCP client" ?
`🟢 Débutant` · Sujet : **MCP**

**Réponse :** Le serveur expose des ressources/outils/prompts consommables. Le client (intégré à une app LLM) se connecte pour découvrir et invoquer ces capacités.
