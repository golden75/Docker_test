FROM ubuntu:focal as app

# ARG sets environment variables during the build stage; they do not persist after the image is built
ARG BLAST_VER="2.14.1"


LABEL base.image="ubuntu:focal"
LABEL dockerfile.version="1"
LABEL software="blast"
LABEL software.version=${BLAST_VER}
LABEL description="Finds matches in sequencing reads"
LABEL website="https://blast.ncbi.nlm.nih.gov/Blast.cgi"
LABEL license="https://www.ncbi.nlm.nih.gov/IEB/ToolBox/CPP_DOC/lxr/source/scripts/projects/blast/LICENSE"
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



# LC_ALL for singularity compatibility; set PATH
ENV LC_ALL=C \
    PATH="${PATH}:/ncbi-blast-${BLAST_VER}+/bin"

# set working directory
WORKDIR /data
