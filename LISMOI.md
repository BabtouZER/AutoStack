# AutoStack

## 🌍 Objectif

Ce projet met en place un environnement de déploiement sécurisé basé sur Docker, en utilisant :
- Un conteneur Debian avec SSH activé
- Un contrôleur Ansible basé sur AlmaLinux
- Un déploiement automatisé de NGINX via Ansible
- Une pipeline CI/CD avec GitLab

## 🔧 Structure du Projet

- `ssh_server/` : Conteneur Debian avec SSH
- `ansible_controller/` : AlmaLinux avec Ansible installé
- `ansible/` : Playbook et inventaire Ansible
- `docker-compose.yml` : Gère les deux services via Docker Compose
- `.gitlab-ci.yml` : Automatise l'ensemble du processus

## 🛡️ Mesures de Sécurité

- Utilisateurs non-root dans les deux conteneurs
- Authentification SSH par mot de passe avec accès limité
- Utilisation de `sudo` sans mot de passe pour l'exécution d'Ansible
- Vérification de la clé hôte SSH désactivée (uniquement pour le développement)

## 🚀 Comment l'utiliser

```bash
docker-compose up --build
