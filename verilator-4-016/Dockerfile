FROM ubuntu:18.04
# Args get erased after FROM

# ARG VERILATOR_VERSION=2825940
# this was verilator_4_016 at some point, I think they redid their tags
ARG VERILATOR_VERSION=v4.016


ARG DEBIAN_FRONTEND=noninteractive

# Top 3 lines are boilerplate
# next, after the break are a list of general reqs
# next, are reqs for riscv
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
libgmp-dev libusb-1.0-0-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev device-tree-compiler \
pkg-config git libexpat1-dev libncurses-dev \
\
python gdb \
\
&& apt-get autoremove -y && \
apt-get clean

RUN git clone https://github.com/verilator/verilator /tmp/verilator && \
cd /tmp/verilator && \
git checkout $VERILATOR_VERSION && \
git submodule update --init --depth 1

RUN cd /tmp/verilator && autoconf && ./configure && make -j2 && make install



#################### 
# Riscv Compiler


RUN git clone https://github.com/riscv/riscv-tools.git /tmp/riscv-tools && \
cd /tmp/riscv-tools && \
git checkout ef03b6a70d9baa03943661bce37b9f70ad36f706 && \
git submodule update --init --recursive && \
export RISCV=/opt/riscv && \
mkdir -p $RISCV && \
./build-rv32ima.sh


RUN ls /opt
RUN ls /opt/riscv


ENV RISCV=/opt/riscv
RUN echo 'export RISCV=/opt/riscv' >> /root/.bashrc


#################### 
# ZeroMQ, needed by final application

RUN cd /tmp && \
git clone https://github.com/zeromq/libzmq && cd libzmq && \
./autogen.sh && ./configure && make -j 2 && \
make check && make install && ldconfig

WORKDIR /src

