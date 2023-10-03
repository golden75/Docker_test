FROM ubuntu:xenial as app

# ARG sets environment variables during the build stage; they do not persist after the image is built
# Main package version
ARG SRST2_VER=0.2.0

# Dependency versions
ARG BOWTIE2_VER=2.2.6-2
ARG SAMTOOLS_VER=0.1.18

LABEL base.image="ubuntu:focal"
LABEL dockerfile.version="1"
LABEL software="SRST2"
LABEL software.version="v0.2.0"
LABEL description="Short Read Sequence Typing for Bacterial Pathogens GBS"
LABEL website1="https://github.com/katholt/srst2"
LABEL license1="https://github.com/katholt/srst2/blob/master/LICENSE.txt"
LABEL website2="https://github.com/swainechen/GBS-SBG"
LABEL license2="https://github.com/swainechen/GBS-SBG/blob/main/LICENSE"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan007@gmail.com"


# to prevent tzdata from asking for a region during apt updates
# ARG DEBIAN_FRONTEND=noninteractive

# Install dependencies via apt; clean up apt garbage
RUN apt-get update && apt-get install -y --no-install-recommends \
    python2.7 \
    python-scipy \
    python-biopython \
    make \
    libc6-dev \
    g++ \
    zlib1g-dev \
    build-essential \
    git \
    libx11-dev \
    xutils-dev \
    zlib1g-dev \
    bowtie2=${BOWTIE2_VER} \
    curl \
    libncurses5-dev \
    unzip \
    wget  \
    locate \
    python-pip \
    python-setuptools && \
    apt-get autoclean && rm -rf /var/lib/apt/lists/*

# download samtools source code; unzip; compile; put executable in /usr/local/bin
RUN curl -O -L https://sourceforge.net/projects/samtools/files/samtools/${SAMTOOLS_VER}/samtools-${SAMTOOLS_VER}.tar.bz2 && \
    tar -xjf samtools-${SAMTOOLS_VER}.tar.bz2 && \
    rm samtools-${SAMTOOLS_VER}.tar.bz2 && \
    cd samtools-${SAMTOOLS_VER} && \
    make && \
    cp -v samtools /usr/local/bin 

# Install SRST2; make /data
RUN pip install biopython git+https://github.com/katholt/srst2.git@v${SRST2_VER} && \
    mkdir /data

# add custom database to /gbs-db directory, make readable to all 
# https://github.com/swainechen/GBS-SBG/blob/main/GBS-SBG.fasta
ADD GBS-SBG.fasta /gbs-db/

# index custom database in /vibrio-cholerae-db directory; ensure files are readable to all users
RUN bowtie2-build /gbs-db/GBS-SBG.fasta /gbs-db/GBS-SBG.fasta; \
    samtools faidx /gbs-db/GBS-SBG.fasta; \
    chmod -R 755 /gbs-db

# LC_ALL for singularity compatibility; set PATH
ENV LC_ALL=C 

# set working directory
WORKDIR /data
