FROM python:3.14-alpine
ARG ANSIBLE_VERSION=13.1.0
ARG PYTHON_VERSION=3.14

COPY conf/requirements.txt /tmp/requirements.txt

RUN mkdir -p /root/.ssh /etc/ansible \
    && apk --no-cache add \
    sshpass \
    openssh-client \
    vim \
    nano \
    git \
    tar \
    rsync \
    && ssh-keyscan gitlab.com >> /root/.ssh/known_hosts \
    && ssh-keyscan github.com >> /root/.ssh/known_hosts \
    && pip install --upgrade pip \
    && pip install --no-cache-dir ansible==$ANSIBLE_VERSION \
    && pip install --no-cache-dir -r /tmp/requirements.txt \
    && ansible-galaxy collection install community.general

COPY conf/ansible.cfg /etc/ansible/ansible.cfg

WORKDIR /app/
