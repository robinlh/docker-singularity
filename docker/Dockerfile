#Download base image ubuntu 20.04
FROM ubuntu:20.04

# LABEL about the custom image
LABEL maintainer="robin@idia.ac.za"
LABEL version="0.1"
LABEL description="This is custom Docker Image with Singularity 3.9 installed in it to run builds with in CirclCI"

ENV SINGULARITY_VERSION=3.9.1

# Disable Prompt During Packages Installation
ARG DEBIAN_FRONTEND=noninteractive

# Update Ubuntu Software repository and install required OS libraries
RUN apt update
RUN apt-get install -y build-essential \
    libssl-dev \
    uuid-dev \
    libgpgme11-dev \
    squashfs-tools \
    libseccomp-dev \
    pkg-config \
    wget

# install Go
RUN wget https://go.dev/dl/go1.17.6.linux-amd64.tar.gz
RUN rm -rf /usr/local/go
RUN tar -C /usr/local -xzf go1.17.6.linux-amd64.tar.gz
ENV PATH=$PATH:/usr/local/go/bin
ENV GOPATH=$HOME/go
ENV PATH=/usr/local/go/bin:$PATH:$GOPATH/bin

# download, compile and install Singularity
RUN mkdir -p $GOPATH/src/github.com/sylabs
WORKDIR $GOPATH/src/github.com/sylabs
RUN wget https://github.com/sylabs/singularity/releases/download/v${SINGULARITY_VERSION}/singularity-ce-${SINGULARITY_VERSION}.tar.gz
RUN tar -xzf singularity-ce-${SINGULARITY_VERSION}.tar.gz
WORKDIR $GOPATH/src/github.com/sylabs/singularity-ce-${SINGULARITY_VERSION}
RUN ./mconfig
RUN make -C ./builddir
RUN make -C ./builddir install
