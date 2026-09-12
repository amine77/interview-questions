# ☸️ Kubernetes & Helm

> Pods, Deployments, Services, Ingress, Helm charts, troubleshooting

**50 questions**

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
