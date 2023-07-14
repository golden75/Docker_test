# base image: Ubuntu
FROM ubuntu:jammy as app

ARG VELVET_VER="1.2.10"

# File Author / Maintainer
LABEL base.image="ubuntu:jammy"
LABEL dockerfile.version="1"
LABEL software="velvet"
LABEL software.version="1.2.10"
LABEL description="removes adapter sequences, primers, poly-A tails and other types of unwanted sequence from sequence data"
LABEL website="https://github.com/dzerbino/velvet/tree/v1.2.10"
LABEL license="https://github.com/dzerbino/velvet/blob/v1.2.10/LICENSE.txt"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan007@gmail.com"

RUN apt-get update; apt-get install -y --no-install-recommends \
    ca-certificates \
    build-essential make gcc wget; \
    wget https://github.com/dzerbino/velvet/archive/refs/tags/v${VELVET_VER}.tar.gz; \
    tar -xzvf v${VELVET_VER}.tar.gz; \
    rm -f v${VELVET_VER}.tar.gz; \
    cd velvet-${VELVET_VER}/; \
    make 'BUNDLEDZLIB=1'; \
    make doc; \
    apt-get autoclean; \
    rm -rf /var/lib/apt/lists/* 


RUN  mkdir /data

ENV PATH="$PATH:/velvet-${VELVET_VER}" \
    LC_ALL=C 

WORKDIR /data