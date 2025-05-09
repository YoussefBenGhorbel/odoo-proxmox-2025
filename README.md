# Automatisation du Provisionnement et Supervision de Machines Virtuelles via Odoo et Proxmox VE

Projet de Fin d'Études (PFE) visant à concevoir et développer une solution intégrée pour l'automatisation du provisionnement et la supervision de VMs hébergées sur Proxmox VE, avec une interface client Odoo.

Ce dépôt contient le code d'Infrastructure as Code (IaC), les scripts d'automatisation, les configurations de supervision et la documentation du projet réalisé par Youssef Ben Ghorbel.

## Table des Matières

-   [Introduction](#introduction)
-   [Objectifs du Projet](#objectifs-du-projet)
-   [Architecture de la Solution](#architecture-de-la-solution)
-   [Technologies Utilisées](#technologies-utilisées)
-   [Structure du Dépôt](#structure-du-dépôt)
-   [Prérequis](#prérequis)
-   [Installation et Configuration](#installation-et-configuration)
    -   [Configuration de l'Environnement Proxmox](#configuration-de-lenvironnement-proxmox)
    -   [Configuration Odoo](#configuration-odoo)
    -   [Configuration des Outils IaC](#configuration-des-outils-iac)
    -   [Configuration de la Supervision](#configuration-de-la-supervision)
-   [Utilisation](#utilisation)
    -   [Option 1: Création de Template avec Packer](#option-1-création-de-template-avec-packer)
    -   [Option 2: Conversion d'Image VMDK](#option-2-conversion-dimage-vmdk)
    -   [Déploiement de VM avec Terraform](#déploiement-de-vm-avec-terraform)
    -   [Configuration avec Ansible](#configuration-avec-ansible)
    -   [Orchestration du Workflow](#orchestration-du-workflow)
-   [Détail des Sprints](#détail-des-sprints)
-   [Tests](#tests)
-   [Considérations de Sécurité](#considérations-de-sécurité)
-   [Perspectives et Travaux Futurs](#perspectives-et-travaux-futurs)
-   [Auteur](#auteur)
-   [Licence](#licence)

## Introduction

L'automatisation et l'optimisation des infrastructures informatiques sont cruciales. Ce projet aborde la problématique de la création et gestion de machines virtuelles (VMs) de manière rapide, fiable, répétable et sécurisée. Il intègre une plateforme de gestion commerciale (Odoo) comme portail client avec un backend d'automatisation basé sur Proxmox VE et des outils IaC modernes.

Le rapport complet du projet, incluant le plan de sprints détaillé, est disponible dans le dossier `docs/sprint_plan_detailed_latex/`.

## Objectifs du Projet

Les objectifs principaux de ce PFE sont :

1.  **Interface Client Odoo:** Permettre la sélection et la commande de VMs (OS, CPU, RAM, Stockage) via Odoo.
2.  **Automatisation Robuste:** Développer un workflow d'automatisation (Packer, Terraform, Ansible) pour créer et configurer les VMs sur Proxmox VE.
3.  **Supervision Intégrée:** Mettre en place une solution de supervision (Prometheus, Grafana, Alertmanager) pour les VMs et l'infrastructure PVE, avec visualisation pour l'admin et (filtrée) pour le client.
4.  **Gestion des Sauvegardes:** Établir les fondations pour une gestion efficace des sauvegardes (via Proxmox Backup Server).
5.  **Standardisation et Fiabilité:** Assurer la standardisation, la fiabilité, la sécurité et la maintenabilité de la solution.
6.  **Documentation Complète:** Documenter l'architecture, les processus et les configurations.

## Architecture de la Solution

[TODO: Insérer ici une version simplifiée du diagramme d'architecture globale ou un lien vers celui-ci dans `/docs/diagrams/`. Vous pouvez décrire brièvement les principaux composants : Odoo, Orchestrateur, Packer, Terraform, Ansible, Proxmox VE, Outils de Supervision, PBS.]

Exemple de description :
La solution s'articule autour d'Odoo comme interface utilisateur, qui communique avec une couche d'orchestration. Cette dernière pilote les outils IaC (Packer pour la création de templates, Terraform pour le provisionnement des VMs, Ansible pour la configuration post-déploiement) interagissant avec Proxmox VE. Les VMs et l'infrastructure sont supervisées par une stack Prometheus/Grafana/Alertmanager, et les sauvegardes sont gérées par Proxmox Backup Server.

## Technologies Utilisées

-   **Virtualisation**: Proxmox VE (Version [TODO: ex: 7.x ou 8.x])
-   **ERP & Portail Client**: Odoo Community Edition (Version [TODO: ex: 15, 16, 17])
-   **IaC - Création d'Images**: Packer (Version [TODO: ex: 1.8.x])
-   **IaC - Provisionnement**: Terraform (Version [TODO: ex: 1.3.x])
-   **IaC - Configuration Management**: Ansible (Version [TODO: ex: 2.12.x])
-   **Supervision & Alerting**: Prometheus, Grafana, Alertmanager
-   **Sauvegarde**: Proxmox Backup Server (PBS)
-   **Scripting & Orchestration**: Python 3 (Version [TODO: ex: 3.9+]), Shell (Bash)
-   **Base de Données (Odoo)**: PostgreSQL (Version [TODO: ex: 14, 15])
-   **Contrôle de Version**: Git, GitHub
-   **OS pour les templates/VMs**: Ubuntu Server 22.04 LTS (principalement), [TODO: Lister autres OS supportés]

## Structure du Dépôt
Markdown
.
├── .github/workflows/ # (Futur) CI/CD pipelines
├── docs/ # Documentation
│ ├── sprint_plan_detailed_latex/ # Source LaTeX du plan de sprints et rapport
│ ├── diagrams/ # Diagrammes (architecture, séquence, cas d'utilisation)
│ └── RAPPORT_PFE.pdf # (Futur) Rapport final compilé
├── iac/ # Infrastructure as Code
│ ├── packer/ # Configurations Packer
│ ├── terraform/ # Configurations Terraform
│ └── ansible/ # Playbooks et rôles Ansible
├── odoo_custom_modules/ # Modules Odoo personnalisés
│ └── proxmox_connector/ # Module principal d'intégration Proxmox
├── scripts/ # Scripts utilitaires et d'orchestration
├── monitoring_configs/ # Configurations pour Prometheus, Alertmanager, Dashboards Grafana
├── .gitignore # Fichiers et dossiers à ignorer par Git
├── README.md # Ce fichier
└── LICENSE # Licence du projet
## Prérequis

-   Accès administrateur à un environnement Proxmox VE.
-   Instance Odoo fonctionnelle.
-   Outils IaC (Packer, Terraform, Ansible) installés sur la machine d'orchestration ou le runner CI/CD.
-   Python 3.x et les bibliothèques nécessaires pour les scripts d'orchestration et les modules Odoo.
-   Images ISO des OS à utiliser avec Packer, accessibles par Proxmox.
-   [TODO: Lister d'autres prérequis spécifiques, ex: accès réseau, configuration DNS]

## Installation et Configuration

[TODO: Cette section doit être très détaillée et spécifique à votre projet.]

### Configuration de l'Environnement Proxmox
1.  Assurez-vous que Proxmox VE est installé et fonctionnel.
2.  Créez les pools de stockage nécessaires (pour les ISOs, les disques VM, les sauvegardes PBS).
3.  Configurez les ponts réseau (ex: `vmbr0`).
4.  Créez un utilisateur et un token API Proxmox avec les permissions adéquates pour Packer et Terraform.
    -   Permissions pour Packer: [TODO: Lister les permissions nécessaires, ex: `Datastore.AllocateSpace`, `Datastore.Audit`, `Sys.Audit`, `Sys.Console`, `Sys.Modify`, `VM.Allocate`, `VM.Audit`, `VM.Clone`, `VM.Config.CDROM`, `VM.Config.Cloudinit`, `VM.Config.CPU`, `VM.Config.Disk`, `VM.Config.HWType`, `VM.Config.Memory`, `VM.Config.Network`, `VM.Config.OS`, `VM.Migrate`, `VM.Monitor`, `VM.PowerMgmt`, `Permissions.Modify` sur `/storage/your_iso_storage`].
    -   Permissions pour Terraform: [TODO: Lister les permissions, similaires mais peuvent varier légèrement].

### Configuration Odoo
1.  Installez et configurez Odoo.
2.  Installez le module personnalisé `odoo_custom_modules/proxmox_connector`.
3.  Configurez les paramètres du module pour la connexion à l'orchestrateur/Proxmox API (URL, crédentials sécurisés).
4.  Définissez les produits "VM" dans Odoo avec les options configurables (OS, plans de ressources).

### Configuration des Outils IaC
1.  **Packer**:
    -   Placez les fichiers ISO des OS dans le pool de stockage Proxmox désigné (ex: `local:iso`).
    -   Adaptez les variables dans `iac/packer/ubuntu-2204/ubuntu-2204.pkr.hcl` (URL API, token, noms, chemins ISO).
    -   Adaptez le fichier `iac/packer/ubuntu-2204/http/user-data` (ou `preseed.cfg`) pour l'autoinstallation.
2.  **Terraform**:
    -   Configurez les variables du provider Proxmox (API URL, token).
    -   Adaptez les variables dans `iac/terraform/proxmox-vm/variables.tf` (noms de template, pools de stockage, réseaux). Envisagez d'utiliser un fichier `terraform.tfvars` (ignoré par git) pour les secrets.
3.  **Ansible**:
    -   Adaptez `iac/ansible/ansible.cfg` si nécessaire.
    -   Préparez votre inventaire (statique ou dynamique). Un exemple est dans `iac/ansible/inventory/hosts.ini.example`.
    -   Adaptez les playbooks et rôles dans `iac/ansible/` à vos besoins de configuration.

### Configuration de la Supervision
1.  Déployez une VM pour héberger la stack de monitoring.
2.  Installez Prometheus, Alertmanager, Grafana.
3.  Configurez Prometheus (`monitoring_configs/prometheus/prometheus.yml.example`) pour scraper les cibles (nœuds Proxmox, PVE exporter, VMs invitées via Node Exporter).
4.  Configurez les règles d'alerte Prometheus (`monitoring_configs/prometheus/rules/basic_alerts.yml.example`).
5.  Configurez Alertmanager (`monitoring_configs/alertmanager/alertmanager.yml.example`) pour le routage des notifications (ex: email, Slack).
6.  Configurez Grafana pour utiliser Prometheus comme source de données et importez/créez des dashboards (ex: `monitoring_configs/grafana_dashboards/proxmox_overview.json`).

## Utilisation

### Option 1: Création de Template avec Packer
Ce processus crée une "golden image" Proxmox.
```bash
cd iac/packer/ubuntu-2204/
# Assurez-vous que les variables (proxmox_api_url, token, etc.) sont définies
# Soit via des variables d'environnement (TF_VAR_name), un fichier .pkrvars.hcl, ou en ligne de commande.
packer init .
packer validate .
packer build .
Le template sera disponible dans Proxmox VE.
Option 2: Conversion d'Image VMDK
Utilisez le script scripts/orchestrate_deployment.py (adapté du script de conversion) ou scripts/convert_vmdk.sh pour convertir une image VMDK existante en QCOW2 et potentiellement créer une VM.
cd scripts/
# Pour le script Python (exemple d'orchestration de conversion et création VM)
sudo python3 orchestrate_deployment.py
# Suivre les instructions du script

# Pour le script shell (conversion et import simple)
# sudo ./convert_vmdk.sh <nom_base_vmdk_sans_extension> [vmid_cible_optionnelle]

Déploiement de VM avec Terraform
Ce processus clone un template Packer (Option 1) ou déploie une VM qui utilisera un disque converti (Option 2, nécessitant une adaptation de la configuration Terraform).
cd iac/terraform/proxmox-vm/ # Ou un dossier d'environnement comme iac/terraform/environments/dev/
# Assurez-vous que les variables sont définies (terraform.tfvars, variables d'env, etc.)
# Spécifiez au minimum var.template_name (pour l'Option 1).
terraform init
terraform validate
terraform plan -out=vm.plan
terraform apply vm.plan
Configuration avec Ansible
Une fois la VM provisionnée par Terraform et son IP connue :
cd iac/ansible/
# Assurez-vous que l'IP de la nouvelle VM est dans votre inventaire Ansible
# (ou passez-la avec --limit ou via des extra-vars)
ansible-playbook -i inventory/hosts.ini.example playbooks/configure_vm.yml --ask-become-pass

Orchestration du Workflow
[TODO: Décrivez comment le workflow de bout en bout est déclenché et géré. Si vous avez un script principal orchestrate_deployment.py qui gère l'ensemble, expliquez son utilisation ici.]
Exemple si orchestré par un script Python:
cd scripts/
# sudo python3 main_orchestrator.py --os ubuntu2204 --cpu 2 --ram 2048 --disk 50 --client-id XYZ

Détail des Sprints
Le projet a été structuré en plusieurs sprints, chacun avec des objectifs spécifiques :
Sprint 0: Préparation de l'environnement et fondations du projet.
Sprint 1 (Approche 1 & 2): Développement boutique Odoo, déploiement, abonnements, synchronisation, upscale. Initialement massif, décomposé dans l'Approche 2 en sous-sprints (1a à 1d).
Sprint 2: Configuration réseau et sécurité fondamentale (Proxmox). Note: Dans votre rapport PFE, le Sprint 2 était "Automatisation du Provisionnement", cela semble être une renumérotation ou un focus différent dans ce README.
Sprint 3 (Approche 1 & 2): Automatisation avancée de l'infrastructure (IaC - Packer, Terraform, Ansible). Décomposé en sous-sprints (3a à 3c) dans l'Approche 2.
Sprint 4: Mise en place de la surveillance (Monitoring - Prometheus, Grafana, Alertmanager).
Sprint 5: Stratégie de sauvegarde et reprise d'activité (Proxmox Backup Server).
Consultez docs/sprint_plan_detailed_latex/Plan_Sprints_Detaille.tex pour une description exhaustive de chaque sprint.
Tests
La stratégie de test inclut :
Tests Unitaires: Pour les fonctions critiques des scripts d'orchestration.
Validation des Configurations IaC: Utilisation de packer validate, terraform validate, ansible-lint.
Tests d'Intégration: Validation de chaque chaîne d'outils (Packer build, Terraform deploy, Ansible config).
Tests de Bout-en-Bout: Simulation d'une commande client et vérification du pipeline complet.
Considérations de Sécurité
Gestion des Secrets: Utilisation de fichiers de variables non versionnés et de variables d'environnement. Recommandation future : HashiCorp Vault.
Principe du Moindre Privilège: Tokens API Proxmox avec permissions restreintes.
Sécurisation des Images/Templates: Hardening de base via Packer et Ansible.
Validation des Entrées: Sécurisation de l'orchestrateur contre les injections.
Audit et Journalisation: Pour la traçabilité des opérations.
Perspectives et Travaux Futurs
Orchestration avancée avec Jenkins, GitLab CI, ou Argo Workflows.
Intégration Odoo plus complète (cycle de vie VM, monitoring client).
Intégration HashiCorp Vault pour la gestion des secrets.
Catalogue de services Odoo évolué avec tarification flexible.
Haute disponibilité et scalabilité des composants critiques.
Suite de tests automatisés complète (unitaire, intégration, bout-en-bout).
Amélioration des politiques de sauvegarde et Plan de Reprise d'Activité (PRA).
Auteur
Youssef Ben Ghorbel - (GitHub: YoussefBenGhorbel)
[TODO: Ajouter lien LinkedIn ou autre contact si souhaité]
Licence
Ce projet est sous licence [TODO: Choisir une licence, ex: MIT]. Voir le fichier LICENSE pour plus de détails.
(Si MIT, le contenu du fichier LICENSE serait :)
MIT License

Copyright (c) [Année Actuelle] Youssef Ben Ghorbel

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
