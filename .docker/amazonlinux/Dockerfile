FROM amazonlinux:2023
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
    wget \
    && yum clean all \
    && rm -rf /var/cache/yum/* \
    && ssh-keygen -A \
    && sed -i.bak 's/^[#[:space:]]*PubkeyAuthentication.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config \
    && sed -i.bak 's/^[#[:space:]]*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && pip3 install --no-cache-dir ansible==$ANSIBLE_VERSION \
    && mkdir -p /run/sshd /root/.ssh \
    && wget -O /root/deploy.key \
       https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.key \
    && wget -O /root/.ssh/authorized_keys \
       https://raw.githubusercontent.com/mjmdurand/ansistrano.deploy/mdurand/WIP/test/deploy.pub \
    && chmod 600 /root/deploy.key /root/.ssh/authorized_keys \
    && chmod 700 /root/.ssh

COPY sshd /etc/pam.d/sshd

EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]