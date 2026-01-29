FROM opensuse/leap:16.0

ARG ANSIBLE_VERSION=13.1.0
ARG PYTHON_VERSION=3.13

RUN zypper refresh \
    && zypper install -y \
       openssh \
       openssh-server \
       rsync \
       tar \
       git \
       unzip \
       subversion \
       mercurial \
       python3 \
       python3-pip \
       curl \
    && zypper clean -a \
    && ssh-keygen -A \
    && [ -f /etc/ssh/sshd_config ] || cp /usr/etc/ssh/sshd_config /etc/ssh/sshd_config \
    && sed -i.bak 's/^[#[:space:]]*PubkeyAuthentication.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config \
    && sed -i.bak 's/^[#[:space:]]*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && pip3 install --no-cache-dir ansible==${ANSIBLE_VERSION} \
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

CMD ["/usr/sbin/sshd", "-D"]
