FROM ubuntu:24.04
ARG ANSIBLE_VERSION=13.1.0
ARG PYTHON_VERSION=3.12

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    openssh-server \
    rsync \
    tar \
    ssh \
    git \
    unzip \
    subversion \
    mercurial \
    python3 \
    python3-pip \
    curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && sed -i.bak 's/^[#[:space:]]*PubkeyAuthentication.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config \
    && sed -i.bak 's/^[#[:space:]]*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && rm /usr/lib/python$PYTHON_VERSION/EXTERNALLY-MANAGED \
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

EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]