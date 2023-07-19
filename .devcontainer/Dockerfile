FROM mcr.microsoft.com/devcontainers/python:0-3.9-bullseye

# change this for every release
ARG _AVD_VERSION
ARG _CLAB_VERSION
ARG _RELEASE_DATE
ARG _YQ_VERSION
ARG _YQ_BINARY

LABEL maintainer="Arista Ansible Team <ansible@arista.com>"
LABEL com.example.version="0.1"
LABEL vendor1="Arista Networks"
LABEL com.example.release-date=${_RELEASE_DATE}
LABEL com.example.version.is-production="False"
LABEL org.opencontainers.image.description="AVD Extended Workshop Devcontainer"

# install some basic tools inside the container
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    sshpass \
    curl \
    iputils-ping \
    htop \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean

# install yq
RUN wget https://github.com/mikefarah/yq/releases/download/${_YQ_VERSION}/${_YQ_BINARY} -O /usr/bin/yq \
    && chmod +x /usr/bin/yq

# switch user to vscode otherwise Ansible will be installed as root
USER vscode
ENV PATH=$PATH:/home/vscode/.local/bin
ENV ANSIBLE_CONFIG="/workspaces/avd-extended-workshop/avd_inventory/ansible.cfg"
# install Ansible AVD collection
RUN pip3 install "ansible-core>=2.13.1,<2.14.0" \
    && ansible-galaxy collection install arista.avd:==${_AVD_VERSION} \
    && pip3 install -r /home/vscode/.ansible/collections/ansible_collections/arista/avd/requirements.txt

# install the latest containerlab
RUN bash -c "$(curl -sL https://get.containerlab.dev)" -- -v ${_CLAB_VERSION}
