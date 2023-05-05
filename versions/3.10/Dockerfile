#########################################################
# Oficial Python Image based in Ubuntu
#########################################################
# Ubuntu Ubuntu 22.04.2 LTS end of life April 2032
FROM ubuntu:jammy
LABEL maintainer="silvio liborio"

ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux

# Define en_US types for the environmet
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_MESSAGES en_US.UTF-8

ENV PYTHON_VERSION=3.10.11

# Update package list
RUN apt-get update && apt-get upgrade -y


##############################################################################
# Install dependencies 
##############################################################################
RUN apt-get install -y \
    apt-transport-https  \
    build-essential  \
    ca-certificates  \
    curl  \
    file \
    gettext \
    git \
    libasound2 \
    libbz2-dev \
    libcurl4-gnutls-dev \
    libexpat1-dev \
    libffi-dev \
    libfontconfig1 \
    libgconf-2-4 \
    libghc-zlib-dev \
    liblzma-dev \
    libncursesw5-dev \
    libnss3 \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    libxi6 \
    libxml2-dev \
    libxmlsec1-dev \
    llvm \
    lsb-release \
    make \
    procps \
    sudo \
    tk-dev \
    unzip \
    wget \
    xvfb \
    xz-utils \
    zip \
    zlib1g-dev \
    sudo \
    software-properties-common \
    jq \
    iputils-ping \
    locales

# Clean up unnecessary files and directories
RUN rm -rf /tmp/* && \
    apt autoremove -y && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*


##############################################################################
# Preparer the user
##############################################################################
RUN adduser ubuntu --disabled-password && usermod -aG sudo ubuntu
RUN echo "ubuntu ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/ubuntu


##############################################################################
# Install a clean and exlusive Python 3.10
##############################################################################
RUN cd /opt && \ 
    wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz && \
    tar -xf Python-$PYTHON_VERSION.tgz && \
    mv Python-$PYTHON_VERSION python && \
    rm Python-$PYTHON_VERSION.tgz && \
    cd python && \
    ./configure --enable-optimizations && \
    make -j$(nproc) && \
    make altinstall

RUN ln -s /usr/local/bin/python3.10 /usr/local/bin/python && \
    ln -s /usr/local/bin/pip3.10 /usr/local/bin/pip

RUN pip install --upgrade pip && \
    pip install yq

##############################################################################
# Final steps
##############################################################################
WORKDIR /home/ubuntu
USER ubuntu

CMD ["bash"]