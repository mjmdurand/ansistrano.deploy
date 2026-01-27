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
    sudo \
    curl \
    && rm /usr/lib/python$PYTHON_VERSION/EXTERNALLY-MANAGED \
    && pip3 install --no-cache-dir ansible==$ANSIBLE_VERSION \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
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