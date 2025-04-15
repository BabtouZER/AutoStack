# Docker-Ansible-Gitlab : Challenge Infra

Le but de cet exercice est de mettre en place un environnement de déploiement et d'utiliser Docker pour construire des images selon les exigences spécifiées.  
La première partie consiste à créer un conteneur Ansible, puis à configurer un serveur SSH, et enfin à déployer un serveur Nginx sur le conteneur SSH.  
En plus de la clarté du code, les mesures de sécurité et de performance mises en œuvre tout au long de l’exercice seront également prises en compte.  
En bonus, tout le processus sera répliqué et exécuté dans un pipeline GitLab CI.

Nous attendons que vous livriez un dépôt git et un court fichier Readme expliquant votre réflexion. Il n’est pas indispensable de terminer complètement le challenge, mais il est important de voir votre raisonnement concernant l’automatisation et la sécurisation.

## Liens utiles

- Comment configurer un serveur SSH dans un conteneur Docker : https://dev.to/s1ntaxe770r/how-to-setup-ssh-within-a-docker-container-i5i  
- Utilisation d’un fichier docker-compose pour construire et exécuter les deux images : https://docs.docker.com/reference/compose-file/build/  
- Définir le nom d’hôte d’un conteneur : https://docs.docker.com/reference/compose-file/services/#hostname  
- Créer un utilisateur non-root : https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user  
- Utiliser sudo sans mot de passe en tant qu’utilisateur Docker non-root : https://dev.to/emmanuelnk/using-sudo-without-password-prompt-as-non-root-docker-user-52bg  
- Bien débuter avec Ansible : https://docs.ansible.com/ansible/latest/getting_started/index.html  
- Intégrer Nginx avec Ansible : https://www.skynats.com/blog/how-to-integrate-nginx-with-ansible/  
- Désactiver la vérification de clé hôte SSH : https://docs.ansible.com/ansible/latest/reference_appendices/config.html#host-key-checking  

---

## 1. Créer une image Docker de serveur SSH basée sur une image Debian-12

Pour cette étape, vous devez configurer un serveur SSH qui hébergera un serveur Nginx :

1. Configurer l’environnement Docker.  
2. Créer un `Dockerfile` utilisant une image `Debian-12` pour exécuter un serveur SSH.  
3. Utiliser `docker-compose` pour configurer le serveur.  
4. Tester la connexion SSH au conteneur.

```
┌──────────────┐          ┌──────────────┐
|  (docker)    |  build   |  (docker)    |
|  Debian      |  ====>   |  ssh_server  |
└──────────────┘          └──────────────┘
```


---

## 2. Créer une image Docker Ansible basée sur une image AlmaLinux-9

À cette étape, vous devez créer un conteneur Docker capable d’exécuter une commande ou un playbook Ansible :

1. Créer un `Dockerfile` pour installer Ansible sur une image `Alma-9`.  
2. Lancer le conteneur avec une commande Ansible pour vérifier son bon fonctionnement (ex : `ansible --version`)  
3. Exécuter le conteneur Ansible pour tester la communication entre les deux conteneurs (ex : `ansible hostname_ssh_server -m ping`)

```
┌──────────────┐          ┌────────────────────┐
|  (docker)    |  build   | (docker)           |
|  AlmaLinux   |  ====>   | ansible_controller |
└──────────────┘          └────────────────────┘
```


---

## 3. Créer un playbook Ansible pour configurer un serveur web Nginx

Maintenant que nous avons un conteneur Ansible et un serveur SSH, nous allons créer un playbook pour installer un serveur Nginx sur le conteneur SSH :

1. Créer un rôle Ansible et un playbook pour Nginx.  
2. Exécuter le playbook à l’aide du conteneur Ansible.  
3. Tester le bon fonctionnement du serveur web avec `curl`.

```
┌────────────── docker-compose ────────────────┐
|                                              |
|  ansible_controller                          |
|     ║                                        |
|     ║ Deploy Nginx server                    |
|     ║ command: ansible-playbook ...          |
|     V                                        |
|  ssh_server                                  |
|                                              |
└──────────────────────────────────────────────┘
```


---

## 4. Bonus : Exécuter tout cela dans un GitLab CI

```
┌────────────── gitlab-ci ──────────────────────────────────┐
|                                                           |
|  [Build] ---> [Deploy] ---> [Install Nginx] ---> [Test]   |
|                                                           |
└───────────────────────────────────────────────────────────┘
```


### Liens utiles

- Tutoriel : Créer et exécuter votre premier pipeline CI/CD GitLab : https://docs.gitlab.com/ci/quick_start/  
- Runners hébergés par GitLab : https://docs.gitlab.com/ci/runners/hosted_runners/  
- Exécuteur Docker pour GitLab Runner : https://docs.gitlab.com/runner/executors/docker/  
- Référence de la syntaxe YAML CI/CD : https://docs.gitlab.com/ci/yaml/  
- Référence des variables prédéfinies CI/CD : https://docs.gitlab.com/ci/variables/predefined_variables/  
