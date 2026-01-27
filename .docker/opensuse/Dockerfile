FROM opensuse/leap:16.0

ARG ANSIBLE_VERSION=13.1.0
ARG PYTHON_VERSION=3.13

# Installation des paquets nécessaires
RUN zypper refresh \
    && zypper install -y \
       openssh \
       rsync \
       tar \
       git \
       unzip \
       subversion \
       mercurial \
       python3 \
       python3-pip \
       sudo \
       curl \
    && pip3 install --no-cache-dir ansible==${ANSIBLE_VERSION} \
    && zypper clean -a \
    && useradd -m -s /bin/bash ansistrano \
    && echo "ansistrano:ansistrano" | chpasswd \
    && echo "ansistrano ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers \
    && curl -L \
      https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.key \
      -o /home/ansistrano/deploy.key \
    && chmod 600 /home/ansistrano/deploy.key \
    && chown ansistrano:ansistrano /home/ansistrano/deploy.key

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
