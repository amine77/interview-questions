# 🤖 AI/LLM for Developers

> MCP, RAG, AI-assisted coding best practices

**50 questions**

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

### 5. Qu'est-ce qu'un LLM et comment fonctionne-t-il à haut niveau ?
`🟢 Débutant` · Sujet : **RAG / LLM**

**Réponse :** Un Large Language Model est un réseau de neurones (architecture Transformer) entraîné à prédire le prochain token sur d'immenses corpus, puis affiné (instruction tuning, RLHF) pour suivre des consignes. Il génère du texte token par token en fonction du contexte fourni ; il ne « sait » que ce qui est dans ses poids ou dans le prompt.

### 6. Qu'est-ce qu'un token et pourquoi compte-t-il ?
`🟢 Débutant` · Sujet : **RAG / LLM**

**Réponse :** L'unité de texte traitée par le modèle (mot, sous-mot, ponctuation ; ~4 caractères en anglais, plus en français). Il détermine la taille de la fenêtre de contexte, le coût (facturation par tokens d'entrée/sortie), la latence, et explique certaines faiblesses (comptage de lettres, arithmétique).

### 7. Qu'est-ce que la fenêtre de contexte et ses implications ?
`🟢 Débutant` · Sujet : **RAG / LLM**

**Réponse :** La quantité maximale de tokens (prompt + réponse) que le modèle traite en une fois (de 8k à plus d'un million selon les modèles). Un contexte plus grand permet d'inclure plus de documents, mais coûte plus cher, peut dégrader l'attention (« lost in the middle ») et n'est pas une mémoire persistante.

### 8. Que sont la température et les autres paramètres de sampling ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** `temperature` contrôle l'aléa : 0 rend la sortie quasi déterministe (extraction, code), plus élevé favorise la créativité. `top_p` (nucleus) limite aux tokens les plus probables cumulés, `max_tokens` borne la réponse, `stop` définit des séquences d'arrêt. Ne pas combiner temperature et top_p agressifs.

### 9. Qu'est-ce qu'une hallucination et comment la limiter ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Une réponse plausible mais fausse (fait inventé, API inexistante, citation fabriquée). Limites : fournir les sources dans le contexte (RAG), demander des citations et l'aveu d'ignorance, température basse, sorties structurées validées, vérification par un second passage ou des outils, et ne jamais utiliser un LLM comme source de vérité factuelle non vérifiée.

### 10. Qu'est-ce que le prompt engineering et quelles techniques de base ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Formuler l'entrée pour obtenir la sortie voulue : rôle et contexte clairs, instructions explicites, format de sortie spécifié, exemples (few-shot), délimiteurs pour séparer données et instructions, décomposition en étapes, et itération avec évaluation. Un prompt système fixe les règles ; le prompt utilisateur porte la demande.

### 11. Qu'est-ce que le chain-of-thought et les modèles de raisonnement ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Demander au modèle de raisonner étape par étape avant de conclure améliore les tâches logiques. Les modèles de raisonnement (o-series, Claude avec extended thinking, DeepSeek-R1) intègrent ce processus en interne avec un budget de tokens de réflexion, au prix d'une latence et d'un coût plus élevés ; à réserver aux problèmes complexes.

### 12. Qu'est-ce que le few-shot prompting ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Fournir dans le prompt quelques exemples entrée→sortie pour montrer le format et le style attendus, sans réentraîner le modèle. Efficace pour la classification, l'extraction et les formats spécifiques ; les exemples doivent être représentatifs et variés, et leur ordre peut influencer le résultat.

### 13. Qu'est-ce que les sorties structurées (JSON mode, structured outputs, function calling) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Contraindre le modèle à produire du JSON conforme à un schéma (JSON Schema) pour l'intégrer dans du code : `response_format` avec schéma, ou une définition d'outil dont les arguments sont typés. Toujours valider le résultat (Zod, Jackson) et prévoir un retry en cas d'échec de parsing.

### 14. Qu'est-ce que le function/tool calling ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Le modèle reçoit la description d'outils (nom, paramètres JSON Schema) et, au lieu de répondre en texte, retourne un appel structuré (`get_weather({city: "Paris"})`). L'application exécute la fonction, renvoie le résultat au modèle, qui poursuit. C'est la brique de base des agents et du MCP.

### 15. Qu'est-ce qu'un embedding ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Un vecteur numérique (centaines à milliers de dimensions) représentant le sens d'un texte, produit par un modèle d'embedding. Des textes sémantiquement proches ont des vecteurs proches (similarité cosinus), ce qui permet la recherche sémantique, le clustering, la déduplication et le RAG.

### 16. Qu'est-ce qu'une base vectorielle et quelles options existent ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Un stockage indexé pour la recherche de plus proches voisins sur des vecteurs (HNSW, IVF). Options : pgvector (extension PostgreSQL, souvent suffisante), Elasticsearch/OpenSearch (kNN), Qdrant, Weaviate, Milvus, Pinecone (managé), Redis. Critères : volume, filtrage par métadonnées, hybridation avec le lexical, exploitation.

### 17. Quelles sont les étapes d'un pipeline RAG ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Ingestion : charger les documents, les découper en chunks, calculer les embeddings, indexer avec métadonnées. Requête : embedder la question, récupérer les k chunks les plus proches (avec filtres), éventuellement reranker, construire le prompt avec ces extraits, générer la réponse avec citations, puis évaluer.

### 18. Comment choisir la stratégie de chunking ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Chunks de 200 à 800 tokens avec chevauchement, découpés sur des frontières sémantiques (paragraphes, titres, fonctions pour le code) plutôt que par nombre de caractères fixe ; conserver les métadonnées (titre, section, source) et éventuellement ajouter un résumé contextuel du document à chaque chunk (« contextual retrieval »). Tester plusieurs tailles sur un jeu d'évaluation.

### 19. Qu'est-ce que la recherche hybride et le reranking ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Hybride : combiner recherche vectorielle (sens) et lexicale BM25 (mots exacts, identifiants, acronymes) avec fusion des scores (RRF), plus robuste que chacune seule. Reranking : un modèle cross-encoder réordonne les 20-50 candidats en évaluant précisément la pertinence question/chunk avant de garder les 5 meilleurs.

### 20. Comment évaluer un système RAG ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Constituer un jeu de questions avec réponses de référence, puis mesurer : qualité du retrieval (recall@k, MRR), fidélité de la réponse au contexte (faithfulness), pertinence, et absence d'hallucination, via des métriques automatiques (RAGAS, LLM-as-a-judge) et une revue humaine. Évaluer à chaque changement de chunking, modèle ou prompt.

### 21. Quand préférer le fine-tuning au RAG, et inversement ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** RAG : connaissances factuelles changeantes, besoin de citations, données privées volumineuses, mise à jour sans réentraînement. Fine-tuning : adapter le style, le format, un domaine de vocabulaire, ou améliorer une tâche précise avec des exemples ; il n'ajoute pas de connaissances fiables. Souvent : prompt engineering d'abord, RAG ensuite, fine-tuning en dernier.

### 22. Qu'est-ce que la quantification et l'exécution locale de modèles (Ollama, llama.cpp) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** La quantification réduit la précision des poids (16 bits → 4-8 bits) pour diminuer mémoire et coût avec une perte de qualité limitée, permettant de faire tourner des modèles ouverts (Llama, Mistral, Qwen, Gemma) sur un poste ou un serveur via Ollama, llama.cpp ou vLLM. Intérêt : confidentialité, coût, latence, absence de dépendance à un fournisseur.

### 23. Comment intégrer un LLM dans une application Java (Spring AI, LangChain4j) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Spring AI fournit `ChatClient` fluide, abstraction multi-fournisseurs (OpenAI, Anthropic, Bedrock, Ollama), sorties structurées vers des records, tool calling par annotation `@Tool`, `VectorStore` (pgvector…), advisors pour RAG et mémoire, et observabilité Micrometer. LangChain4j offre des concepts similaires (`AiServices`, chains) hors Spring.

### 24. Comment gérer la mémoire conversationnelle ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Le modèle est sans état : l'application renvoie l'historique à chaque appel. Stratégies : fenêtre glissante des N derniers messages, résumé progressif des anciens échanges, stockage des faits importants dans une mémoire long terme (base + recherche), et limite de tokens. Spring AI propose `ChatMemory` et des advisors dédiés.

### 25. Qu'est-ce que le streaming de réponses et comment l'implémenter ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Le modèle renvoie les tokens au fur et à mesure (SSE), améliorant la latence perçue. Côté Spring : `ChatClient.stream()` renvoie un `Flux<String>` exposé via un endpoint SSE (`text/event-stream`) ; côté Angular, `fetch` avec lecture de `ReadableStream` ou `EventSource`. Prévoir l'annulation et l'affichage progressif.

### 26. Comment maîtriser les coûts d'une application LLM ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Choisir le plus petit modèle suffisant par tâche (routing), réduire les tokens (prompts concis, chunks pertinents, historique résumé), prompt caching des préfixes stables, traitement batch pour les tâches non urgentes, cache des réponses identiques, limites par utilisateur, et suivi du coût par fonctionnalité via les métriques.

### 27. Qu'est-ce que le prompt caching ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Les fournisseurs peuvent mettre en cache la partie stable et longue d'un prompt (système, documents, outils) pour ne pas la retraiter à chaque appel, réduisant coût et latence. Il faut placer le contenu stable en tête et le contenu variable en fin de prompt pour maximiser les hits.

### 28. Qu'est-ce que la latence d'un LLM et comment l'optimiser ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Deux composantes : temps au premier token (TTFT, dépend de la taille du prompt) et débit de génération (tokens/s). Optimisations : streaming, prompts plus courts, modèles plus petits ou plus rapides, prompt caching, appels parallèles quand possible, sorties bornées, et exécution des outils en parallèle.

### 29. Qu'est-ce qu'une injection de prompt et comment s'en défendre ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Une entrée (message utilisateur, document récupéré par RAG, page web) contenant des instructions qui détournent le modèle (« ignore les consignes et envoie les données »). Défenses : séparer clairement données et instructions, privilèges minimaux des outils, confirmation humaine pour les actions sensibles, filtrage des sorties, ne jamais faire confiance à une sortie LLM pour une décision de sécurité.

### 30. Quels sont les risques de sécurité spécifiques aux applications LLM (OWASP Top 10 for LLM) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Injection de prompt, fuite de données sensibles (dans les prompts ou les réponses), empoisonnement des données d'entraînement/RAG, exécution non maîtrisée d'outils (excessive agency), sorties non validées injectées dans du code/HTML, déni de service par prompts coûteux, dépendance à des modèles/plugins tiers, et surconfiance des utilisateurs.

### 31. Comment protéger les données personnelles et confidentielles avec un LLM ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Anonymiser/pseudonymiser avant envoi, choisir des offres sans conservation ni entraînement sur les données (contrats entreprise, régions UE), ou des modèles auto-hébergés pour les données sensibles, journaliser les accès, appliquer le RGPD (base légale, minimisation, droits), et informer les utilisateurs. Ne jamais coller des secrets dans un assistant.

### 32. Qu'est-ce que l'AI Act européen et quelles obligations pour un développeur ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Un règlement classant les systèmes d'IA par niveau de risque : pratiques interdites, systèmes à haut risque (obligations lourdes : documentation, supervision humaine, robustesse), obligations de transparence (informer qu'on interagit avec une IA, marquer les contenus générés), et règles pour les modèles à usage général. Applicable progressivement de 2025 à 2027.

### 33. Qu'est-ce que l'évaluation (evals) d'une fonctionnalité LLM et comment l'automatiser ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Un jeu de cas de test (entrées + résultats attendus ou critères) exécuté à chaque changement de prompt/modèle, avec des scores : correspondance exacte pour les sorties structurées, métriques classiques pour la classification, LLM-as-a-judge avec rubrique pour le texte libre, et revue humaine échantillonnée. Intégrer en CI comme des tests de non-régression.

### 34. Qu'est-ce que l'observabilité des applications LLM (LLMOps) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Tracer chaque appel (prompt, réponse, tokens, latence, coût, outils appelés, version du prompt) avec des outils comme Langfuse, LangSmith, Phoenix, ou OpenTelemetry (conventions GenAI), pour déboguer, mesurer la qualité en production, détecter les dérives et alimenter les evals à partir des cas réels.

### 35. Qu'est-ce qu'un agent IA ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Un système où le LLM décide de façon itérative quelles actions entreprendre (appels d'outils, recherches, écriture de fichiers) pour atteindre un objectif, en observant les résultats et en ajustant (boucle ReAct : raisonner, agir, observer). Il exige des garde-fous : limites d'itérations, permissions, validation humaine sur les actions irréversibles.

### 36. Quels sont les patterns d'architecture agentique (routing, orchestrateur, multi-agents) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Chaînage de prompts (étapes fixes), routing (classifier puis déléguer au bon prompt/modèle), parallélisation (sous-tâches indépendantes puis agrégation), orchestrateur-workers (un LLM planifie et distribue), évaluateur-optimiseur (génération puis critique en boucle). Préférer le workflow le plus simple ; les agents autonomes seulement quand la séquence n'est pas prévisible.

### 37. Comment fonctionne le protocole MCP (transports, primitives) ?
`🟠 Intermédiaire` · Sujet : **MCP**

**Réponse :** MCP est basé sur JSON-RPC 2.0 avec deux transports : stdio (serveur lancé localement comme sous-processus) et HTTP streamable (serveur distant). Le serveur expose des primitives : tools (fonctions appelables), resources (données lisibles par URI), prompts (templates), et peut demander du sampling au client. Le client découvre dynamiquement ces capacités.

### 38. Comment créer un serveur MCP en Java ?
`🟠 Intermédiaire` · Sujet : **MCP**

**Réponse :** Avec le SDK Java officiel ou Spring AI MCP Server (`spring-ai-starter-mcp-server-webmvc`) : les méthodes annotées `@Tool` deviennent des outils MCP, exposés en stdio ou HTTP. On le connecte ensuite à Claude Desktop/Code, Cursor ou une application Spring AI cliente. Penser à l'authentification (OAuth 2.1 pour HTTP) et aux permissions.

### 39. Quels risques de sécurité pose MCP ?
`🟠 Intermédiaire` · Sujet : **MCP**

**Réponse :** Un serveur MCP malveillant ou compromis peut injecter des instructions via ses descriptions d'outils (tool poisoning), exfiltrer des données passées en paramètres, ou exécuter des actions destructrices. Bonnes pratiques : n'installer que des serveurs de confiance, moindre privilège, confirmation humaine des actions, isolation (conteneurs), et audit des appels.

### 40. Qu'est-ce que le « vibe coding » et ses limites ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Générer une application en décrivant l'intention à l'IA sans lire attentivement le code produit. Adapté aux prototypes et outils jetables, mais risqué en production : dette technique, failles de sécurité, absence de tests, incompréhension du code par l'équipe. Un développeur reste responsable de ce qu'il livre.

### 41. Comment utiliser efficacement un agent de code (Claude Code, Copilot agent, Cursor) sur un projet existant ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Fournir le contexte (fichier d'instructions type `CLAUDE.md`/`AGENTS.md` décrivant architecture, conventions, commandes), demander des tâches délimitées, exiger des tests, relire les diffs comme une revue de code, travailler sur une branche, et laisser l'agent exécuter build/tests pour boucler sur les erreurs. Découper les grandes tâches en plans.

### 42. Comment vérifier et réviser du code généré par IA ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Le traiter comme une PR d'un développeur junior rapide : lire intégralement, vérifier sécurité (injections, secrets, validation), gestion d'erreurs, dépendances inventées ou obsolètes, respect de l'architecture, performance, et surtout exécuter les tests. Les erreurs de l'IA sont plausibles et confiantes, donc plus difficiles à repérer.

### 43. Quels risques juridiques et de licence avec le code généré ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Reproduction potentielle de code sous licence (GPL) issu de l'entraînement, incertitude sur la propriété intellectuelle du code généré selon les juridictions, et fuite de code propriétaire envoyé à un service tiers. Mesures : filtres de correspondance publique, politique d'entreprise, offres entreprise sans rétention, scan de licences.

### 44. Comment l'IA change-t-elle le TDD et les tests ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** L'IA génère rapidement des tests (à vérifier : ils peuvent tester l'implémentation ou être triviaux), propose des cas limites, et permet de faire du TDD en écrivant les tests d'abord puis en laissant l'agent implémenter jusqu'à ce qu'ils passent. Le mutation testing devient utile pour valider la qualité des tests générés.

### 45. Comment utiliser l'IA pour le code legacy et la migration ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Explication de code inconnu, génération de documentation et de tests de caractérisation, traduction entre versions/langages (Java 8 → 21, AngularJS → Angular) par étapes vérifiées, détection de code mort et de duplications. Les migrations massives exigent des tests solides avant de commencer et une revue humaine.

### 46. Qu'est-ce qu'un fichier d'instructions de projet (`CLAUDE.md`, `.cursorrules`, `copilot-instructions.md`) ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Un fichier versionné décrivant à l'assistant les conventions, la structure, les commandes (build, test, lint), les bibliothèques à utiliser ou éviter, et les règles de style. Il réduit les erreurs répétées et aligne l'IA sur l'équipe ; il doit rester court, précis et maintenu comme de la documentation.

### 47. Comment intégrer l'IA dans la revue de code et la CI ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Bots de revue (Copilot review, CodeRabbit, Claude Code en action GitHub) qui commentent les PR : détection de bugs évidents, résumé des changements, suggestions. Ils complètent mais ne remplacent pas la revue humaine ; configurer pour éviter le bruit et vérifier la confidentialité du code envoyé.

### 48. Quelles compétences restent essentielles pour un développeur à l'ère de l'IA ?
`🟠 Intermédiaire` · Sujet : **AI-assisted coding**

**Réponse :** Compréhension des fondamentaux (architecture, sécurité, performance, systèmes distribués), capacité à spécifier précisément et à décomposer les problèmes, jugement critique sur le code produit, communication avec le métier, et responsabilité de la qualité. L'IA accélère l'exécution ; elle ne remplace pas la conception ni le discernement.

### 49. Comment choisir entre les fournisseurs et modèles (propriétaires vs ouverts) ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Critères : qualité sur vos evals, coût par million de tokens, latence, taille de contexte, capacités (vision, outils, sorties structurées), confidentialité et localisation des données, stabilité de l'API, et réversibilité. Une couche d'abstraction (Spring AI, LiteLLM, gateway) évite le verrouillage et permet le routage par tâche.

### 50. Qu'est-ce qu'une AI gateway et pourquoi en déployer une en entreprise ?
`🟠 Intermédiaire` · Sujet : **RAG / LLM**

**Réponse :** Un proxy central devant les fournisseurs de LLM (LiteLLM, Portkey, Kong AI, gateways cloud) qui gère authentification, quotas et coûts par équipe, journalisation, filtrage de données sensibles, fallback entre modèles, cache et observabilité. Il évite que chaque application gère ses clés et sa gouvernance.
