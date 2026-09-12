# 🏗️ Infrastructure as Code

> Terraform, Ansible, modules, providers, playbooks

**12 questions**

---

### 1. À quoi sert `terraform.tfstate` ?
`🟢 Débutant` · Sujet : **Terraform**

**Réponse :** Stocke l'état actuel de l'infrastructure gérée par Terraform, permettant de calculer les différences lors des futurs plan/apply.

### 2. Qu'est-ce qu'un playbook Ansible ?
`🟢 Débutant` · Sujet : **Ansible**

**Réponse :** Fichier YAML décrivant des tâches à exécuter sur des hôtes distants, définissant l'état désiré du système, de façon idempotente.

### 3. À quoi servent les modules Terraform ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Regroupent et réutilisent un ensemble de ressources sous forme de composant paramétrable, favorisant modularité et cohérence.

### 4. Qu'est-ce qu'un rôle Ansible ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Structure organisée de répertoires regroupant une logique de configuration réutilisable entre playbooks.

### 5. Différence `plan` / `apply` ?
`🟢 Débutant` · Sujet : **Terraform**

**Réponse :** `plan` = simulation des changements. `apply` = exécution réelle des changements.

### 6. Qu'est-ce que l'idempotence ?
`🟢 Débutant` · Sujet : **Ansible**

**Réponse :** Exécuter plusieurs fois le même playbook produit le même résultat final sans effet indésirable.

### 7. Qu'est-ce qu'un provider ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Plugin permettant à Terraform d'interagir avec une plateforme spécifique (AWS, Azure, K8s).

### 8. Qu'est-ce qu'un handler ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Tâche déclenchée uniquement lorsqu'elle est notifiée par une autre tâche ayant produit un changement.

### 9. À quoi sert `terraform init` ?
`🟢 Débutant` · Sujet : **Terraform**

**Réponse :** Initialise le répertoire (téléchargement providers, config backend).

### 10. Qu'est-ce qu'un inventaire ?
`🟢 Débutant` · Sujet : **Ansible**

**Réponse :** Fichier listant les hôtes cibles organisés en groupes, avec variables associées.

### 11. Qu'est-ce qu'un data source ?
`🟠 Intermédiaire` · Sujet : **Terraform**

**Réponse :** Lit des informations sur une ressource existante sans la gérer directement.

### 12. Qu'est-ce qu'`ansible-vault` ?
`🟠 Intermédiaire` · Sujet : **Ansible**

**Réponse :** Chiffre des données sensibles pour les versionner en toute sécurité dans Git.
