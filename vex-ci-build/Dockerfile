FROM ubuntu:18.04
# FROM ghcr.io/base-band/docker-images/verilator-4-016:latest
# Args get erased after FROM

# ARG VERILATOR_VERSION=2825940
# this was verilator_4_016 at some point, I think they redid their tags
# ARG VERILATOR_VERSION=v4.016


ARG DEBIAN_FRONTEND=noninteractive
ENV LC_ALL=C
RUN echo 'export LC_ALL=C' >> /root/.bashrc

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
openjdk-11-jdk \
nano vim iproute2 zip unzip sudo curl make \
&& apt-get autoremove -y && \
apt-get clean

RUN echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
RUN echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | sudo tee /etc/apt/sources.list.d/sbt_old.list
RUN curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
RUN apt-get update && apt-get install -y sbt \
&& apt-get autoremove -y && \
apt-get clean



WORKDIR /src

