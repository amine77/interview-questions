# ☸️ Kubernetes & Helm

> Pods, Deployments, Services, Ingress, Helm charts, troubleshooting

**18 questions**

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
