FROM ubuntu:22.04

WORKDIR /app

ARG GO_VERSION="go1.25.4"
ARG GO_URL="https://go.dev/dl/${GO_VERSION}.linux-amd64.tar.gz"

ARG BOOT_DEV_CLI_URL="github.com/bootdotdev/bootdev@latest"

#install git
RUN apt update && apt install -y \
software-properties-common && \
add-apt-repository -y ppa:git-core/ppa && \
apt install -y git

RUN apt install -y curl

#install go
RUN curl -OL ${GO_URL} && \
    rm -rf /usr/local/go && \
    tar -C /usr/local -xzf ${GO_VERSION}.linux-amd64.tar.gz

ENV PATH=$PATH:/usr/local/go/bin

#install bootdev cli
RUN go install ${BOOT_DEV_CLI_URL}

ENV PATH=$PATH:/root/go/bin


#install kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" &&\
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256" &&\
    echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

RUN install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
