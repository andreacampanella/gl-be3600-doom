FROM ubuntu:22.04

# Install dependencies
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    git \
    wget \
    curl \
    ca-certificates \
    musl-tools \
    python3 \
    python3-pip \
    bc \
    bison \
    flex \
    libncurses-dev \
    unzip \
    file \
    cpio \
    make \
    sudo \
    rsync \
    gawk \
    pkg-config \
    xz-utils \
    ninja-build \
    cmake \
    clang \
    vim \
    libssl-dev

# Setup musl-cross-make
WORKDIR /opt
RUN git clone https://github.com/richfelker/musl-cross-make.git && \
    cd musl-cross-make && \
    echo "TARGET = aarch64-linux-musl" > config.mak && \
    echo "OUTPUT = /opt/musl-aarch64" >> config.mak && \
    make -j$(nproc) && \
    make install

ENV PATH="/opt/musl-aarch64/bin:$PATH"
ENV CROSS_COMPILE=aarch64-linux-musl-
ENV ARCH=arm64

# Create a working dir
RUN mkdir /build
WORKDIR /build

# Copy BusyBox build script on container start (optional)
CMD ["/bin/bash"]

