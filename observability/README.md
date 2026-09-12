# 📊 Observability

> Logs, métriques, traces, SLI/SLO/SLA, golden signals, dashboards

**10 questions**

---

### 1. Quels sont les trois piliers de l'observabilité ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Les logs (événements horodatés détaillés), les métriques (mesures numériques agrégées, ex : latence, taux d'erreur) et les traces distribuées (suivi d'une requête à travers plusieurs services), souvent combinés via Prometheus, Grafana et Zipkin/Jaeger.

### 2. Quelle est la différence entre monitoring et observabilité ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Le monitoring surveille des métriques prédéfinies pour détecter des problèmes connus. L'observabilité permet de comprendre l'état interne d'un système à partir de ses sorties (logs, métriques, traces), y compris pour diagnostiquer des problèmes imprévus.

### 3. Qu'est-ce que le "distributed tracing" et quel identifiant relie les spans entre services ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Suivi d'une requête à travers plusieurs microservices. Chaque requête reçoit un trace ID unique propagé entre services, et chaque étape locale devient un span rattaché à ce trace ID.

### 4. Qu'est-ce qu'un SLI, un SLO et un SLA ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** SLI = métrique mesurée. SLO = objectif interne. SLA = engagement contractuel envers le client, souvent avec pénalités.

### 5. Cardinalité des métriques et enjeu dans Prometheus ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Nombre de combinaisons uniques de labels. Une cardinalité trop élevée explose l'utilisation mémoire de Prometheus.

### 6. Golden signals de Google SRE ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Latence, trafic, erreurs, saturation. Vue d'ensemble suffisante pour détecter la plupart des problèmes.

### 7. Corrélation logs/traces ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Injection du trace ID dans les logs applicatifs, permettant de retrouver tous les logs d'une requête à travers plusieurs services.

### 8. Dashboard as code avec Grafana ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Définir les dashboards en JSON/YAML versionnés dans Git, permettant reproductibilité, revue de code, déploiement automatisé.

### 9. Sampling dans le tracing distribué ?
`🟠 Intermédiaire` · Sujet : **Observabilité**

**Réponse :** Collecte d'un sous-ensemble représentatif des traces, réduisant le volume de données tout en gardant une visibilité statistique.

### 10. Alert fatigue et comment la limiter ?
`🟢 Débutant` · Sujet : **Observabilité**

**Réponse :** Volume excessif d'alertes désensibilisant les équipes. Limité via seuils basés sur l'impact réel et regroupement des alertes.
