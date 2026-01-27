FROM fedora:40
ARG ANSIBLE_VERSION=13.1.0
ARG PYTHON_VERSION=3.12

RUN dnf update -y \
    && dnf install -y \
    openssh-server \
    openssh-clients \
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
    && pip3 install --no-cache-dir ansible==$ANSIBLE_VERSION \
    && dnf clean all \
    && rm -rf /var/cache/dnf/* \
    && useradd -m -s /bin/bash ansistrano \
    && echo "ansistrano:ansistrano" | chpasswd \
    && echo "ansistrano ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    && mkdir -p /run/sshd \
    && curl -L \
      https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.key \
      -o /home/ansistrano/deploy.key \
    && chmod 600 /home/ansistrano/deploy.key \
    && chown ansistrano:ansistrano /home/ansistrano/deploy.key

EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]