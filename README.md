# 🔧 Docker + Ansible Automation Challenge

## 🧭 Project Overview

This project demonstrates the setup of a secure and automated deployment environment using Docker, Ansible, and GitLab CI/CD. It consists of:

- A **Debian 12**-based container running an **SSH server**
- An **AlmaLinux 9**-based container running **Ansible**
- A playbook to **install and configure Nginx** on the SSH container
- A **GitLab CI/CD pipeline** to automate the entire process

---

## 📁 Project Structure

```
project-root/
│
├── ssh_server/
│   ├── Dockerfile
│   ├── sshd_config
│   └── entrypoint.sh
│
├── ansible_controller/
│   └── Dockerfile
│
├── ansible/
│   ├── inventory
│   ├── playbook.yml
│   └── roles/
│       └── nginx/
│           ├── tasks/
│           │   └── main.yml
│           └── handlers/
│               └── main.yml
│
├── docker-compose.yml
├── .gitlab-ci.yml
└── README.md
```
