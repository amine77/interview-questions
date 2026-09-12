# 🐧 Linux, Réseau & Shell pour développeurs

> TCP, HTTP/2 et HTTP/3, DNS, TLS, outils de diagnostic, scripting bash

**51 questions**

---

### 1. Quelles sont les couches du modèle TCP/IP et à quoi correspondent-elles ?
`🟢 Débutant` · Sujet : **Réseau**

**Réponse :** Accès réseau (Ethernet, Wi-Fi), Internet (IP : adressage et routage), Transport (TCP fiable et ordonné, UDP léger sans garantie), Application (HTTP, DNS, TLS, SSH). Un développeur travaille surtout aux couches transport et application ; les problèmes de latence, MTU ou pare-feu se situent en dessous.

### 2. Comment fonctionne l'établissement d'une connexion TCP (three-way handshake) ?
`🟢 Débutant` · Sujet : **Réseau**

**Réponse :** Le client envoie SYN, le serveur répond SYN-ACK, le client confirme par ACK : la connexion est établie, avec numéros de séquence synchronisés. Cela coûte un aller-retour (RTT) avant toute donnée, d'où l'intérêt des connexions persistantes (keep-alive), du pooling et de HTTP/2. La fermeture se fait par FIN/ACK de chaque côté (état TIME_WAIT côté initiateur).

### 3. Différence entre TCP et UDP, et quand utiliser UDP ?
`🟢 Débutant` · Sujet : **Réseau**

**Réponse :** TCP : orienté connexion, fiable, ordonné, contrôle de flux et de congestion ; adapté à HTTP, bases de données, SSH. UDP : sans connexion, pas de retransmission ni d'ordre, faible latence ; utilisé pour DNS, streaming vidéo/voix, jeux, et par QUIC (HTTP/3) qui réimplémente la fiabilité au-dessus.

### 4. Qu'est-ce qu'un port et quels ports faut-il connaître ?
`🟢 Débutant` · Sujet : **Réseau**

**Réponse :** Un numéro (0-65535) identifiant un service sur une machine. Ports < 1024 réservés à root. À connaître : 22 SSH, 53 DNS, 80 HTTP, 443 HTTPS, 25/587 SMTP, 3306 MySQL, 5432 PostgreSQL, 6379 Redis, 9092 Kafka, 8080 alternatif HTTP. `ss -tlnp` liste les ports en écoute avec le processus.

### 5. Comment fonctionne la résolution DNS ?
`🟢 Débutant` · Sujet : **DNS**

**Réponse :** Le résolveur (souvent celui du système ou du réseau) vérifie son cache, puis interroge récursivement : serveurs racine → serveurs du TLD (`.com`) → serveurs autoritaires du domaine, qui renvoient l'enregistrement. Chaque réponse porte un TTL de cache. Types courants : A/AAAA (adresse IPv4/IPv6), CNAME (alias), MX (mail), TXT (vérifications, SPF), NS, SRV.

### 6. Pourquoi le TTL DNS est-il important lors d'un déploiement ou d'une migration ?
`🟠 Intermédiaire` · Sujet : **DNS**

**Réponse :** Les résolveurs cachent les enregistrements pendant le TTL : un changement d'IP n'est vu qu'à expiration. Avant une migration, abaisser le TTL (60 s) plusieurs heures à l'avance, basculer, puis le remonter. Attention aux clients Java : la JVM cache les résolutions DNS (`networkaddress.cache.ttl`) indépendamment du TTL, source classique de pannes après bascule.

### 7. Comment fonctionne le DNS dans Kubernetes et Docker ?
`🟠 Intermédiaire` · Sujet : **DNS**

**Réponse :** CoreDNS résout `service.namespace.svc.cluster.local` vers le ClusterIP (ou les IPs des Pods pour un service headless) ; les Pods ont `/etc/resolv.conf` avec des `search` domains permettant `service` ou `service.namespace`. Docker Compose fournit un DNS interne où chaque service est joignable par son nom sur le réseau du projet.

### 8. Quelles sont les différences entre HTTP/1.1, HTTP/2 et HTTP/3 ?
`🟠 Intermédiaire` · Sujet : **HTTP**

**Réponse :** HTTP/1.1 : texte, une requête à la fois par connexion (head-of-line blocking), d'où plusieurs connexions parallèles. HTTP/2 : binaire, multiplexage de flux sur une connexion, compression des headers (HPACK), priorisation ; mais un paquet TCP perdu bloque tous les flux. HTTP/3 : sur QUIC (UDP), flux indépendants, handshake TLS intégré (0-RTT), migration de connexion (changement de réseau mobile).

### 9. Qu'est-ce que le head-of-line blocking ?
`🟠 Intermédiaire` · Sujet : **HTTP**

**Réponse :** Une situation où un élément en attente bloque tous ceux derrière lui. En HTTP/1.1, une réponse lente bloque les suivantes sur la même connexion. En HTTP/2, le multiplexage résout ce point applicatif mais TCP réintroduit le blocage au niveau des paquets perdus. QUIC/HTTP/3 traite chaque flux indépendamment et supprime les deux.

### 10. Comment fonctionnent les connexions persistantes et le keep-alive ?
`🟠 Intermédiaire` · Sujet : **HTTP**

**Réponse :** En HTTP/1.1 la connexion reste ouverte après la réponse pour réutilisation (`Connection: keep-alive` implicite), évitant handshakes TCP/TLS répétés. Côté client Java, `HttpClient`, RestClient et les pools (Apache HttpClient) réutilisent les connexions ; côté serveur, un timeout d'inactivité ferme les connexions. Les load balancers doivent être configurés avec des timeouts cohérents pour éviter les erreurs de connexion réinitialisée.

### 11. Que sont les codes de statut HTTP à connaître et leurs pièges ?
`🟠 Intermédiaire` · Sujet : **HTTP**

**Réponse :** 2xx succès (200, 201 créé, 202 accepté, 204 sans contenu), 3xx redirections (301/308 permanent, 302/307 temporaire, 304 non modifié), 4xx erreur client (400, 401 non authentifié, 403 non autorisé, 404, 409 conflit, 422, 429 trop de requêtes), 5xx serveur (500, 502 bad gateway, 503 indisponible, 504 timeout amont). 502/504 signalent presque toujours un problème entre le proxy et le backend.

### 12. Comment fonctionne le cache HTTP (`Cache-Control`, `ETag`) ?
`🟠 Intermédiaire` · Sujet : **HTTP**

**Réponse :** `Cache-Control: max-age=3600, public` autorise le cache (navigateur, CDN) ; `no-store` l'interdit ; `no-cache` impose une revalidation. `ETag`/`Last-Modified` permettent une requête conditionnelle (`If-None-Match`) répondue par 304 sans corps. `stale-while-revalidate` sert l'ancien contenu pendant le rafraîchissement. `Vary` indique les headers influençant la réponse.

### 13. Comment fonctionne TLS à haut niveau ?
`🟠 Intermédiaire` · Sujet : **TLS**

**Réponse :** Le client et le serveur négocient une version et une suite de chiffrement, le serveur présente son certificat (vérifié par la chaîne jusqu'à une autorité de confiance et le nom d'hôte), un échange de clés (ECDHE, confidentialité persistante) établit une clé de session symétrique qui chiffre ensuite le trafic. TLS 1.3 réduit le handshake à un aller-retour et supprime les algorithmes faibles.

### 14. Qu'est-ce qu'un certificat X.509, une chaîne de certification et Let's Encrypt ?
`🟠 Intermédiaire` · Sujet : **TLS**

**Réponse :** Un certificat lie une clé publique à une identité (nom de domaine), signé par une autorité de certification (CA). La chaîne va du certificat serveur aux intermédiaires puis à la racine présente dans le magasin de confiance du client. Let's Encrypt délivre gratuitement des certificats de 90 jours via le protocole ACME (validation HTTP-01 ou DNS-01), automatisés par certbot ou cert-manager.

### 15. Quelles sont les erreurs TLS courantes et comment les diagnostiquer ?
`🟠 Intermédiaire` · Sujet : **TLS**

**Réponse :** Certificat expiré, nom d'hôte non couvert (SAN), chaîne intermédiaire manquante (fonctionne dans le navigateur qui la connaît, échoue en Java : `PKIX path building failed`), CA privée absente du truststore, versions/ciphers incompatibles. Diagnostiquer avec `openssl s_client -connect host:443 -servername host`, `curl -v`, et pour Java `-Djavax.net.debug=ssl:handshake`.

### 16. Qu'est-ce que le mTLS et où est-il utilisé ?
`🟠 Intermédiaire` · Sujet : **TLS**

**Réponse :** TLS mutuel : le client présente aussi un certificat, authentifiant les deux parties. Utilisé entre services (service mesh comme Istio/Linkerd, qui gère l'émission et la rotation automatiquement), pour les APIs B2B sensibles et l'accès à des infrastructures. Il remplace ou complète les secrets partagés, mais exige une PKI et une gestion du cycle de vie des certificats.

### 17. Comment gérer un truststore et un keystore en Java ?
`🟠 Intermédiaire` · Sujet : **TLS**

**Réponse :** Le keystore contient la clé privée et le certificat du serveur (`server.ssl.key-store` dans Spring Boot, formats PKCS12 recommandé). Le truststore contient les CA de confiance (`cacerts` du JDK par défaut, ou `-Djavax.net.ssl.trustStore`). Ajouter une CA interne : `keytool -importcert -alias corp -file ca.pem -cacerts`. Spring Boot 3.1+ propose les SSL Bundles pour configurer ces éléments par propriétés et les recharger.

### 18. Qu'est-ce que la latence, le débit et le RTT, et comment les mesurer ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Latence : délai pour qu'un paquet arrive ; RTT : aller-retour ; débit : quantité de données par seconde. Une application « lente » peut être limitée par le RTT (nombreux petits appels séquentiels) plus que par le débit. Mesurer avec `ping` (RTT ICMP), `curl -w '%{time_connect} %{time_starttransfer} %{time_total}'`, `mtr` (latence par saut), `iperf3` (débit).

### 19. Comment diagnostiquer « je n'arrive pas à joindre le service » étape par étape ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** 1) Résolution : `dig host` / `nslookup`. 2) Routage et joignabilité : `ping`, `traceroute`/`mtr`. 3) Port ouvert : `nc -zv host 443`, `telnet`. 4) Couche applicative : `curl -v` (handshake TLS, code HTTP, headers). 5) Côté serveur : `ss -tlnp` (le service écoute-t-il sur la bonne interface, pas seulement `127.0.0.1` ?), pare-feu (`iptables`/security groups), logs. Isoler la couche qui échoue.

### 20. Qu'est-ce qu'un proxy, un reverse proxy et un load balancer ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Un proxy (forward) agit pour le client vers l'extérieur (filtrage, cache, sortie d'entreprise ; variables `HTTP_PROXY`). Un reverse proxy (Nginx, Traefik, Envoy) reçoit les requêtes pour le compte de serveurs backend : terminaison TLS, routage, cache, compression. Un load balancer répartit le trafic entre instances (L4 sur TCP, L7 sur HTTP avec règles). Les headers `X-Forwarded-For`/`X-Forwarded-Proto` transmettent l'origine réelle.

### 21. Qu'est-ce que NAT, une IP privée et pourquoi un service dans un conteneur n'est-il pas joignable de l'extérieur ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Les plages privées (10/8, 172.16/12, 192.168/16) ne sont pas routables sur Internet ; le NAT traduit les adresses à la sortie. Un conteneur a une IP privée sur un réseau virtuel : il faut publier un port (`-p 8080:8080`) pour que l'hôte le redirige, et écouter sur `0.0.0.0` (pas `localhost`) dans le conteneur.

### 22. Qu'est-ce que le MTU et pourquoi certaines requêtes échouent-elles seulement avec de gros payloads ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** La taille maximale d'un paquet sur un lien (1500 octets Ethernet, moins avec VPN/tunnels/overlays Kubernetes). Si la découverte du MTU (PMTUD) est bloquée par un pare-feu filtrant ICMP, les gros paquets sont perdus silencieusement : les petites requêtes passent, les grosses restent bloquées. Diagnostic : `ping -M do -s 1400 host` ; remède : abaisser le MTU ou autoriser ICMP.

### 23. Que sont les WebSockets et Server-Sent Events, et leurs contraintes réseau ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** WebSocket : connexion bidirectionnelle persistante issue d'un upgrade HTTP ; SSE : flux unidirectionnel serveur→client sur HTTP simple, reconnexion automatique. Contraintes : proxies et load balancers doivent supporter l'upgrade et avoir des timeouts longs, affinité ou bus partagé (Redis) pour le multi-instances, et gestion des reconnexions côté client.

### 24. Quelle est la structure du système de fichiers Linux ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** `/etc` configuration, `/var` données variables (logs dans `/var/log`, données d'applications dans `/var/lib`), `/tmp` temporaire, `/home` utilisateurs, `/opt` logiciels tiers, `/usr` programmes et bibliothèques, `/proc` et `/sys` interfaces vers le noyau (état des processus, ressources), `/dev` périphériques. Savoir où chercher les logs et la configuration accélère tout diagnostic.

### 25. Comment fonctionnent les permissions Linux (rwx, chmod, chown, umask) ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Trois triplets (propriétaire, groupe, autres) de droits lecture/écriture/exécution, en notation symbolique ou octale (`chmod 640 file` = rw-r-----). Pour un répertoire, x signifie « traverser ». `chown user:group` change le propriétaire, `umask` fixe les droits par défaut à la création. Bits spéciaux : setuid/setgid, sticky bit (`/tmp`). Les conteneurs non-root doivent avoir les droits d'écriture nécessaires sur leurs volumes.

### 26. Qu'est-ce qu'un processus, un signal, et comment arrêter proprement une application ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Un processus a un PID, un parent, des descripteurs de fichiers et un état. Les signaux (`kill -SIGTERM pid`) demandent une action : SIGTERM (arrêt gracieux, à intercepter pour terminer proprement, ce que fait Spring Boot avec le graceful shutdown), SIGKILL (arrêt immédiat, non interceptable), SIGHUP (rechargement pour beaucoup de daemons). Kubernetes envoie SIGTERM puis SIGKILL après `terminationGracePeriodSeconds`. Le PID 1 d'un conteneur doit propager les signaux (utiliser `exec` ou `tini`).

### 27. Comment surveiller CPU, mémoire, disque et I/O ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** `top`/`htop` (processus, charge), `uptime` (load average : nombre de processus en attente de CPU ou d'I/O, à comparer au nombre de cœurs), `free -h` (mémoire, en distinguant cache et réellement utilisée), `vmstat 1`, `iostat -x 1` (utilisation disque, latence), `df -h` (espace), `du -sh *` (taille des répertoires), `iotop`, `pidstat`. Un load élevé avec CPU faible indique une attente I/O.

### 28. Qu'est-ce que la mémoire résidente, virtuelle, le swap et l'OOM killer ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** VSZ : mémoire virtuelle réservée ; RSS : mémoire physique réellement utilisée. Le swap déplace des pages sur disque en cas de pression (dégrade fortement une JVM : le désactiver ou `swappiness` bas sur les serveurs Java). Quand la mémoire est épuisée, l'OOM killer du noyau tue le processus le plus gourmand ; dans un conteneur, dépasser la limite cgroup provoque un `OOMKilled` (exit code 137).

### 29. Que sont les descripteurs de fichiers et l'erreur « Too many open files » ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Chaque fichier, socket ou pipe ouvert consomme un descripteur, limité par processus (`ulimit -n`, souvent 1024 par défaut) et globalement. Une application serveur avec beaucoup de connexions ou une fuite de connexions non fermées atteint la limite. Diagnostic : `ls /proc/<pid>/fd | wc -l`, `lsof -p <pid>` ; remède : corriger la fuite, augmenter la limite (`LimitNOFILE` systemd, `ulimits` Docker).

### 30. Comment fonctionnent les logs système et journald ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Les services systemd écrivent dans le journal : `journalctl -u myapp -f` (suivre), `--since "1 hour ago"`, `-p err`. Les applications classiques écrivent dans `/var/log` avec rotation par `logrotate`. En conteneur, écrire sur stdout/stderr pour que Docker/Kubernetes collecte (`kubectl logs`). Un disque plein de logs est une cause fréquente de panne : surveiller `df`.

### 31. Qu'est-ce que systemd et comment gérer un service ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Le gestionnaire de services et d'init des distributions modernes. Un fichier unit (`/etc/systemd/system/app.service`) décrit la commande, l'utilisateur, les dépendances, le redémarrage automatique (`Restart=on-failure`), les limites et variables d'environnement. Commandes : `systemctl start|stop|restart|status|enable app`, `systemctl daemon-reload` après modification, `journalctl -u app` pour les logs.

### 32. Qu'est-ce que SSH et comment l'utiliser efficacement ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Un protocole d'accès distant chiffré. Authentification par clés (`ssh-keygen -t ed25519`, `ssh-copy-id`) plutôt que par mot de passe, `~/.ssh/config` pour les alias et options, agent SSH pour éviter de retaper la passphrase, tunnels (`-L 5432:db:5432` pour accéder à une base privée, `-D` proxy SOCKS), `scp`/`rsync` pour les fichiers, et bastion avec `ProxyJump`. Désactiver le login root et les mots de passe côté serveur.

### 33. Qu'est-ce que les cgroups et namespaces, et quel lien avec les conteneurs ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Les namespaces isolent la vue d'un processus (PID, réseau, montages, utilisateurs, hostname) ; les cgroups limitent et comptabilisent les ressources (CPU, mémoire, I/O). Un conteneur est un processus Linux ordinaire combinant les deux, plus un système de fichiers en couches. La JVM lit les limites cgroup pour dimensionner heap et threads (`-XX:+UseContainerSupport`, actif par défaut).

### 34. Comment fonctionnent les variables d'environnement et pourquoi servent-elles à la configuration ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** Des paires clé/valeur héritées par les processus enfants (`export VAR=x`, `env`, `printenv`). Elles permettent de configurer une même image pour plusieurs environnements sans modifier les fichiers (12-factor), sont injectées par Docker/Kubernetes (ConfigMaps, Secrets), et lues par Spring Boot avec le relaxed binding. Elles ne conviennent pas aux secrets très sensibles (visibles dans `/proc/<pid>/environ`) : préférer des fichiers montés.

### 35. Quelles sont les commandes de manipulation de texte indispensables ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `grep -rn` (chercher, `-E` regex étendues, `-v` inverser), `sed 's/a/b/g'` (substitution en flux, `-i` en place), `awk '{print $2}'` (colonnes, calculs), `cut -d, -f1`, `sort | uniq -c | sort -rn` (comptage d'occurrences), `tr`, `head`/`tail -f`, `wc -l`, `xargs`, `jq` pour le JSON. Combinées par pipes, elles remplacent beaucoup de scripts.

### 36. Comment fonctionnent les redirections et pipes ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `>` écrase, `>>` ajoute, `<` lit, `2>` redirige stderr, `2>&1` fusionne stderr dans stdout, `&>` les deux, `| tee file` affiche et écrit. Le pipe `|` connecte la sortie standard d'une commande à l'entrée de la suivante. `/dev/null` absorbe une sortie. Comprendre stdout vs stderr évite les logs perdus et les pipes qui « ne voient pas » les erreurs.

### 37. Quelles sont les bonnes pratiques pour écrire un script bash robuste ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** Commencer par `#!/usr/bin/env bash` et `set -euo pipefail` (arrêt à la première erreur, variable non définie interdite, échec dans un pipe propagé), toujours citer les variables (`"$var"`), utiliser `[[ ]]` pour les tests, des fonctions, `trap 'cleanup' EXIT` pour le nettoyage, `mktemp` pour les fichiers temporaires, et vérifier avec `shellcheck`. Au-delà de 100 lignes ou avec de la logique complexe, passer à Python.

### 38. Différence entre `$var`, `"$var"`, `${var:-default}`, `$(cmd)` et backticks ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** Sans guillemets, la valeur est découpée sur les espaces et les globs sont étendus (source de bugs avec les noms de fichiers). `${var:-default}` fournit une valeur par défaut, `${var:?msg}` échoue si vide, `${var%.txt}` retire un suffixe. `$(cmd)` capture la sortie d'une commande (imbriquable, préférable aux backticks). `$?` est le code de retour de la dernière commande, `$@` tous les arguments.

### 39. Comment gérer les arguments et options dans un script ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `$1`, `$2`… positionnels, `$#` nombre, `shift` pour consommer. `getopts "hv:o:"` pour les options courtes, ou une boucle `case "$1" in --output) ...` pour les longues. Toujours fournir `--help`, valider les arguments requis, et retourner un code de sortie non nul en cas d'erreur (`exit 1`) pour que la CI détecte l'échec.

### 40. Comment déboguer un script shell ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `bash -x script.sh` ou `set -x` (affiche chaque commande exécutée avec ses valeurs), `set -v`, `PS4='+ ${BASH_SOURCE}:${LINENO}: '` pour localiser, `echo` ciblés vers stderr (`>&2`), `shellcheck` pour les erreurs statiques, et tester les portions dans un shell interactif. Vérifier les fins de ligne CRLF (`file script.sh`, `dos2unix`) quand un script écrit sous Windows échoue mystérieusement.

### 41. Comment fonctionnent les tâches en arrière-plan, `nohup`, `screen`/`tmux` ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `cmd &` lance en arrière-plan (tué à la fermeture du shell), `nohup cmd &` survit à la déconnexion, `jobs`/`fg`/`bg` gèrent les tâches, `disown` détache. `tmux`/`screen` gardent des sessions terminal persistantes pour les travaux longs sur un serveur. Pour un vrai service, utiliser systemd plutôt que `nohup`.

### 42. Comment fonctionnent `cron` et les alternatives ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `crontab -e` planifie des commandes : `min heure jour mois jour-semaine commande` (`0 2 * * * backup.sh`), avec `MAILTO` pour les sorties et un environnement minimal (préciser `PATH`, chemins absolus). Alternatives : timers systemd (logs dans journald, dépendances), CronJobs Kubernetes, ou un planificateur applicatif. Rediriger les sorties dans un log et surveiller les échecs.

### 43. Comment utiliser `curl` efficacement pour tester une API ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `curl -v` (headers et handshake), `-X POST -H 'Content-Type: application/json' -d @body.json`, `-u user:pass` ou `-H 'Authorization: Bearer ...'`, `-o /dev/null -w '%{http_code} %{time_total}'` pour mesurer, `-L` suivre les redirections, `-k` ignorer TLS (test uniquement), `--resolve host:443:IP` pour tester un serveur avant bascule DNS, `-s` silencieux, et `| jq` pour lire le JSON.

### 44. Comment fonctionnent les codes de sortie et les opérateurs `&&`, `||`, `;` ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** Chaque commande renvoie 0 en succès, autre chose en erreur. `a && b` exécute b seulement si a réussit, `a || b` seulement si a échoue, `;` enchaîne sans condition. `if cmd; then` teste directement le code. Les scripts de CI et les `RUN` de Dockerfile dépendent de ces codes : une commande qui échoue silencieusement avec 0 est un piège classique (`cmd | tee` sans `pipefail`).

### 45. Comment trouver et traiter des fichiers en masse (`find`, `xargs`) ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `find . -name '*.log' -mtime +7 -size +10M` filtre par nom, âge, taille, type ; `-exec cmd {} +` ou `| xargs -0` (avec `-print0` pour les noms avec espaces) applique une commande en lot ; `-delete` supprime. `xargs -P 8` parallélise. Toujours tester avec `echo`/`ls` avant une suppression.

### 46. Comment capturer et analyser le trafic réseau (`tcpdump`, Wireshark) ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** `tcpdump -i eth0 port 5432 -w capture.pcap` capture les paquets (filtres BPF : `host`, `port`, `tcp`), analysés ensuite dans Wireshark (suivre un flux TCP, voir les retransmissions, le handshake TLS, les temps de réponse). Utile pour les problèmes de timeout, de MTU, de connexions réinitialisées, ou pour vérifier ce qu'une bibliothèque envoie réellement.

### 47. Qu'est-ce qu'un pare-feu, les security groups, et comment vérifier qu'un port est bloqué ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Un filtre de paquets par règles (source, destination, port, protocole) : `iptables`/`nftables` ou `ufw` sur l'hôte, security groups et NACL dans le cloud, NetworkPolicies dans Kubernetes. Un port « filtré » (`nmap`, `nc -zv` sans réponse, timeout) diffère d'un port « fermé » (refus immédiat, aucun service). Vérifier successivement le pare-feu de l'hôte, du réseau et l'écoute du service.

### 48. Comment fonctionnent les en-têtes `X-Forwarded-For` et pourquoi sont-ils sensibles ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Un reverse proxy remplace l'IP source par la sienne ; il ajoute `X-Forwarded-For: client, proxy1` pour transmettre l'IP d'origine, et `X-Forwarded-Proto`/`Host`. L'application ne doit faire confiance à ces headers que s'ils proviennent d'un proxy connu (`server.forward-headers-strategy` dans Spring Boot, `trusted proxies`), sinon un client peut usurper son IP pour contourner rate limiting ou allow-lists.

### 49. Qu'est-ce que le `Host` header, le SNI et le routage par nom ?
`🟠 Intermédiaire` · Sujet : **Réseau**

**Réponse :** Un même serveur/IP héberge plusieurs sites : HTTP utilise le header `Host` pour choisir la configuration ; TLS utilise SNI (Server Name Indication) pendant le handshake pour présenter le bon certificat avant que HTTP ne commence. Un `curl` avec `--resolve` ou une IP directe sans le bon `Host`/SNI renvoie souvent un certificat ou un site par défaut inattendu.

### 50. Comment analyser rapidement un serveur qui répond lentement ?
`🟠 Intermédiaire` · Sujet : **Linux**

**Réponse :** En 60 secondes : `uptime` (load), `dmesg -T | tail` (erreurs noyau, OOM), `vmstat 1` (CPU, run queue, swap), `mpstat -P ALL 1` (un cœur saturé ?), `pidstat 1` (quel processus), `iostat -xz 1` (disque saturé ?), `free -m`, `sar -n DEV 1` (réseau), `top`. Puis côté application : thread dump, pool de connexions, GC. Chercher d'abord la ressource saturée.

### 51. Quelles différences entre bash, sh, zsh, et pourquoi cela compte-t-il en CI et Docker ?
`🟠 Intermédiaire` · Sujet : **Shell**

**Réponse :** `sh` (dash sur Debian/Ubuntu, busybox sur Alpine) est POSIX minimal : pas de tableaux, `[[ ]]`, `source`, `pipefail`. Un script avec des bashismes échoue sous `#!/bin/sh` ou dans une image Alpine sans bash. Préciser `#!/usr/bin/env bash` et installer bash, ou écrire du POSIX pur (`shellcheck -s sh`). `zsh` (macOS par défaut) a d'autres différences pour l'usage interactif.
