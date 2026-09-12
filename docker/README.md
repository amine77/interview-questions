# 🐳 Docker

> Images, conteneurs, multi-stage builds, networking, volumes

**8 questions**

---

### 1. Quelle est la différence entre une image et un conteneur Docker ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** Une image est un modèle immuable en lecture seule contenant le code, les dépendances et la configuration. Un conteneur est une instance en cours d'exécution de cette image, avec un état modifiable.

### 2. À quoi sert un multi-stage build ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Utiliser plusieurs étapes (`FROM`) : build avec tous les outils, puis étape finale ne copiant que les artefacts, réduisant la taille de l'image.

### 3. Différence `CMD` / `ENTRYPOINT` ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** ENTRYPOINT = commande principale difficile à surcharger. CMD = arguments par défaut remplaçables à l'exécution.

### 4. Différence `docker run` / `docker start` ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** `run` crée et démarre un nouveau conteneur. `start` redémarre un conteneur existant arrêté.

### 5. Qu'est-ce qu'un volume Docker ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Mécanisme de persistance de données indépendant du cycle de vie du conteneur.

### 6. Différence `docker-compose up` / `up -d` ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** `up` attaché (logs visibles). `-d` détaché (arrière-plan).

### 7. Pourquoi créer un réseau Docker personnalisé ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Résolution DNS automatique par nom de conteneur, isolation de la communication.

### 8. Qu'est-ce que `.dockerignore` ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Liste les fichiers exclus du contexte de build envoyé au daemon Docker.
