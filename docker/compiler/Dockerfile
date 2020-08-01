FROM ubuntu:18.04

RUN apt-get update && apt-get -y install sudo git automake g++ libncurses5-dev \
  subversion libssl-dev gawk libxml-parser-perl unzip wget build-essential python \
  build-essential libtool lsb-release make cmake ninja-build iproute2 exuberant-ctags \
  rsync software-properties-common

RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

RUN mkdir /src
RUN usermod -u 1000 docker
RUN chown -R docker:docker /src
WORKDIR /src


