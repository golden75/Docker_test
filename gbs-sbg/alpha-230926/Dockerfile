FROM ubuntu:focal as app

# ARG sets environment variables during the build stage; they do not persist after the image is built
ARG BLAST_VER="2.14.1"
ARG GBS_SBG_VER="alpha-230926"


LABEL base.image="ubuntu:focal"
LABEL dockerfile.version="1"
LABEL software="blast"
LABEL software.version=${GBS_SBG_VER}
LABEL description="serotyping Streptococcus agalactiae or GBS"
LABEL website1="https://blast.ncbi.nlm.nih.gov/Blast.cgi"
LABEL license1="https://www.ncbi.nlm.nih.gov/IEB/ToolBox/CPP_DOC/lxr/source/scripts/projects/blast/LICENSE"
LABEL website2="https://github.com/swainechen/GBS-SBG"
LABEL license2="https://github.com/swainechen/GBS-SBG/blob/main/LICENSE"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan007@gmail.com"


# to prevent tzdata from asking for a region during apt updates
ARG DEBIAN_FRONTEND=noninteractive

# Install dependencies via apt; clean up apt garbage
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    libncurses5-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    zlib1g-dev \
    libssl-dev \
    gcc \
    make \
    perl \
    bzip2 \
    gnuplot \
    ca-certificates \
    gawk \
    curl \
    sed \
    build-essential \
    unzip && \
    apt-get autoclean && rm -rf /var/lib/apt/lists/*

# install blast; make /data for use as working directory
RUN wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.14.1/ncbi-blast-${BLAST_VER}+-x64-linux.tar.gz && \
    tar -xvf ncbi-blast-${BLAST_VER}+-x64-linux.tar.gz && \
    rm ncbi-blast-${BLAST_VER}+-x64-linux.tar.gz && \
    mkdir /data

RUN git clone https://github.com/swainechen/GBS-SBG

# LC_ALL for singularity compatibility; set PATH
ENV LC_ALL=C \
    PATH="${PATH}:/ncbi-blast-${BLAST_VER}+/bin:/GBS-SBG"

# set working directory
WORKDIR /data
