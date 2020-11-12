FROM mikefarah/yq:3.3.4 AS yq
FROM hashicorp/terraform:0.13.3 AS terraform
FROM lachlanevenson/k8s-kubectl:v1.19.3 as kubectl
FROM lachlanevenson/k8s-helm:v3.3.4 as helm
FROM docker:19.03.13 AS docker
FROM mcr.microsoft.com/powershell:lts-debian-buster-slim as pwsh
FROM python:3-slim-buster

RUN apt-get update && apt-get install --no-install-recommends -y \
    ca-certificates \
    curl \
    wget \
    sudo \
    git \
    gzip \
    tar \
    jq \
    openssh-client \
    sshpass \
    bash-completion \
    iputils-ping \
    dnsutils

RUN pip install yamllint

COPY --from=yq /usr/bin/yq /usr/local/bin/yq
COPY --from=terraform /bin/terraform /usr/local/bin/terraform
COPY --from=kubectl /usr/local/bin/kubectl /usr/local/bin/kubectl
COPY --from=helm /usr/local/bin/helm /usr/local/bin/helm
COPY --from=docker /usr/local/bin/docker /usr/local/bin/docker
COPY --from=pwsh /opt/microsoft/powershell/7-lts/ /opt/microsoft/powershell/7-lts/
RUN chmod a+x,o-w /opt/microsoft/powershell/7-lts/pwsh && ln -s /opt/microsoft/powershell/7-lts/pwsh /usr/local/bin/pwsh

WORKDIR /home

ENTRYPOINT [ "/bin/bash" ]
