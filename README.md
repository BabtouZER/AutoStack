# AutoStack

## 🌍 Purpose

This project sets up a secure Docker-based deployment environment using:
- An SSH-enabled Debian container
- An AlmaLinux Ansible controller
- Automated NGINX deployment via Ansible
- CI/CD pipeline using GitLab

## 🔧 Project Structure

- `ssh_server/`: Debian container with SSH
- `ansible_controller/`: AlmaLinux with Ansible
- `ansible/`: Ansible playbook + inventory
- `docker-compose.yml`: Manages both services
- `.gitlab-ci.yml`: Automates the full process

## 🛡️ Security Measures

- Non-root users in both containers
- SSH password authentication with limited user access
- Sudo without password for Ansible execution
- Host key checking disabled (development only)

## 🚀 How to Use

```bash
docker-compose up --build
