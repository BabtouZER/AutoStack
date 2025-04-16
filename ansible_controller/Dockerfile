FROM almalinux:9

RUN dnf install -y epel-release && \
    dnf install -y ansible python3 python3-pip openssh-clients sshpass sudo && \
    pip3 install ansible && \
    useradd -ms /bin/bash ansible && \
    echo "ansible:ansiblepass" | chpasswd && \
    echo "ansible ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN dnf clean all

USER ansible
WORKDIR /home/ansible