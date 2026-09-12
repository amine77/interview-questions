# ☸️ Kubernetes & Helm

> Pods, Deployments, Services, Ingress, Helm charts, troubleshooting

**100 questions**

---

### 1. Différence entre un Pod et un Deployment ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** Un Pod est la plus petite unité déployable. Un Deployment gère le cycle de vie des Pods (réplication, mise à jour progressive, rollback).

### 2. Qu'est-ce qu'un chart Helm ?
`🟢 Débutant` · Sujet : **Helm**

**Réponse :** Package contenant les fichiers de définition Kubernetes (templates YAML, valeurs par défaut, métadonnées) pour un déploiement paramétrable et réutilisable.

### 3. Différence `ConfigMap` / `Secret` ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `ConfigMap` = données non sensibles en clair. `Secret` = données sensibles encodées en base64 (non chiffrées par défaut).

### 4. À quoi sert `values.yaml` ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** Définit les valeurs par défaut des paramètres configurables du chart, surchargeables via `--set` ou fichier custom.

### 5. Qu'est-ce qu'un Service K8s ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** Expose un ensemble de Pods sous une IP/DNS stable, assurant découverte et équilibrage de charge.

### 6. Commande d'installation d'un chart ?
`🟢 Débutant` · Sujet : **Helm**

**Réponse :** `helm install <nom-release> <chart>`.

### 7. Différence StatefulSet / Deployment ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** StatefulSet = identité stable + stockage persistant dédié. Deployment = Pods interchangeables sans état stable.

### 8. À quoi sert `helm rollback` ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** Revenir à une révision précédente d'une release en cas de problème.

### 9. Qu'est-ce qu'un namespace ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** Partitionnement logique d'un cluster, isolant des groupes de ressources.

### 10. Différence `install` / `upgrade` ?
`🟢 Débutant` · Sujet : **Helm**

**Réponse :** install crée une nouvelle release. upgrade met à jour une release existante.

### 11. Qu'est-ce qu'un Ingress ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Gère l'accès HTTP/HTTPS externe, règles de routage par hôte/chemin, avec contrôleur dédié.

### 12. Qu'est-ce qu'un hook Helm ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** Exécute des ressources K8s à des moments précis du cycle de vie d'une release.

### 13. Comment diagnostiquer un Pod en état CrashLoopBackOff ?
`🟠 Intermédiaire` · Sujet : **Kubernetes troubleshooting**

**Réponse :** En consultant les logs du conteneur (kubectl logs <pod> --previous), en décrivant le Pod (kubectl describe pod) pour voir les événements et codes de sortie, et en vérifiant les probes de santé (livenessProbe) et les limites de ressources (OOMKill).

### 14. Diagnostiquer un problème de connectivité réseau entre Pods ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Kubernetes**

**Réponse :** Vérifier NetworkPolicies, tester la résolution DNS interne, vérifier que les Services ciblent les bons labels, utiliser kubectl exec pour tests de connectivité.

### 15. Pod en état Pending, causes courantes ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Kubernetes**

**Réponse :** Ressources insuffisantes sur les nœuds, PVC non satisfait, règles d'affinité restrictives, absence de nœud correspondant aux tolérances.

### 16. État ImagePullBackOff et résolution ?
`🟢 Débutant` · Sujet : **Troubleshooting Kubernetes**

**Réponse :** Kubernetes n'arrive pas à télécharger l'image (nom incorrect, tag inexistant, credentials manquants). Résolu en vérifiant le nom et configurant un imagePullSecret.

### 17. Diagnostiquer une latence élevée en K8s ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Kubernetes**

**Réponse :** Vérifier limites CPU/mémoire (kubectl top), analyser métriques Prometheus, inspecter logs de timeout, utiliser tracing distribué.

### 18. Déboguer un ConfigMap/Secret mal monté ?
`🟠 Intermédiaire` · Sujet : **Troubleshooting Kubernetes**

**Réponse :** Vérifier le nom référencé, inspecter les événements du Pod, exécuter un shell pour vérifier le contenu effectif monté.

### 19. Quels sont les composants du control plane et des nœuds Kubernetes ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** Control plane : kube-apiserver (point d'entrée REST), etcd (stockage clé-valeur de l'état), kube-scheduler (placement des Pods), kube-controller-manager (boucles de réconciliation), cloud-controller-manager. Nœud : kubelet (exécute les Pods), kube-proxy (règles réseau des Services), container runtime (containerd, CRI-O).

### 20. Différence entre les types de Service `ClusterIP`, `NodePort`, `LoadBalancer` et `ExternalName` ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** `ClusterIP` (défaut) : IP virtuelle interne au cluster. `NodePort` : expose un port sur chaque nœud. `LoadBalancer` : provisionne un LB cloud externe. `ExternalName` : alias DNS vers un service externe. Un Service headless (`clusterIP: None`) retourne directement les IP des Pods (StatefulSets).

### 21. Qu'est-ce que `requests` et `limits`, et que se passe-t-il en cas de dépassement ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `requests` réserve des ressources pour le scheduling ; `limits` plafonne. Dépasser la limite CPU provoque du throttling ; dépasser la limite mémoire tue le conteneur (OOMKilled). Les combinaisons définissent la QoS class (Guaranteed, Burstable, BestEffort) qui détermine l'ordre d'éviction sous pression.

### 22. Quels sont les trois types de probes et leurs différences ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `livenessProbe` : redémarre le conteneur s'il est bloqué. `readinessProbe` : retire le Pod des endpoints du Service tant qu'il n'est pas prêt (ne redémarre pas). `startupProbe` : protège les applications à démarrage lent en désactivant les autres probes jusqu'au premier succès. Une liveness trop agressive cause des boucles de redémarrage.

### 23. Qu'est-ce que le Horizontal Pod Autoscaler et sur quelles métriques peut-il se baser ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Le HPA ajuste le nombre de réplicas d'un Deployment selon l'utilisation CPU/mémoire (metrics-server), des métriques custom (Prometheus Adapter : requêtes/s, lag Kafka) ou externes. KEDA étend ce mécanisme aux événements (taille de file SQS, topic Kafka) avec scale-to-zero.

### 24. Qu'est-ce que le Vertical Pod Autoscaler et le Cluster Autoscaler / Karpenter ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Le VPA recommande ou applique des `requests` adaptées à la consommation réelle. Le Cluster Autoscaler ajoute/retire des nœuds selon les Pods en attente. Karpenter (AWS, puis générique) provisionne des nœuds à la volée en choisissant le type d'instance optimal, plus rapide et plus économique que les node groups fixes.

### 25. Qu'est-ce qu'un DaemonSet et un Job/CronJob ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un DaemonSet garantit un Pod par nœud (agents de logs, monitoring, CNI). Un Job exécute une tâche jusqu'à complétion avec gestion des retries et du parallélisme ; un CronJob planifie des Jobs (batch, sauvegardes) avec `concurrencyPolicy` pour éviter les chevauchements.

### 26. Comment fonctionne le rolling update et que signifient `maxSurge` et `maxUnavailable` ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Le Deployment crée un nouveau ReplicaSet et bascule progressivement. `maxSurge` : nombre de Pods supplémentaires autorisés au-delà du désiré ; `maxUnavailable` : nombre de Pods pouvant être indisponibles. `maxSurge: 1, maxUnavailable: 0` garantit la capacité pleine. `kubectl rollout undo` revient au ReplicaSet précédent.

### 27. Qu'est-ce qu'un PersistentVolume, un PersistentVolumeClaim et une StorageClass ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un PV est un volume de stockage (disque EBS, NFS). Un PVC est la demande d'un Pod (taille, mode d'accès). Une StorageClass permet le provisionnement dynamique : le PVC référence la classe, et le CSI driver crée le PV. Les modes `ReadWriteOnce`/`ReadWriteMany` conditionnent le partage entre Pods.

### 28. Qu'est-ce qu'une NetworkPolicy ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un pare-feu au niveau Pod : par défaut tout trafic est autorisé ; une NetworkPolicy sélectionne des Pods et définit les flux entrants/sortants permis (labels, namespaces, CIDR, ports). Elle nécessite un CNI qui la supporte (Calico, Cilium). Bonne pratique : deny-all par namespace puis autorisations explicites.

### 29. Qu'est-ce que RBAC dans Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Role/ClusterRole définissent des permissions (verbs sur des ressources), RoleBinding/ClusterRoleBinding les attribuent à des utilisateurs, groupes ou ServiceAccounts. Chaque Pod tourne avec un ServiceAccount ; lui donner le minimum et désactiver `automountServiceAccountToken` si l'application n'appelle pas l'API.

### 30. Qu'est-ce qu'un `SecurityContext` et les bonnes pratiques de durcissement d'un Pod ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `runAsNonRoot: true`, `readOnlyRootFilesystem: true`, `allowPrivilegeEscalation: false`, suppression des capabilities (`drop: [ALL]`), `seccompProfile: RuntimeDefault`. Les Pod Security Standards (baseline/restricted) appliqués par le Pod Security Admission au niveau namespace imposent ces règles.

### 31. Qu'est-ce qu'un init container et un sidecar ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un init container s'exécute avant les conteneurs principaux (attendre une base, migrer un schéma, télécharger une configuration). Un sidecar tourne à côté du conteneur principal (proxy mesh, agent de logs). Depuis Kubernetes 1.29, les sidecars natifs (`restartPolicy: Always` sur un init container) démarrent avant et s'arrêtent après l'application.

### 32. Comment placer les Pods avec `nodeSelector`, affinity, taints et tolerations ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `nodeSelector`/`nodeAffinity` attirent les Pods vers des nœuds étiquetés (GPU, zone). `podAffinity`/`podAntiAffinity` rapprochent ou séparent des Pods (répartir les réplicas sur plusieurs nœuds). Les taints repoussent les Pods d'un nœud sauf s'ils ont la toleration correspondante (nœuds dédiés, Spot). `topologySpreadConstraints` équilibre entre zones.

### 33. Qu'est-ce qu'un PodDisruptionBudget ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Une garantie du nombre minimal de Pods disponibles (`minAvailable`) ou maximal indisponibles pendant les perturbations volontaires (drain de nœud, mise à jour du cluster). Sans PDB, une maintenance peut retirer tous les réplicas simultanément.

### 34. Quelles sont les principales étapes pour diagnostiquer un problème avec `kubectl` ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `kubectl get pods -o wide` (état, nœud, restarts), `kubectl describe pod` (events : scheduling, image, probes), `kubectl logs -f --previous` (logs du conteneur précédent après crash), `kubectl exec -it` pour inspecter, `kubectl get events --sort-by=.lastTimestamp`, `kubectl top` pour la consommation, et `kubectl debug` pour attacher un conteneur éphémère d'outillage.

### 35. Comment fonctionne le DNS interne de Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** CoreDNS résout `service.namespace.svc.cluster.local` vers le ClusterIP, et pour les headless Services vers les IP des Pods. Depuis un Pod, `service` seul fonctionne dans le même namespace grâce aux search domains. Les problèmes de résolution se diagnostiquent avec `nslookup` depuis un Pod de debug et les logs CoreDNS.

### 36. Qu'est-ce qu'un Ingress Controller et la Gateway API ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** L'Ingress est une ressource déclarative ; un controller (NGINX, Traefik, AWS Load Balancer Controller) la traduit en configuration de proxy. La Gateway API est son successeur : rôles séparés (GatewayClass, Gateway, HTTPRoute), routage avancé (header, poids, TCP/gRPC) et portabilité entre implémentations sans annotations propriétaires.

### 37. Qu'est-ce qu'un Operator et une CustomResourceDefinition ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Une CRD étend l'API Kubernetes avec un nouveau type (ex : `KafkaCluster`). Un Operator est un controller qui réconcilie ces ressources en encodant l'expertise opérationnelle (déploiement, sauvegardes, failover). Exemples : Strimzi (Kafka), CloudNativePG, Prometheus Operator. Le pattern reproduit le modèle déclaratif natif.

### 38. Comment gérer les secrets de façon sécurisée dans Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Les Secrets sont seulement encodés en base64 : activer le chiffrement at-rest d'etcd, restreindre le RBAC, et éviter de les commiter en clair. Approches GitOps : Sealed Secrets (chiffrés par le cluster), SOPS, ou External Secrets Operator qui synchronise depuis Vault/AWS Secrets Manager. Le CSI Secrets Store monte les secrets sans les stocker dans etcd.

### 39. Qu'est-ce qu'un admission controller et policy engine (Kyverno, OPA Gatekeeper) ?
`🔴 Avancé` · Sujet : **Kubernetes**

**Réponse :** Les admission webhooks (validating/mutating) interceptent chaque requête à l'API avant sa persistance. Kyverno et Gatekeeper permettent de définir des politiques : interdire `latest`, imposer les labels et les limites, refuser les images non signées, injecter des sidecars. C'est le mécanisme de « policy as code » du cluster.

### 40. Qu'est-ce qu'un `ResourceQuota` et un `LimitRange` ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `ResourceQuota` plafonne la consommation totale d'un namespace (CPU, mémoire, nombre de Pods, PVC). `LimitRange` définit des valeurs par défaut et des bornes pour chaque conteneur, ce qui évite les Pods sans `requests`. Ensemble ils permettent la multi-location d'un cluster partagé.

### 41. Comment fonctionne le graceful shutdown d'un Pod ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** À la suppression, le Pod passe en `Terminating`, est retiré des endpoints, le `preStop` hook s'exécute, puis SIGTERM est envoyé. L'application a `terminationGracePeriodSeconds` (30 s par défaut) pour finir les requêtes en cours avant SIGKILL. Un `preStop` avec `sleep 5` laisse le temps aux load balancers de propager le retrait.

### 42. Qu'est-ce que la topologie de cluster multi-tenant et les stratégies d'isolation ?
`🔴 Avancé` · Sujet : **Kubernetes**

**Réponse :** Isolation par namespace (RBAC, quotas, NetworkPolicies, Pod Security), par nœuds dédiés (taints), ou par clusters séparés (isolation la plus forte, coût plus élevé). Les clusters virtuels (vCluster) offrent un compromis. Le choix dépend de la confiance entre locataires et des exigences de conformité.

### 43. Comment écrire un template Helm avec conditions, boucles et helpers ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** Les templates utilisent Go templates : `{{ if .Values.ingress.enabled }}`, `{{ range .Values.env }}`, `{{ include "chart.fullname" . }}` avec des helpers définis dans `_helpers.tpl`, et les fonctions Sprig (`default`, `toYaml | nindent 4`, `quote`). `helm template` et `helm lint` valident le rendu avant installation.

### 44. Qu'est-ce qu'une dépendance de chart et `Chart.yaml` ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** `Chart.yaml` décrit le chart (nom, version, `appVersion`) et sa section `dependencies` (sous-charts comme PostgreSQL de Bitnami, avec `condition` pour les activer). `helm dependency update` télécharge les charts dans `charts/`. Les values des sous-charts se surchargent par leur nom (`postgresql.auth.password`).

### 45. Comment tester un chart Helm ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** `helm lint` (structure), `helm template --debug` (rendu), `helm install --dry-run`, `helm test` (Pods de test annotés `helm.sh/hook: test`), et des tests unitaires de templates avec le plugin `helm-unittest`. Chart-testing (`ct`) automatise lint et install en CI sur un cluster kind.

### 46. Qu'est-ce qu'un OCI registry pour Helm et comment publier un chart ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** Depuis Helm 3.8, les charts se stockent dans des registries OCI comme les images Docker : `helm package` puis `helm push chart-1.0.0.tgz oci://registry/charts`, et `helm install app oci://registry/charts/app --version 1.0.0`. Cela unifie l'hébergement, l'authentification et la signature (cosign) des images et des charts.

### 47. Différence entre `helm upgrade --install`, `--atomic` et `--wait` ?
`🟠 Intermédiaire` · Sujet : **Helm**

**Réponse :** `--install` installe si la release n'existe pas (idempotence en CI). `--wait` attend que les ressources soient prêtes avant de marquer la release réussie. `--atomic` combine `--wait` et un rollback automatique en cas d'échec, évitant de laisser une release en état `failed`.

### 48. Comment diagnostiquer un Pod OOMKilled et un conteneur qui redémarre sans logs ?
`🟠 Intermédiaire` · Sujet : **Kubernetes troubleshooting**

**Réponse :** `kubectl describe pod` montre `Last State: Terminated, Reason: OOMKilled`. Comparer la limite mémoire à la consommation réelle (`kubectl top`, métriques Prometheus), vérifier la configuration JVM (`MaxRAMPercentage`) et la mémoire hors heap. Sans logs, utiliser `--previous`, augmenter le niveau de log au démarrage, ou un `startupProbe` plus tolérant si l'app est tuée avant d'écrire.

### 49. Comment diagnostiquer un Service qui ne route pas vers les Pods ?
`🟠 Intermédiaire` · Sujet : **Kubernetes troubleshooting**

**Réponse :** Vérifier que le `selector` du Service correspond aux labels des Pods (`kubectl get endpoints svc` doit lister des IP), que le `targetPort` correspond au port du conteneur, que les Pods sont `Ready` (readiness probe), et qu'aucune NetworkPolicy ne bloque. Tester avec `kubectl port-forward` directement sur un Pod pour isoler le problème.

### 50. Comment diagnostiquer un nœud `NotReady` ou sous pression ?
`🔴 Avancé` · Sujet : **Troubleshooting Kubernetes**

**Réponse :** `kubectl describe node` affiche les conditions (`MemoryPressure`, `DiskPressure`, `PIDPressure`) et les events. Causes : kubelet arrêté, disque plein (images, logs), réseau CNI en panne, certificats expirés. Actions : `kubectl cordon`/`drain` pour évacuer, inspection via SSH (`journalctl -u kubelet`), nettoyage d'images (`crictl rmi --prune`).

### 51. Que fait `kubectl apply` par rapport à `create` et `replace`, et qu'est-ce que le Server-Side Apply ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** `create` crée (échec si existant), `replace` remplace entièrement, `apply` calcule un diff déclaratif et fusionne (three-way merge via l'annotation `last-applied-configuration`). Le Server-Side Apply (`--server-side`) déplace cette logique dans l'API server avec suivi par « field manager », résolvant les conflits entre outils (Helm, contrôleurs, kubectl) champ par champ.

### 52. Comment fonctionne le cycle de vie d'une requête `kubectl` jusqu'au Pod qui tourne ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** `kubectl` envoie une requête REST à l'API server (authentification, autorisation RBAC, admission), l'objet est stocké dans etcd ; les contrôleurs (Deployment → ReplicaSet → Pods) réconcilient l'état désiré ; le scheduler assigne un nœud ; le kubelet du nœud tire l'image et lance les conteneurs via le runtime (containerd) ; kube-proxy/CNI configurent le réseau. Tout est asynchrone et basé sur des boucles de réconciliation.

### 53. Quelles commandes `kubectl` de diagnostic faut-il maîtriser ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** `get pods -o wide`, `describe pod` (événements en bas), `logs -f --previous -c container`, `exec -it -- sh`, `get events --sort-by=.lastTimestamp`, `top pods/nodes`, `rollout status|history|undo`, `port-forward`, `debug` (conteneur éphémère), `explain` (documentation des champs), `-o yaml`/`jsonpath`, `--field-selector`, `kubectl auth can-i`. `k9s` et `stern` accélèrent le quotidien.

### 54. Qu'est-ce qu'un label, un selector et une annotation ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** Labels : paires clé/valeur identifiant et sélectionnant des objets (Service → Pods, `kubectl get -l app=api`), avec des conventions recommandées (`app.kubernetes.io/name`, `version`). Annotations : métadonnées non sélectionnables pour les outils (ingress class, Prometheus scrape, checksums de config). Les selectors des Deployments sont immuables : les planifier dès le départ.

### 55. Comment passer de la configuration à une application (env, fichiers, arguments) ?
`🟢 Débutant` · Sujet : **Kubernetes**

**Réponse :** `env` littéral, `envFrom` un ConfigMap/Secret entier, `valueFrom` (`configMapKeyRef`, `secretKeyRef`, `fieldRef` pour le nom du Pod, `resourceFieldRef` pour les limites), volumes montés (fichiers rechargés automatiquement sauf `subPath`), `args`/`command`. Les variables d'environnement ne se mettent pas à jour sans redémarrage : ajouter un checksum de ConfigMap en annotation du Pod template (Helm) pour déclencher un rollout.

### 56. Comment fonctionnent les Endpoints/EndpointSlices et la relation Service ↔ Pods ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un Service sélectionne des Pods par label ; le contrôleur d'endpoints crée des EndpointSlices listant les IPs des Pods **ready**. kube-proxy (iptables/IPVS) ou le CNI (eBPF avec Cilium) programme la répartition. Un Service sans endpoints (selector erroné, Pods non ready, port nommé incorrect) est la cause n°1 des « connection refused » ; `kubectl get endpointslices` le révèle.

### 57. Qu'est-ce qu'un Service headless et quand l'utiliser ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `clusterIP: None` : le DNS renvoie directement les IPs des Pods (enregistrements A multiples, et un nom stable par Pod avec un StatefulSet : `pod-0.svc`). Utilisé pour les bases distribuées, Kafka, le client-side load balancing (gRPC) et la découverte des pairs. Pas de VIP ni de répartition par kube-proxy.

### 58. Comment fonctionnent `externalTrafficPolicy`, `sessionAffinity` et le load balancing gRPC ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `externalTrafficPolicy: Local` préserve l'IP source et évite un saut supplémentaire (Pods uniquement sur les nœuds qui les hébergent). `sessionAffinity: ClientIP` colle un client à un Pod (à éviter, préférer un état externalisé). gRPC (HTTP/2, connexions longues) n'est pas réparti par un Service L4 : utiliser un Service headless + load balancing côté client, ou un proxy L7 (Envoy, service mesh, Ingress gRPC-aware).

### 59. Comment configurer un Ingress avec TLS, réécriture et plusieurs backends ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `ingressClassName`, `rules` par host/path (`pathType: Prefix|Exact`), `tls` avec un Secret de type `kubernetes.io/tls` (émis par cert-manager via `ClusterIssuer` Let's Encrypt et l'annotation `cert-manager.io/cluster-issuer`), annotations spécifiques au contrôleur (NGINX : `rewrite-target`, timeouts, body size, rate limit, affinité). La Gateway API standardise ces fonctionnalités (`HTTPRoute` avec filtres) sans annotations propriétaires.

### 60. Qu'est-ce que la Gateway API et pourquoi remplace-t-elle progressivement Ingress ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Des ressources standard (`GatewayClass`, `Gateway`, `HTTPRoute`, `GRPCRoute`, `TCPRoute`) séparant les rôles (infra : Gateway ; développeurs : Routes dans leur namespace), avec routage par header, pondération (canary), réécritures, redirections, timeouts et TLS exprimés nativement, sans annotations propriétaires. Implémentée par NGINX Gateway Fabric, Envoy Gateway, Istio, Cilium, cloud providers. Ingress est gelé fonctionnellement.

### 61. Comment fonctionnent les NetworkPolicies avancées (egress, DNS, namespaces) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Par défaut tout est ouvert ; une politique `podSelector` avec `policyTypes: [Ingress, Egress]` passe en deny-by-default pour ces Pods. Autoriser explicitement le DNS vers kube-system (`udp/53`), les dépendances par `namespaceSelector` + `podSelector` (combinés dans un même élément = ET), et les IPs externes par `ipBlock`. Cilium ajoute des politiques L7 (FQDN, méthodes HTTP). Tester avec `kubectl exec ... nc -zv`.

### 62. Qu'est-ce qu'un service mesh (Istio, Linkerd, Cilium) et quand en avoir besoin ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un plan de données (sidecars Envoy, ou mode ambient/eBPF sans sidecar) qui apporte mTLS automatique entre services, observabilité uniforme (métriques dorées, traces), résilience (retries, timeouts, circuit breaking), routage fin (canary, mirroring) et autorisation par identité. Coût : complexité, latence, ressources. À adopter quand ces besoins concernent des dizaines de services et plusieurs équipes ; sinon des bibliothèques applicatives suffisent.

### 63. Comment fonctionnent les requests CPU vs limits et les classes de QoS ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Les `requests` servent au scheduling et à la garantie (part de CPU pondérée, mémoire réservée) ; les `limits` plafonnent (CPU throttlé par CFS, mémoire → OOMKill). QoS : `Guaranteed` (requests = limits sur tous les conteneurs), `Burstable`, `BestEffort` (aucune) ; en cas de pression mémoire sur le nœud, l'éviction commence par BestEffort. Recommandation courante : requests mémoire = limits, requests CPU réalistes, limites CPU généreuses ou absentes.

### 64. Qu'est-ce que le scheduler et comment fonctionnent taints/tolerations et topology spread ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Le scheduler filtre les nœuds (ressources, affinités, taints) puis les note (répartition, images présentes). Taints (`NoSchedule`, `NoExecute`) repoussent les Pods sans toleration correspondante (nœuds GPU, spot, dédiés). `topologySpreadConstraints` répartit les réplicas sur les zones/nœuds (`maxSkew`, `whenUnsatisfiable`) pour la haute disponibilité, plus fin que `podAntiAffinity`.

### 65. Comment fonctionne le Cluster Autoscaler et Karpenter ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Le Cluster Autoscaler ajoute des nœuds quand des Pods sont Pending faute de ressources et retire les nœuds sous-utilisés, par node groups prédéfinis. Karpenter (AWS, Azure) provisionne directement des instances adaptées aux Pods en attente (taille, architecture, spot), plus rapide et moins coûteux, avec consolidation continue. Les deux dépendent de requests correctes et de PodDisruptionBudgets.

### 66. Qu'est-ce que KEDA et le scaling basé sur des événements ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Kubernetes Event-Driven Autoscaling étend le HPA avec des « scalers » sur des sources externes : lag Kafka, longueur d'une file SQS/RabbitMQ, métriques Prometheus, cron, et permet le scale-to-zero. Un `ScaledObject` définit la cible et les seuils ; idéal pour les consommateurs de messages et les workers batch dont la charge ne se voit pas sur le CPU.

### 67. Comment fonctionnent les stratégies de déploiement avancées (blue/green, canary) sur Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Nativement : rolling update seulement. Blue/green : deux Deployments et bascule du selector du Service. Canary : deux Deployments derrière un même Service avec un ratio de réplicas (grossier), ou pondération via Ingress/Gateway API/service mesh (précis). Argo Rollouts et Flagger automatisent l'analyse (métriques Prometheus) et la promotion/rollback progressifs.

### 68. Comment fonctionne un StatefulSet en détail (identité, volumes, mise à jour) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Pods nommés `name-0..N` avec DNS stable (Service headless), création et suppression ordonnées (`podManagementPolicy`), `volumeClaimTemplates` créant un PVC par Pod conservé après suppression du Pod, mise à jour `RollingUpdate` en ordre inverse avec `partition` pour les canaris. Utilisé pour les bases, Kafka, Elasticsearch ; les opérateurs les encapsulent souvent.

### 69. Comment gérer le stockage : StorageClass, provisioning dynamique, modes d'accès et snapshots ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Une `StorageClass` (CSI driver, paramètres, `reclaimPolicy`, `volumeBindingMode: WaitForFirstConsumer` pour respecter la zone) provisionne dynamiquement les PV à la création d'un PVC. Modes : `ReadWriteOnce` (disque bloc, un nœud), `ReadWriteMany` (NFS/EFS), `ReadWriteOncePod`. `VolumeSnapshot` sauvegarde via CSI ; l'expansion en ligne est possible si `allowVolumeExpansion`. Ne pas stocker de données critiques sur `emptyDir`/`hostPath`.

### 70. Comment sauvegarder et restaurer un cluster et ses données (Velero, etcd) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Velero sauvegarde les objets Kubernetes (par namespace/label) et les volumes (snapshots CSI ou restic/Kopia) vers un object storage, avec planification et restauration sélective, y compris vers un autre cluster (migration). Le control plane managé sauvegarde etcd ; en auto-géré, `etcdctl snapshot save` régulièrement. Tester les restaurations.

### 71. Comment fonctionne le RBAC en détail (Role, ClusterRole, binding, ServiceAccount, agrégation) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `Role` (namespace) / `ClusterRole` (cluster ou réutilisable) listent des règles (`apiGroups`, `resources`, `verbs`) ; les `RoleBinding`/`ClusterRoleBinding` les lient à des utilisateurs, groupes ou ServiceAccounts. Un `ClusterRole` peut être lié par un `RoleBinding` pour limiter au namespace. `aggregationRule` compose des rôles. Principe du moindre privilège, `kubectl auth can-i --as`, et audit des bindings `cluster-admin`.

### 72. Comment un Pod s'authentifie-t-il auprès de l'API ou du cloud (ServiceAccount tokens, Workload Identity) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Chaque Pod reçoit un token de ServiceAccount projeté (JWT à durée limitée, audience, rotation automatique) monté dans `/var/run/secrets/kubernetes.io/serviceaccount`. Pour le cloud, IRSA/Pod Identity (AWS), Workload Identity (GCP/Azure) fédèrent ce token OIDC vers un rôle cloud : aucune clé stockée. Désactiver `automountServiceAccountToken` si le Pod n'en a pas besoin.

### 73. Qu'est-ce que les Pod Security Standards et comment les appliquer ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Trois niveaux (`privileged`, `baseline`, `restricted`) définis par Kubernetes et appliqués par le Pod Security Admission via des labels de namespace (`pod-security.kubernetes.io/enforce: restricted`, plus `audit`/`warn`). `restricted` exige non-root, `allowPrivilegeEscalation: false`, capabilities droppées, seccomp `RuntimeDefault`, pas de hostPath. Pour des règles personnalisées, Kyverno ou Gatekeeper.

### 74. Comment durcir la sécurité d'un cluster (checklist) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Images minimales signées et scannées, registre privé avec admission (Kyverno `verifyImages`), PSS restricted, NetworkPolicies deny-by-default, RBAC minimal et audit logs activés, secrets chiffrés au repos (KMS) et gérés par External Secrets/Vault, pas d'accès public à l'API server, mises à jour régulières de version, runtime security (Falco), CIS benchmark (kube-bench), et limitation des `exec` en production.

### 75. Comment fonctionnent les webhooks d'admission (mutating/validating) et les CEL ValidatingAdmissionPolicy ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un `MutatingWebhookConfiguration` appelle un service qui modifie les objets (injection de sidecars, valeurs par défaut) ; un `ValidatingWebhookConfiguration` accepte ou refuse. Risques : latence, indisponibilité bloquant le cluster (`failurePolicy`), à exclure kube-system. Depuis 1.30, `ValidatingAdmissionPolicy` en CEL exprime des règles simples directement dans l'API server sans webhook.

### 76. Comment écrire un Operator (controller-runtime, Kubebuilder, Java Operator SDK) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Définir une CRD (schéma OpenAPI, versions, status subresource), implémenter une boucle `Reconcile(request)` idempotente qui lit l'état désiré et converge l'état réel (crée/met à jour les ressources enfants avec owner references), gère les finalizers pour le nettoyage, met à jour `status` et des conditions, et watche les ressources dépendantes. Tester avec envtest ; le Java Operator SDK offre l'équivalent pour les équipes Java.

### 77. Qu'est-ce que Kustomize et comment le comparer à Helm ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Kustomize (intégré à `kubectl -k`) superpose des overlays (patches stratégiques, JSON patch, `configMapGenerator`, images, namespaces) sur une base YAML sans templating : simple, lisible, sans logique. Helm apporte templating, packaging, versioning, dépendances et hooks : mieux pour distribuer des applications tierces et des charts paramétrables. Souvent combinés : Helm pour les charts externes, Kustomize pour les overlays d'environnement (ou `helm template | kustomize`).

### 78. Comment fonctionne GitOps avec Argo CD ou Flux sur Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Un contrôleur dans le cluster synchronise en continu l'état désiré depuis Git (Helm, Kustomize, YAML) et signale ou corrige les dérives ; les déploiements sont des commits/PR revus, avec rollback par revert. Argo CD : UI, `Application`/`ApplicationSet` multi-clusters, sync waves et hooks, RBAC par projet. Flux : plus modulaire (sources, kustomizations, HelmReleases, image automation). Les secrets passent par SOPS ou External Secrets.

### 79. Qu'est-ce qu'un `ApplicationSet` et les sync waves d'Argo CD ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `ApplicationSet` génère des Applications à partir de générateurs (liste de clusters, répertoires Git, matrices) pour déployer la même application sur N environnements/clusters sans duplication. Les sync waves (`argocd.argoproj.io/sync-wave`) ordonnent le déploiement (CRD et namespaces d'abord, base avant application) ; les hooks `PreSync`/`PostSync` exécutent migrations et tests.

### 80. Comment gérer les migrations de base de données lors d'un déploiement Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Éviter de lancer les migrations dans chaque réplica au démarrage (courses, rollouts bloqués) : un `Job` dédié exécuté avant le rollout (Helm hook `pre-upgrade`, Argo `PreSync`, ou étape de pipeline), migrations rétrocompatibles (expand/contract) pour permettre la coexistence des versions pendant le rolling update, et l'application démarre avec `ddl-auto=validate`. Un init container avec verrou est une alternative pour les petits déploiements.

### 81. Comment fonctionnent les Jobs et CronJobs en détail (parallélisme, backoff, concurrence) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `Job` : `completions`, `parallelism`, `backoffLimit`, `activeDeadlineSeconds`, `ttlSecondsAfterFinished`, mode `Indexed` pour les partitions, `podFailurePolicy` (1.31) pour distinguer erreurs réessayables. `CronJob` : `schedule` (fuseau via `timeZone`), `concurrencyPolicy: Forbid|Replace|Allow`, `startingDeadlineSeconds`, historiques `successfulJobsHistoryLimit`. Prévoir l'idempotence : un job peut s'exécuter deux fois.

### 82. Comment déboguer un conteneur sans shell ni outils (images distroless) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `kubectl debug -it pod --image=busybox --target=app --share-processes` attache un conteneur éphémère avec des outils dans le même namespace de processus (voir `/proc/<pid>/root` pour le système de fichiers de l'app) ; `kubectl debug node/` pour le nœud ; `kubectl cp` pour extraire des fichiers ; JFR/thread dump via `jcmd` depuis le conteneur éphémère si la JVM est visible. Prévoir cette procédure dans les runbooks.

### 83. Comment collecter logs, métriques et traces d'un cluster ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Logs : les Pods écrivent sur stdout ; un DaemonSet (Fluent Bit, Vector, Promtail/Alloy) collecte vers Loki/Elasticsearch/cloud. Métriques : kube-state-metrics + node-exporter + cAdvisor scrapés par Prometheus (kube-prometheus-stack), annotations ou `ServiceMonitor`/`PodMonitor` pour les applications. Traces : OpenTelemetry Collector (DaemonSet ou Deployment) vers Tempo/Jaeger. Tableaux de bord Grafana par namespace et alertes sur la saturation.

### 84. Qu'est-ce que le Descheduler et pourquoi les Pods ne se rééquilibrent-ils pas seuls ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Le scheduler ne décide qu'au placement initial : après un ajout de nœuds ou une panne, la répartition peut rester déséquilibrée. Le Descheduler évince périodiquement les Pods violant des politiques (nœuds surchargés, affinités non respectées, Pods trop anciens, duplicatas) pour qu'ils soient replanifiés, en respectant les PodDisruptionBudgets.

### 85. Comment gérer les mises à jour de version du cluster (control plane, nœuds) sans interruption ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Lire les notes de version (APIs supprimées : `kubectl deprecations`/Pluto), mettre à jour le control plane d'une version mineure à la fois, puis les nœuds par rotation (cordon, drain en respectant les PDB, remplacement des nœuds sur cloud managé), vérifier les add-ons (CNI, CSI, ingress, cert-manager) compatibles, et tester en préproduction. Les PDB et plusieurs réplicas répartis sont indispensables pour que le drain soit indolore.

### 86. Comment fonctionne `kubectl drain`, `cordon` et l'éviction ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `cordon` marque un nœud unschedulable ; `drain` évince les Pods (respect des PDB, `--ignore-daemonsets`, `--delete-emptydir-data`) en utilisant l'API d'éviction, qui refuse si un PDB serait violé (le drain réessaie). Les Pods non gérés par un contrôleur sont perdus. Après maintenance, `uncordon`. Les nœuds spot et les mises à jour automatiques utilisent le même mécanisme.

### 87. Comment fonctionne le multi-cluster et quand le choisir ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Motivations : isolation forte (prod/non-prod, régions, réglementaire), limite de taille, blast radius. Approches : clusters indépendants déployés par GitOps (ApplicationSet), fédération de services (Istio multi-cluster, Cilium ClusterMesh, Submariner), routage global par DNS/CDN. Coût : duplication des add-ons et de l'exploitation ; un cluster par environnement avec namespaces est souvent suffisant au départ.

### 88. Comment optimiser les coûts d'un cluster Kubernetes ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Right-sizing des requests (VPA en recommandation, Goldilocks, Kubecost/OpenCost pour le coût par namespace), autoscaling nœuds (Karpenter avec consolidation) et Pods (HPA/KEDA, scale-to-zero hors heures), instances spot pour les workloads tolérants, ARM, images légères, limites de ressources par namespace (ResourceQuota), suppression des ressources orphelines (PV, load balancers), et rétention des logs maîtrisée.

### 89. Comment configurer correctement une application Java/Spring pour Kubernetes (checklist) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Readiness/liveness séparées (Actuator groups), `startupProbe` pour le temps de démarrage JVM, graceful shutdown + `preStop` sleep, `terminationGracePeriodSeconds` cohérent, `MaxRAMPercentage` avec limites mémoire, requests CPU suffisantes pour le démarrage (ou pas de limite CPU), logs JSON sur stdout, configuration par env/ConfigMap, secrets montés, utilisateur non-root, image en couches, PDB, HPA sur une métrique pertinente, et labels standard.

### 90. Pourquoi une JVM démarre-t-elle lentement dans Kubernetes et comment corriger ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Limites CPU basses (throttling pendant le JIT et l'initialisation Spring), `requests` inférieures aux besoins de démarrage, image lourde à tirer, probes liveness trop agressives qui redémarrent le Pod en boucle avant la fin du démarrage. Corrections : `startupProbe` généreuse, limites CPU absentes ou élevées (le burst au démarrage est bénéfique), CDS/AOT/Native, images en couches, pull policy et cache d'images sur les nœuds.

### 91. Comment fonctionnent les Ephemeral Volumes, `projected` volumes et les Secrets immuables ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `emptyDir` (mémoire avec `medium: Memory`, ou disque, vie du Pod), generic ephemeral volumes (PVC créé et supprimé avec le Pod), `projected` (combine ConfigMap, Secret, token de ServiceAccount, downward API dans un même répertoire). `immutable: true` sur un ConfigMap/Secret empêche les modifications accidentelles et réduit la charge sur l'API server (pas de watch).

### 92. Comment gérer les dépendances au démarrage (attendre une base, Kafka) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Ne pas dépendre de l'ordre de déploiement : l'application réessaie ses connexions (Spring : retries de connexion Kafka natifs, HikariCP `initializationFailTimeout`), readiness `false` tant que la dépendance manque, init container `wait-for` pour les cas simples, et probes de la dépendance elle-même. Les redémarrages de Pod pendant l'attente sont normaux (CrashLoopBackOff transitoire) mais mieux évités par des retries applicatifs.

### 93. Qu'est-ce que l'API Priority and Fairness, et les `PriorityClass` de Pods ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `PriorityClass` donne une priorité aux Pods : le scheduler peut préempter (évincer) des Pods moins prioritaires pour placer les critiques (`system-cluster-critical` pour les add-ons). À utiliser avec parcimonie (workloads critiques vs batch). API Priority and Fairness protège l'API server en répartissant les requêtes des clients (contrôleurs bavards) par niveaux de priorité et files.

### 94. Comment exposer une application avec un LoadBalancer cloud, et quels sont les coûts et alternatives ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `type: LoadBalancer` crée un équilibreur par Service (NLB/ALB, coût par instance) ; préférer un seul Ingress/Gateway controller derrière un LoadBalancer unique, avec le routage L7 par host/path. Annotations pour NLB interne, certificats ACM, `externalTrafficPolicy`. En on-premise : MetalLB ou Cilium LB IPAM pour attribuer des IPs.

### 95. Comment fonctionne le réseau des Pods (CNI) et que changent Cilium/eBPF ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Chaque Pod a une IP routable dans le cluster (modèle plat), fournie par le plugin CNI (Calico, Cilium, AWS VPC CNI, Flannel) via overlay (VXLAN) ou routage natif. Cilium utilise eBPF pour remplacer kube-proxy (plus performant, pas d'iptables), appliquer des politiques L3-L7, observer les flux (Hubble) et faire du mesh sans sidecar. Le choix du CNI conditionne NetworkPolicies et performances.

### 96. Comment tester un manifeste ou un chart avant déploiement (validation, policies, conformance) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** `kubectl apply --dry-run=server`, `kubeconform`/`kubectl-validate` contre les schémas, `helm lint`/`helm template` + `kubeconform`, tests de politiques Kyverno/Conftest (OPA) en CI (pas de `latest`, requests obligatoires, non-root), `helm unittest`, déploiement sur un cluster éphémère (kind, k3d) avec tests de fumée, et `polaris`/`kube-score` pour les bonnes pratiques.

### 97. Que sont kind, k3s/k3d, minikube et comment développer localement ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** kind (Kubernetes dans Docker, rapide, idéal en CI), k3d (k3s dans Docker, léger, avec load balancer), minikube (VM ou Docker, add-ons). Workflow local : `skaffold`/`tilt`/`devspace` pour reconstruire et redéployer en continu, `telepresence`/`mirrord` pour exécuter un service localement connecté au cluster distant, et Docker Compose pour les dépendances quand Kubernetes n'est pas nécessaire au développement.

### 98. Comment gérer les secrets avec External Secrets Operator et Sealed Secrets ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** External Secrets Operator synchronise des secrets depuis Vault/AWS Secrets Manager/GCP/Azure vers des Secrets Kubernetes via `ExternalSecret` + `SecretStore` (rotation automatique, source de vérité externe). Sealed Secrets chiffre un secret avec la clé publique du cluster pour le committer dans Git (déchiffré uniquement par le contrôleur). SOPS + KMS est l'alternative côté Git. Ne jamais committer des Secrets en base64 clair.

### 99. Comment surveiller et alerter sur la santé des workloads (règles clés) ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Pods en CrashLoopBackOff/Pending/OOMKilled (kube-state-metrics), réplicas disponibles < désirés, rollouts bloqués, throttling CPU élevé, utilisation mémoire proche des limites, PVC presque pleins, certificats proches de l'expiration (cert-manager), nœuds NotReady ou sous pression, erreurs 5xx et latence de l'Ingress, lag des consommateurs. Utiliser les règles de kube-prometheus-stack comme base et les adapter.

### 100. Comment fonctionne le Downward API et à quoi sert-il ?
`🟠 Intermédiaire` · Sujet : **Kubernetes**

**Réponse :** Il expose au conteneur des informations sur le Pod (nom, namespace, labels, annotations, IP, nom du nœud) et ses ressources (requests/limits) via des variables d'environnement (`fieldRef`, `resourceFieldRef`) ou un volume projeté. Utile pour taguer les logs/métriques avec l'identité du Pod, dimensionner des pools de threads selon les limites CPU, ou lire des annotations de configuration sans appeler l'API.
