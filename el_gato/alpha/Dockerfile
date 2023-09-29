FROM ubuntu:focal as app

# ARG sets environment variables during the build stage; they do not persist after the image is built
ARG EL_GATO_VER="alpha"

LABEL base.image="ubuntu:focal"
LABEL dockerfile.version="1"
LABEL software="el_gato"
LABEL software.version=${EL_GATO_VER}
LABEL description="Legionella Genome based Typying"
LABEL website="https://github.com/jennahamlin/el_gato"
LABEL license="https://github.com/jennahamlin/el_gato/blob/main/LICENSE"
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
    curl \
    sed \
    build-essential \
    unzip && \
    apt-get autoclean && rm -rf /var/lib/apt/lists/*

# install mummer; make /data for use as working directory
RUN mkdir -p ~/miniconda3;\
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh; \
    bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3; \
    rm -rf ~/miniconda3/miniconda.sh; \
    ~/miniconda3/bin/conda init bash; \
    conda create -n elgato -c bioconda -c conda-forge -c appliedbinf elgato


# LC_ALL for singularity compatibility; set PATH
ENV LC_ALL=C

# set working directory
WORKDIR /data
