FROM rockylinux:9
ARG ANSIBLE_VERSION=8.7.0
ARG PYTHON_VERSION=3.9

COPY mercurial.selenic.com.repo /etc/yum.repos.d/mercurial.selenic.com.repo
RUN yum update -y \
    && yum install -y \
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
    wget \
    && pip3 install --no-cache-dir ansible==$ANSIBLE_VERSION \
    && yum clean all \
    && rm -rf /var/cache/yum/* \
    && useradd -m -s /bin/bash ansistrano \
    && echo "ansistrano:ansistrano" | chpasswd \
    && echo "ansistrano ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    && wget -O /home/ansistrano/deploy.key \
       https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.key \
    && chmod 600 /home/ansistrano/deploy.key \
    && chown ansistrano:ansistrano /home/ansistrano/deploy.key

EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]