FROM alpine:3.16

ARG ANSIBLE_VERSION

RUN echo "===> Installing sudo to emulate normal OS behavior..."  && \
    apk --update add sudo                                         
    # && \
    # \
    # \
RUN echo "===> Adding Python runtime..."  && \
    apk --update add python py-pip openssl ca-certificates    && \
    apk --update add --virtual build-dependencies \
                python-dev libffi-dev openssl-dev build-base  && \
    pip install --upgrade pip pycrypto cffi                   
    # && \
    # \
    # \
RUN echo "===> Installing Ansible..."  && \
    pip install ansible==1.9.4         
    # && \
    # \
    # \
RUN echo "===> Installing handy tools (not absolutely required)..."  && \
    apk --update add sshpass openssh-client rsync  
    # && \
    # \
    # \
RUN echo "===> Removing package list..."  && \
    apk del build-dependencies            && \
    rm -rf /var/cache/apk/*               
    # && \
    # \
    # \
RUN echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible                        && \
    echo 'localhost' > /etc/ansible/hosts


# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]