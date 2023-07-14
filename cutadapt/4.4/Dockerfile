# base image: Ubuntu
FROM ubuntu:jammy as app

ARG CUTADAPT_VER="4.4"

# File Author / Maintainer
LABEL base.image="ubuntu:jammy"
LABEL dockerfile.version="1"
LABEL software="cutadapt"
LABEL software.version="4.4"
LABEL description="removes adapter sequences, primers, poly-A tails and other types of unwanted sequence from sequence data"
LABEL website="https://cutadapt.readthedocs.io/en/stable/"
LABEL license="https://github.com/marcelm/cutadapt/blob/main/LICENSE"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan007@gmail.com"

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    make \
    gcc \
    wget \
    python3 \
    python3-dev \
    python3-pip && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/*

# install cutadapt
RUN python3 -m pip install cutadapt && \
    mkdir /data

ENV LC_ALL=C

WORKDIR /data

