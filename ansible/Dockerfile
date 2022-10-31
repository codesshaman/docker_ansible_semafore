FROM python:3.12.0a1-alpine3.16

ARG ANSIBLE_VERSION

RUN echo "===> Installing sudo to emulate normal OS behavior..."  && \
    apk --update add sudo                                         && \
    \
    \
    echo "===> Adding Python runtime..."  && \
    apk update add git net-tools && \
    python -m pip install --upgrade pip; \
    pip install --upgrade setuptools; \
    \
    \
    echo "===> Installing Ansible..."  && \
    pip install 'ansible==${ANSIBLE_VERSION}'; \
    pip install pyvmomi; \
    \
    \
    echo "===> Removing package list..."  && \
    apk del build-dependencies            && \
    rm -rf /var/cache/apk/*               && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible                        && \
    \
    \
    echo 'localhost' > /etc/ansible/hosts

COPY ansible-playbook-wrapper /usr/local/bin/

# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]