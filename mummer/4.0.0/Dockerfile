# builder
FROM ubuntu:jammy as app

# ARG sets environment variables during the build stage; they do not persist after the image is built
ARG MUMMER_VER="4.0.0"
ARG MASH_VER="2.3"

LABEL base.image="ubuntu:jammy"
LABEL dockerfile.version="1"
LABEL software="mummer"
LABEL software.version=${MUMMER_VER}
LABEL description="MUMmer is a versatile alignment tool for DNA and protein sequences."
LABEL website="https://github.com/mummer4/mummer"
LABEL license="https://github.com/mummer4/mummer/blob/master/LICENSE.md"
LABEL maintainer="Neranjan Perera"
LABEL maintainer.email="neranjan007@gmail.com"

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

# install mummer; make /data for use as working directory
RUN wget https://github.com/mummer4/mummer/releases/download/v${MUMMER_VER}rc1/mummer-${MUMMER_VER}rc1.tar.gz; \
    tar -xvf mummer-${MUMMER_VER}rc1.tar.gz; \
    rm mummer-${MUMMER_VER}rc1.tar.gz; \
    cd mummer-${MUMMER_VER}rc1; \
    ./configure && \
    make && \
    make install; \
    ldconfig; \
    cd ..; \
    mkdir /data

# install ncbi datasets tool (pre-compiled binary); place in $PATH
RUN wget https://ftp.ncbi.nlm.nih.gov/pub/datasets/command-line/LATEST/linux-amd64/datasets; \
    chmod +x datasets; \
    mv -v datasets /usr/local/bin

# downloading mash binary
RUN wget https://github.com/marbl/Mash/releases/download/v${MASH_VER}/mash-Linux64-v${MASH_VER}.tar; \
    tar -xvf mash-Linux64-v${MASH_VER}.tar; \
    rm -rf mash-Linux64-v${MASH_VER}.tar

# download Lee's ani-m script
RUN wget https://github.com/lskatz/ani-m/archive/refs/tags/v0.1.tar.gz; \
    tar xzf v0.1.tar.gz; \
    rm -v v0.1.tar.gz

ENV PATH="${PATH}:/ani-m-0.1:/mash-Linux64-v${MASH_VER}" \
    LC_ALL=C

# set working directory
WORKDIR /data
