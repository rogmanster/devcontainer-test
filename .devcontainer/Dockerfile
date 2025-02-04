# This is an official python image.
FROM mcr.microsoft.com/vscode/devcontainers/python:3.11-bookworm
# Set the user to root.
USER root
# Prevent interactive popups when initializing debian.
ENV DEBIAN_FRONTEND=noninteractive
# Set up a dir for our stuff
RUN mkdir -p /devcontainer && chmod -R 777 /devcontainer
# Install OS packages
RUN apt-get update && sudo apt upgrade -y && apt-get install --no-install-recommends -y \
    build-essential \
    curl \
    git \
    cmake \
    wget \
    jq \
    cmake \
    zip \
    unzip \
    azure-cli
# Set user to vscode
USER vscode
COPY ./requirements.txt /devcontainer/requirements.txt
# Install python packages
RUN pip install --upgrade pip --disable-pip-version-check --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org && \
    pip install -r /devcontainer/requirements.txt --disable-pip-version-check --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host files.pythonhosted.org && \
    pip --disable-pip-version-check list --outdated --format=json | python -c "import json, sys; print('\n'.join([x['name'] for x in json.load(sys.stdin)]))" | xargs -n1 pip install -U
