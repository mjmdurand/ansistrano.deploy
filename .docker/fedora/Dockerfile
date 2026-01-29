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
    curl \
    && dnf clean all \
    && rm -rf /var/cache/dnf/* \
    && ssh-keygen -A \
    && sed -i.bak 's/^[#[:space:]]*PubkeyAuthentication.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config \
    && sed -i.bak 's/^[#[:space:]]*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && pip3 install --no-cache-dir ansible==$ANSIBLE_VERSION \
    && mkdir -p /run/sshd /root/.ssh \
    && curl -L \
      https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.key \
      -o /root/deploy.key \
    && curl -L \
      https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.pub \
      -o /root/.ssh/authorized_keys \
    && chmod 600 /root/deploy.key /root/.ssh/authorized_keys \
    && chmod 700 /root/.ssh

COPY sshd /etc/pam.d/sshd

EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]