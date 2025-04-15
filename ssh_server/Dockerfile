FROM debian:12

RUN apt-get update && \
    apt-get install -y openssh-server python3 sudo curl openssh-client && \
    useradd -ms /bin/bash user && \
    echo "user:userpass" | chpasswd && \
    echo "user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

COPY sshd_config /etc/ssh/
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

EXPOSE 22
CMD ["/entrypoint.sh"]
