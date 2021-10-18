# FROM ubuntu:18.04
FROM ghcr.io/base-band/docker-images/verilator-4-016:latest
# Args get erased after FROM

# ARG VERILATOR_VERSION=2825940
# this was verilator_4_016 at some point, I think they redid their tags
ARG VERILATOR_VERSION=v4.016


ARG DEBIAN_FRONTEND=noninteractive

# Top 3 lines are boilerplate
# next, after the break are a list of general reqs
# next, are reqs for riscv
# next are reqs for lattice
# next are needed by final repo / code
# final 2 lines are boilerplate to cleanup

RUN apt-get update && apt-get install apt-utils software-properties-common -y && \
apt-get upgrade -y && \
add-apt-repository -y ppa:git-core/ppa && \
apt-get update && apt-get install -y \
\
cmake make wget unzip tar build-essential python3 python3-pip git \
flex bison autoconf \
\
autoconf automake autotools-dev curl libmpc-dev libmpfr-dev \
libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev \
pkg-config libexpat1-dev libncurses-dev \
\
python \
nano ssh x11-apps vim iproute2 zip unzip expect \
&& apt-get autoremove -y && \
apt-get clean



#################### 
# Quartus

RUN mkdir -p /root/builds/quartus-lite-20.1.1

ADD qinstall.sh /root/builds/quartus-lite-20.1.1

RUN chmod +x /root/builds/quartus-lite-20.1.1/qinstall.sh

RUN cd /root/builds/quartus-lite-20.1.1 && wget -nv https://download.altera.com/akdlm/software/acdsinst/20.1std.1/720/ib_tar/Quartus-lite-20.1.1.720-linux.tar && tar -xf Quartus-lite-20.1.1.720-linux.tar && rm -rf Quartus-lite-20.1.1.720-linux.tar

RUN cd /root/builds/quartus-lite-20.1.1/ && ./qinstall.sh


ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL=C

RUN echo "X11DisplayOffset 10" >> /etc/ssh/sshd_config && \
echo "X11UseLocalhost no" >> /etc/ssh/sshd_config && \
mkdir -p /root/.ssh && touch /root/.ssh/authorized_keys

RUN echo 'export LC_ALL=C' >> /root/.bashrc






WORKDIR /src

