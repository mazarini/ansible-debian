# 🚀 MyHost Infrastructure (Ansible + Incus + Btrfs)

Ce dépôt contient l'automatisation complète de mon serveur **MyHost**. Le projet est conçu pour gérer à la fois la couche hôte (système) et l'orchestration des conteneurs via Incus.



## 🛠 Stack Technique
* **OS:** Debian 13 (Trixie)
* **Kernel:** 6.12+ (Optimisé pour Btrfs)
* **FileSystem:** Btrfs (RAID1 / Subvolumes `@trixie` & `@home`)
* **Virtualisation:** [Incus](https://linuxcontainers.org/incus/)
* **Automatisation:** Ansible

## 📂 Structure du Projet
* `host_config.yml` : Configuration du serveur physique (Sécurité, SSH, Btrfs, Réseau).
* `containers_config.yml` : Gestion du cycle de vie des conteneurs et des images.
* `group_vars/` : Paramètres globaux (réseau Incus, stockage).
* `host_vars/` : Paramètres spécifiques à l'hôte (IP, variables locales - *ignoré par Git*).

## 🚀 Installation & Usage

### 1. Pré-requis
Copier le template de configuration de l'hôte :
\`\`\`bash
cp host_vars/myhost.yml.example host_vars/myhost.yml
# Éditez host_vars/myhost.yml avec l'IP réelle du serveur
\`\`\`

### 2. Déploiement de l'Hôte
Configure le système, la sécurité et initialise Incus :
\`\`\`bash
ansible-playbook -i inventory.ini host_config.yml --ask-vault-pass
\`\`\`

### 3. Gestion des Conteneurs
Déploie les services dans des instances Incus :
\`\`\`bash
ansible-playbook -i inventory.ini containers_config.yml
\`\`\`

## 🔒 Sécurité
* **SSH:** Authentification par clés uniquement, accès Root restreint.
* **Secrets:** Les mots de passe (Incus trust, etc.) sont chiffrés via **Ansible Vault**.
* **Isolation:** Chaque conteneur utilise des profils Incus restreints.

---
*Projet maintenu par Mazarini.*