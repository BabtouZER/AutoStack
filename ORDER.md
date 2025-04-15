# Docker-Ansible-Gitlab: Challenge Infra
The purpose of this exercise is to set up a deployment environment and use Docker to build images based on the specified requirements.
The first part involves creating an Ansible container, then setting up an SSH server, and finally deploying an Nginx server on the SSH Container.
In addition to code clarity, the security and performance measures implemented throughout the exercise will also be taken into account.
As a bonus step, the entire process will be replicated and executed within a GitLab CI pipeline

We expect you to deliver a git repository and a short Readme explaning your reflexion. You don't absolutely need to complete the challenge but it's important to see you thought process about the automation and securization.

Useful links:
- How to setup an ssh server within a docker container : https://dev.to/s1ntaxe770r/how-to-setup-ssh-within-a-docker-container-i5i
- You can use a docker-compose file to build and run both images: https://docs.docker.com/reference/compose-file/build/
- Set container hostname: https://docs.docker.com/reference/compose-file/services/#hostname
- Creating a non-root user: https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user
- Using sudo without password prompt as non-root docker user: https://dev.to/emmanuelnk/using-sudo-without-password-prompt-as-non-root-docker-user-52bg
- Get start with Ansible: https://docs.ansible.com/ansible/latest/getting_started/index.html
- How to integrate nginx with Ansible: https://www.skynats.com/blog/how-to-integrate-nginx-with-ansible/
- Disble SSH host key checking: https://docs.ansible.com/ansible/latest/reference_appendices/config.html#host-key-checking

### 1. Create a SSH server Docker image base on Debian-12 image
For this step, you need to set up an SSH server that will host a nginx server:
1) Set up the Docker environment.
2) Create a Dockerfile using a Debian-12 image to run an SSH server.
3) Use Docker Compose to configure the server.
4) Test SSH connection to the container.

```
┌──────────────┐          ┌──────────────┐
|  (docker)    |  build   |  (docker)    |
|  Debian      |  ====>   |  ssh_server  |
└──────────────┘          └──────────────┘
```

### 2. Create an Ansible Docker image based on AlmaLinux-9 image

At this step, you need to create a Docker container capable of executing an Ansible command or playbook:
1) Create a Dockerfile to install Ansible on an Alma-9 image. 
2) Launch the container with an Ansible command to ensure proper functionality (e.g., ansible --version)
3) Run the Ansible container to test communication between the two containers (e.g., ansible hostname_ssh_server -m ping)

```
┌──────────────┐          ┌────────────────────┐
|  (docker)    |  build   | (docker)           |
|  AlmaLinux   |  ====>   | ansible_controller |
└──────────────┘          └────────────────────┘
```

### 3. Create an Ansible playbook to configure an Nginx web server
Now that we have an Ansible container and an SSH server, we will create a playbook to set up a Nginx server on the SSH container:
1) Create an Ansible role and playbook for Nginx.
2) Run the playbook using the Ansible container.
3) Test the web server functionality using curl.

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

### 4. Bonus Run it in a Gitlab CI

```
┌────────────── gitlab-ci ──────────────────────────────────┐
|                                                           |
|  [Build] ---> [Deploy] ---> [Install Nginx] ---> [Test]   |
|                                                           |
└───────────────────────────────────────────────────────────┘
```

Useful links:
- Tutorial: Create and run your first GitLab CI/CD pipeline: https://docs.gitlab.com/ci/quick_start/
- GitLab-hosted runners: https://docs.gitlab.com/ci/runners/hosted_runners/
- Gitlab runner Docker executor: https://docs.gitlab.com/runner/executors/docker/
- CI/CD YAML syntax reference: https://docs.gitlab.com/ci/yaml/
- Predefined CI/CD variables reference: https://docs.gitlab.com/ci/variables/predefined_variables/
