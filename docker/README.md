# 🐳 Docker

> Images, conteneurs, multi-stage builds, networking, volumes

**50 questions**

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

### 9. Différence entre un conteneur et une machine virtuelle ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** Une VM virtualise le matériel et embarque un OS complet (lourd, démarrage en minutes, isolation forte). Un conteneur partage le noyau de l'hôte et isole les processus via namespaces et cgroups (léger, démarrage en secondes, isolation plus faible). Les conteneurs sont adaptés au packaging d'applications, les VM à l'isolation forte et aux OS différents.

### 10. Quelles sont les couches (layers) d'une image et comment fonctionne le cache de build ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** Chaque instruction du Dockerfile crée une couche immuable empilée via un système de fichiers en union (overlay2). Au build, une couche est réutilisée si l'instruction et son contexte sont inchangés ; dès qu'une couche change, toutes les suivantes sont reconstruites. D'où l'ordre : dépendances (changent peu) avant code source.

### 11. Différence entre `COPY` et `ADD` ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** `COPY` copie des fichiers du contexte de build. `ADD` fait de même mais décompresse automatiquement les archives locales et accepte des URL, comportements implicites source de surprises. La recommandation est d'utiliser `COPY` sauf besoin explicite de décompression.

### 12. Différence entre `EXPOSE` et `-p` ?
`🟢 Débutant` · Sujet : **Docker**

**Réponse :** `EXPOSE` est une documentation dans l'image indiquant les ports écoutés ; il ne publie rien. `docker run -p 8080:80` mappe réellement un port de l'hôte vers le conteneur. `-P` publie tous les ports `EXPOSE` sur des ports aléatoires.

### 13. Comment écrire un bon Dockerfile pour une application Spring Boot ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Multi-stage : étape de build avec Maven/Gradle et cache des dépendances, étape finale sur une image JRE minimale (Temurin, distroless), utilisateur non-root, extraction du jar en layers (`java -Djarmode=tools -jar app.jar extract --layers`) pour que les dépendances soient une couche stable, `ENTRYPOINT ["java", ...]` en forme exec, et `HEALTHCHECK` ou probes Kubernetes.

### 14. Pourquoi utiliser la forme exec (`["java","-jar"]`) plutôt que shell pour `ENTRYPOINT`/`CMD` ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** La forme shell lance `/bin/sh -c`, faisant du shell le PID 1 : les signaux (SIGTERM) n'atteignent pas l'application, qui est tuée brutalement après le timeout, et les variables d'environnement s'y interprètent. La forme exec fait de l'application le PID 1 et lui transmet les signaux, permettant le graceful shutdown.

### 15. Qu'est-ce que le problème du PID 1 et des zombies, et quand utiliser `tini`/`--init` ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Le PID 1 doit récolter les processus orphelins et gérer les signaux ; une application classique ne le fait pas. Si le conteneur lance des sous-processus (scripts, navigateurs headless), `docker run --init` ou `tini` comme entrypoint évite les zombies et propage correctement les signaux.

### 16. Comment réduire la taille d'une image ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Image de base minimale (Alpine, distroless, `-slim`), multi-stage pour exclure les outils de build, regrouper `RUN` et nettoyer dans la même couche (`apt-get clean`, `rm -rf /var/lib/apt/lists/*`), `.dockerignore` strict, pas de fichiers temporaires, et analyse avec `docker history` ou `dive`.

### 17. Quels sont les pièges d'Alpine pour Java ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Alpine utilise musl au lieu de glibc : certaines librairies natives (et anciennement le JDK) ne fonctionnent pas ou nécessitent des builds spécifiques ; problèmes de DNS et de locales ont existé. Aujourd'hui Temurin fournit des images Alpine officielles, mais distroless ou Ubuntu chiseled/`-jammy` restent des choix sûrs.

### 18. Comment exécuter un conteneur en tant qu'utilisateur non-root ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Créer un utilisateur dans le Dockerfile (`RUN adduser --system app`) puis `USER app` avant l'entrypoint, en s'assurant que les fichiers nécessaires sont accessibles (`COPY --chown`). Éviter les ports < 1024. Kubernetes peut l'imposer avec `runAsNonRoot`. Docker rootless renforce en plus la sécurité du démon.

### 19. Différence entre volume nommé, bind mount et tmpfs ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Volume nommé : géré par Docker (`/var/lib/docker/volumes`), portable, idéal pour les données persistantes (bases). Bind mount : monte un chemin de l'hôte (développement, configuration). tmpfs : en mémoire, non persistant, pour les données sensibles temporaires. En Kubernetes, ces notions deviennent PVC, hostPath et emptyDir.

### 20. Quels sont les drivers réseau Docker ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `bridge` (défaut, réseau privé sur l'hôte avec NAT ; un réseau bridge personnalisé apporte la résolution DNS par nom de conteneur), `host` (partage la pile réseau de l'hôte, sans isolation), `none`, `overlay` (multi-hôtes avec Swarm), `macvlan` (adresse MAC propre sur le réseau physique).

### 21. Comment les conteneurs d'un même `docker compose` communiquent-ils ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Compose crée un réseau bridge dédié au projet ; chaque service est joignable par son nom (`db:5432`) grâce au DNS intégré. Les ports internes n'ont pas besoin d'être publiés pour la communication inter-conteneurs, seulement pour l'accès depuis l'hôte.

### 22. Que sont `depends_on`, `healthcheck` et `condition: service_healthy` dans Compose ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `depends_on` ordonne le démarrage mais n'attend pas que le service soit prêt. Avec un `healthcheck` défini sur la dépendance et `depends_on: db: condition: service_healthy`, Compose attend que la base réponde réellement avant de lancer l'application, évitant les échecs de connexion au démarrage.

### 23. Comment gérer la configuration et les secrets avec Compose ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Variables via `environment`, `env_file` (`.env` non commité), substitution `${VAR:-default}`. Pour les secrets, `secrets:` monte des fichiers dans `/run/secrets/` plutôt que des variables d'environnement visibles dans `docker inspect`. Les `profiles` activent des services optionnels (`--profile debug`).

### 24. Différence entre `docker compose` (v2) et `docker-compose` (v1), et que sont les overrides ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `docker compose` est le plugin Go intégré à Docker CLI (v1 Python est déprécié). Compose fusionne automatiquement `compose.yaml` et `compose.override.yaml` (config locale), et `-f` permet d'empiler des fichiers par environnement. `docker compose config` affiche la configuration finale.

### 25. Comment déboguer un conteneur qui s'arrête immédiatement ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `docker logs <id>` (ou `docker compose logs`), `docker inspect --format '{{.State.ExitCode}}'` (137 = OOM/SIGKILL, 139 = segfault, 1 = erreur applicative), lancer avec un entrypoint alternatif (`docker run -it --entrypoint sh image`) pour inspecter le système de fichiers, vérifier les permissions, variables et le chemin de l'exécutable.

### 26. Que signifient les codes de sortie 137 et 143 ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** 128 + numéro du signal : 137 = SIGKILL (9), typiquement OOM killer ou `docker kill` ; 143 = SIGTERM (15), arrêt demandé proprement. Un 137 récurrent indique une limite mémoire trop basse ou une JVM mal dimensionnée.

### 27. Comment limiter les ressources d'un conteneur ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `--memory=512m`, `--memory-swap`, `--cpus=1.5` ou `--cpu-shares` (poids relatif), `--pids-limit`. Ces limites s'appuient sur les cgroups (v2 par défaut aujourd'hui). La JVM lit ces limites (`UseContainerSupport`) pour dimensionner heap et threads.

### 28. Comment Docker gère-t-il les logs et quels drivers existent ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Par défaut `json-file` capture stdout/stderr dans un fichier par conteneur (à limiter avec `max-size`/`max-file` pour éviter de remplir le disque). Autres drivers : `local`, `journald`, `syslog`, `fluentd`, `awslogs`, `gelf`. L'application doit écrire sur stdout, jamais dans des fichiers internes.

### 29. Qu'est-ce qu'un `HEALTHCHECK` dans une image ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Une commande exécutée périodiquement (`HEALTHCHECK --interval=30s CMD curl -f http://localhost:8080/actuator/health || exit 1`) qui définit l'état healthy/unhealthy du conteneur, visible dans `docker ps` et utilisable par Compose. Kubernetes l'ignore et utilise ses propres probes.

### 30. Comment scanner une image pour les vulnérabilités ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Trivy (`trivy image app:1.0`), Grype, Docker Scout ou Snyk analysent les paquets OS et les dépendances applicatives (jar, npm) contre les bases CVE. Intégrer en CI avec un seuil bloquant (CRITICAL/HIGH corrigeables), et rescanner régulièrement les images déployées car de nouvelles CVE apparaissent.

### 31. Qu'est-ce qu'un digest d'image et pourquoi épingler par digest ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Le digest `sha256:...` identifie de manière immuable le contenu d'une image, contrairement à un tag qui peut être réassigné. `FROM eclipse-temurin:21-jre@sha256:...` garantit la reproductibilité et protège contre la substitution d'image ; Renovate met à jour le digest lors des nouvelles versions.

### 32. Comment signer et vérifier des images (cosign, Notation) ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `cosign sign` signe le digest d'une image et stocke la signature dans la registry ; `cosign verify` (ou une policy Kyverno/Gatekeeper) vérifie avant déploiement. Le mode keyless utilise l'identité OIDC de la CI (Sigstore/Fulcio/Rekor). Notation est l'alternative du projet Notary v2.

### 33. Qu'est-ce qu'une image multi-architecture et comment la construire ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Un manifest list référençant une image par plateforme (`linux/amd64`, `linux/arm64`) sous un même tag : le client récupère la variante adaptée. `docker buildx build --platform linux/amd64,linux/arm64 --push` la construit via QEMU ou des builders natifs. Indispensable pour les Mac Apple Silicon et les instances ARM (Graviton).

### 34. Qu'est-ce que le cache mount et le secret mount de BuildKit ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `RUN --mount=type=cache,target=/root/.m2 mvn package` conserve le cache Maven entre builds sans le laisser dans l'image. `RUN --mount=type=secret,id=npmrc` rend un secret disponible pendant l'instruction sans le persister dans une couche (contrairement à `ARG`, visible dans `docker history`).

### 35. Différence entre `ARG` et `ENV` ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `ARG` est une variable de build (`--build-arg`) disponible uniquement pendant le build, absente du conteneur final (mais visible dans l'historique). `ENV` définit une variable d'environnement persistante dans l'image et le conteneur. Un pattern courant : `ARG VERSION` puis `ENV APP_VERSION=$VERSION`.

### 36. Qu'est-ce que le contexte de build et pourquoi `.dockerignore` est-il crucial ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Tout le répertoire passé à `docker build` est envoyé au démon. Sans `.dockerignore`, `node_modules`, `.git`, `target/` alourdissent l'envoi, invalident le cache et peuvent fuiter des secrets (`.env`) dans l'image. Le fichier suit la syntaxe de `.gitignore`.

### 37. Comment fonctionne le rechargement à chaud (hot reload) en développement avec Docker ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Bind mount du code source dans le conteneur et outil de watch (Spring DevTools, nodemon, `ng serve`), ou `docker compose watch` (sync/rebuild automatiques). Sur macOS/Windows, les performances des bind mounts sont limitées ; Docker Desktop propose VirtioFS, et des outils comme Tilt/Skaffold ciblent Kubernetes.

### 38. Qu'est-ce que la registry Docker et comment héberger une registry privée ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Une registry stocke et distribue les images (Docker Hub, GHCR, ECR, GitLab Registry, Harbor, Nexus). Une registry privée exige authentification (`docker login`, `imagePullSecrets` dans Kubernetes), politiques de rétention, scan intégré (Harbor) et éventuellement un proxy/cache (pull-through) pour limiter les rate limits de Docker Hub.

### 39. Comment nettoyer l'espace disque utilisé par Docker ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `docker system df` montre l'usage ; `docker system prune` supprime conteneurs arrêtés, réseaux et images dangling ; `-a` retire aussi les images non utilisées ; `docker volume prune` les volumes orphelins (attention aux données). Sur les nœuds Kubernetes, kubelet gère le garbage collection des images.

### 40. Différence entre `docker stop`, `docker kill` et `docker rm -f` ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** `stop` envoie SIGTERM puis SIGKILL après 10 s (`-t`), laissant le temps d'un arrêt propre. `kill` envoie directement SIGKILL (ou un signal choisi). `rm -f` tue puis supprime le conteneur. `docker restart` combine stop et start.

### 41. Qu'est-ce que l'OCI et la différence entre Docker, containerd, CRI-O et Podman ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** L'Open Container Initiative standardise les formats d'image et de runtime, assurant l'interopérabilité. containerd et CRI-O sont des runtimes de haut niveau utilisés par Kubernetes (Docker n'y est plus nécessaire depuis 1.24) ; runc exécute réellement les conteneurs. Podman est une alternative à la CLI Docker sans démon, rootless par défaut.

### 42. Qu'est-ce que Docker Swarm et pourquoi Kubernetes l'a-t-il supplanté ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Swarm est l'orchestrateur intégré à Docker : simple (`docker stack deploy` avec un fichier Compose), mais limité en fonctionnalités (autoscaling, écosystème, CRDs, stockage). Kubernetes s'est imposé pour la production ; Swarm reste pertinent pour de petits déploiements ou l'edge.

### 43. Comment passer les options JVM et le profil Spring à un conteneur ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Par variables d'environnement : `JAVA_TOOL_OPTIONS` (lue automatiquement par la JVM) ou `JDK_JAVA_OPTIONS` (pour le lanceur `java` seulement), et `SPRING_PROFILES_ACTIVE=prod`. Cela évite de reconstruire l'image par environnement et permet à Kubernetes de les injecter via ConfigMap.

### 44. Comment déboguer une application Java dans un conteneur ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Activer JDWP via `JAVA_TOOL_OPTIONS=-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005` et publier le port, puis attacher l'IDE. Pour les diagnostics : `docker exec` avec `jcmd`/`jstack` (si présents dans l'image, sinon `kubectl debug`/conteneur éphémère), JFR activé à distance, Actuator.

### 45. Qu'est-ce que les Cloud Native Buildpacks (`pack`, Spring Boot `build-image`) ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Une alternative au Dockerfile : `mvn spring-boot:build-image` ou `pack build` détectent le type d'application et produisent une image OCI optimisée (couches, JVM configurée par le memory calculator, SBOM inclus) sans écrire de Dockerfile. Avantage : bonnes pratiques par défaut ; inconvénient : moins de contrôle et images plus grosses.

### 46. Qu'est-ce que Jib ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Un plugin Maven/Gradle de Google qui construit des images Java sans Docker installé ni Dockerfile, directement vers la registry, en séparant dépendances, ressources et classes en couches reproductibles. Très rapide en CI et compatible avec l'absence de démon Docker.

### 47. Comment sécuriser le démon Docker et l'accès au socket ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Ne jamais exposer `/var/run/docker.sock` à un conteneur non fiable (accès root sur l'hôte), ni le socket TCP sans TLS. Utiliser Docker rootless, restreindre le groupe `docker`, privilégier `docker context` avec SSH, et en CI préférer BuildKit/Kaniko/Buildah à Docker-in-Docker privilégié.

### 48. Qu'est-ce que Docker-in-Docker et ses alternatives en CI ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** DinD lance un démon Docker dans le job CI (conteneur privilégié, risque de sécurité, cache non persistant). Alternatives : monter le socket de l'hôte (partage du démon), ou des builders sans démon : Kaniko, Buildah, BuildKit en mode rootless, Jib/Buildpacks pour Java.

### 49. Comment gérer les fuseaux horaires, locales et l'entropie dans un conteneur ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Le conteneur est en UTC par défaut : injecter `TZ=Europe/Paris` (avec `tzdata` installé) ou, mieux, garder UTC et convertir à l'affichage. Locales : définir `LANG`/`LC_ALL` si l'application en dépend. Pour la JVM, `-Djava.security.egd=file:/dev/./urandom` évitait les blocages d'entropie sur les anciennes versions.

### 50. Comment mettre en œuvre un conteneur « distroless » et le déboguer ?
`🟠 Intermédiaire` · Sujet : **Docker**

**Réponse :** Une image sans shell, gestionnaire de paquets ni outils (`gcr.io/distroless/java21`), réduisant fortement la surface d'attaque. Pour déboguer : variante `:debug` avec busybox, conteneur éphémère `kubectl debug --image=busybox --target=app` partageant les namespaces, ou `docker cp` des fichiers vers l'hôte.
