FROM ubuntu:xenial as app

# metadata
LABEL base.image="ubuntu:xenial"
LABEL software="jq"
LABEL software.version="1.6"
LABEL dexcription="JSON processor"
LABEL website="https://jqlang.github.io/jq/"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan.perera007@gmail.com"

RUN apt-get update && apt-get install --no-install-recommends -y \
    wget \
    ca-certificates && \
    apt-get autoclean && rm -rf /var/lib/apt/lists/* 

RUN mkdir /data

WORKDIR bin/

RUN wget https://github.com/jqlang/jq/releases/download/jq-1.6/jq-linux64 && \
    chmod +x jq-linux64 && \
    ln -s jq-linux64 jq 

ENV LC_ALL=C.UTF-8 


WORKDIR /data
