# builder
FROM ubuntu:jammy as builder

ARG AMRFINDER_VER="3.11.14"
ARG AMRFINDER_DB_VER="2023-04-17.1"
ARG BLAST_VER="2.14.0"

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    wget \
    libgomp1 \
    hmmer \
    procps && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/*

# download and install amrfinderplus pre-compiled binaries; make /data
RUN mkdir amrfinder && cd /amrfinder && \
    wget https://github.com/ncbi/amr/releases/download/amrfinder_v${AMRFINDER_VER}/amrfinder_binaries_v${AMRFINDER_VER}.tar.gz && \
    tar zxf amrfinder_binaries_v${AMRFINDER_VER}.tar.gz && \
    rm amrfinder_binaries_v${AMRFINDER_VER}.tar.gz && \
    mkdir /data

# install ncbi-blast linux binaries
RUN wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/${BLAST_VER}/ncbi-blast-${BLAST_VER}+-x64-linux.tar.gz && \
    tar -xzf ncbi-blast-${BLAST_VER}+-x64-linux.tar.gz && \
    rm -v ncbi-blast-${BLAST_VER}+-x64-linux.tar.gz

# app
# base image: Ubuntu
FROM ubuntu:jammy as app

# File Author / Maintainer
LABEL base.image="ubuntu:jammy"
LABEL dockerfile.version="1"
LABEL software="ncbi-amrfinderplus"
LABEL software.version="3.11.14"
LABEL description="identify acquired antimicrobial resistance genes"
LABEL website="https://github.com/ncbi/amr"
LABEL license="https://github.com/ncbi/amr/blob/master/LICENSE"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan007@gmail.com"

ARG AMRFINDER_VER="3.11.14"
ARG AMRFINDER_DB_VER="2023-04-17.1"
ARG BLAST_VER="2.14.0"

RUN apt-get update && apt-get install -y --no-install-recommends \
    libgomp1 \
    hmmer \
    procps && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* \
    mkdir /ncbi-blast-${BLAST_VER}+ amrfinder 

COPY --from=builder /ncbi-blast-${BLAST_VER}+/* ncbi-blast-${BLAST_VER}+/

COPY --from=builder amrfinder/* amrfinder/

# set PATH and locale settings for singularity compatibiliity, set amrfinder and manually-installed blast as higher priority in PATH
ENV PATH="/amrfinder:/ncbi-blast-${BLAST_VER}+/bin:$PATH" \
    LC_ALL=C

# set final working directory
WORKDIR /data

