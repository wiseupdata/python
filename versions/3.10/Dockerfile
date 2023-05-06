#########################################################
# Oficial Python Image based in Ubuntu
#########################################################
# Ubuntu Ubuntu 22.04.2 LTS end of life April 2032
FROM ubuntu:jammy
LABEL maintainer="silvio liborio"


###############################################################################
RUN echo "Initial setup and envs" 
##############################################################################

ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux

# Define en_US types for the environmet
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_MESSAGES en_US.UTF-8
ENV PYTHON_VERSION=3.10.11

RUN echo "Clean up unnecessary files and directories"

RUN rm -rf /tmp/* && \
    apt autoremove -y && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/*
    

RUN apt-get update && apt-get upgrade


##############################################################################
RUN echo "Installing essential packages"
##############################################################################
# apt-transport-https: Allows apt-get to use HTTPS transport.
# ca-certificates: Provides a bundle of CA certificates to verify SSL connections.
# curl: A tool to transfer data from or to a server.
# file: A utility to determine file type.
# gettext: A package to internationalize and localize messages.
# git: A distributed version control system.
# make: A build automation tool.
# procps: Provides process information utilities.
# sudo: Allows users to run programs with the security privileges of another user.
# bash: The GNU Bourne Again shell.
# libc6: The standard C library.
# libpam-modules: Pluggable Authentication Modules for the Linux PAM (Pluggable Authentication Modules) library.
# libnss3: A set of libraries designed to support cross-platform development of security-enabled client and server applications.
# gosu: A tool to run a command as another user.
# libsecret-1-dev: A library to store and retrieve passwords and other secrets.
# libx11-dev: A library for X Window System communication.
# libxkbfile-dev: A library to handle keyboard descriptions in X.Org.
# gnupg2: Provides cryptographic functions for secure communication.
# build-essential: Contains essential packages required for building Debian packages.

RUN set -ex && apt-get install -y apt-transport-https ca-certificates curl file gettext git make procps sudo bash libc6 libpam-modules libnss3 procps gosu  libsecret-1-dev libx11-dev libxkbfile-dev gnupg2 build-essential


##############################################################################
RUN echo "Installing required packages for most applications"
##############################################################################
# libbz2-dev: Development files for the bzip2 compression library.
# libcurl4-gnutls-dev: Development files and documentation for libcurl (GnuTLS flavour).
# libexpat1-dev: Development files for the XML parsing library.
# libffi-dev: Development files for libffi, a library that provides a high-level interface for calling C functions.
# libfontconfig1: Font configuration and customization library.
# liblzma-dev: Development files for the XZ compression library.
# libncursesw5-dev: Development files for the ncurses library.
# libreadline-dev: Development files for the GNU readline library.
# libsqlite3-dev: Development files for the SQLite3 library.
# libssl-dev: Development files for the OpenSSL library.
# libxml2-dev: Development files for the libxml2 library.
# libxmlsec1-dev: Development files for the XML security library.
# llvm: A collection of modular and reusable compiler and toolchain technologies.
# unzip: A tool to extract compressed files in a ZIP archive format.
# wget: A tool to download files from the Internet.
# xvfb: A virtual X server used for headless testing.
# xz-utils: A set of compression utilities using the LZMA algorithm.
# zip: A tool to compress files in a ZIP archive format.
# zlib1g-dev: Development files for the zlib data compression library.
# tini: A tiny but valid init for containers.
# krb5-user is a package that installs the Kerberos client programs, including kinit, klist, kpasswd, and kdestroy. Kerberos is a network authentication protocol designed to provide strong authentication for client/server applications by using secret-key cryptography. The krb5-user package is required if you need to authenticate your application with a Kerberos server.
# GCC stands for GNU Compiler Collection and is a set of compilers for programming languages, including C, C++, and Fortran. It is a popular and widely used tool for compiling and building software on various platforms.
# lsb-release is a command that provides information about the Linux Standard Base (LSB) version and distribution of a Linux system. It is commonly used to check the version of a Linux distribution for compatibility with software packages.

RUN set -ex && apt-get install -y libbz2-dev libcurl4-gnutls-dev libexpat1-dev libffi-dev libfontconfig1 liblzma-dev libncursesw5-dev libreadline-dev libsqlite3-dev libssl-dev libxml2-dev libxmlsec1-dev llvm unzip wget xvfb xz-utils zip zlib1g-dev tini krb5-user gcc lsb-release


##############################################################################
RUN echo "Installing usefull packages"
##############################################################################
# locales: Allows for localization of the system's language and character encoding settings.
# iputils-ping: Includes the ping command for testing network connectivity.
# jq: A command-line JSON processor.
# net-tools: Contains various networking tools.

RUN set -ex && apt-get install -y locales iputils-ping jq net-tools


##############################################################################
RUN echo "Preparering Ubuntu user"
##############################################################################

RUN adduser ubuntu --disabled-password && usermod -aG sudo ubuntu
RUN echo "ubuntu ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/ubuntu


##############################################################################
RUN echo "Installing a clean and exlusive Python 3.10 - Official"
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

RUN pip install --upgrade pip


##############################################################################
RUN echo "Installing usefull packages for the system using Python"
##############################################################################

RUN pip install yq


##############################################################################
RUN echo "Final steps"
##############################################################################

RUN rm -rf /tmp/* && \
    apt autoremove -y && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apt/*

WORKDIR /home/ubuntu
USER ubuntu

CMD ["bash"]