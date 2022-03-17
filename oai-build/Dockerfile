FROM ubuntu:bionic-20220301
MAINTAINER Ben


# Required for some packages to install
ENV DEBIAN_FRONTEND noninteractive

# apt-get clean autoclean
# only need to run clean, as it is a superset of autoclean

RUN apt-get update && apt-get -yq install \
software-properties-common apt-utils && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get -yq install \
apt-file && \
apt-get clean && \
apt-file update && \
rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get -yq install \
apt-utils \
autoconf \
automake \
bison \
build-essential \
ccache \
check \
cmake \
cpufrequtils \
ctags \
dialog \
dkms \
doxygen \
doxygen-gui \
entr \
ethtool \
flex \
fort77 \
g++ \
gawk \
gdb \
git \
git-core \
graphviz \
gtk2-engines-pixbuf \
gtkwave \
guile-2.0-dev \
iperf \
iproute2 \
iptables \
iptables-dev \
libasound2-dev \
libatlas-base-dev \
libblas-dev \
libboost-all-dev \
libcomedi-dev \
libcppunit-1.14-0 \
libcppunit-dev \
libcppunit-doc \
libffi-dev \
libfftw3-bin \
libfftw3-dev \
libfftw3-doc \
libfontconfig1-dev \
libforms-bin \
libforms-dev \
libgcrypt11-dev \
libgmp-dev \
libgsl-dev \
libgtk-3-dev \
libidn11-dev \
libidn2-0-dev \
libmysqlclient-dev \
libncurses5 \
libncurses5-dbg \
libncurses5-dev \
liboctave-dev \
liborc-0.4-0 \
liborc-0.4-dev \
libpgm-dev \
libpthread-stubs0-dev \
libpulse-dev \
libqt4-dev \
libqt4-dev-bin \
libqwt5-qt4-dev \
libqwt6abi1 \
libqwtplot3d-qt5-dev \
libsctp1 \
libsctp-dev \
libsdl1.2-dev \
libssl-dev \
libtasn1-dev \
libtool \
libudev-dev \
libusb-1.0-0 \
libusb-1.0-0-dev \
libusb-dev \
libxi-dev \
libxml2 \
libxml2-dev \
libxrender-dev \
libxslt1-dev \
libzmq3-dev \
mscgen \
nano \
ncurses-bin \
ntpdate \
octave \
octave-signal \
openssh-client \
openssh-server \
openssl \
openvpn \
pkg-config \
pydb \
pyqt4-dev-tools \
python \
python3 \
python3-mako \
python3-pip \
python3-requests \
python3-setuptools \
python-cheetah \
python-dev \
python-docutils \
python-gtk2 \
python-lxml \
python-mako \
python-numpy \
python-numpy-dbg \
python-numpy-doc \
python-opengl \
python-pexpect \
python-pip \
python-qt4 \
python-qt4-dbg \
python-qt4-dev \
python-qt4-doc \
python-qwt5-qt4 \
python-requests \
python-scipy \
python-setuptools \
python-sphinx \
python-tk \
python-wxgtk3.0 \
python-zmq \
qt4-bin-dbg \
qt4-default \
qt4-dev-tools \
qt4-doc \
r-base-dev \
sshfs \
sshpass \
subversion \
sudo \
swig \
texlive-latex-base \
tshark \
uml-utilities \
unzip \
valgrind \
vim-common \
vlan \
wget \
wvdial \
xmlstarlet && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

RUN mkdir -p /root/builds

# RUN cd /root/builds && git clone https://gitlab.eurecom.fr/oai/asn1c.git && cd asn1c && git checkout 224dc1f && \
# ./configure && make -j4 && make install


# origin	https://gitlab.eurecom.fr/oai/openairinterface5g.git (fetch)
# * develop                                                                   595dd27ab0 [origin/develop] Configure only one address for asterix's N310


RUN cd /root/builds && git clone https://gitlab.eurecom.fr/oai/openairinterface5g.git && cd openairinterface5g && git checkout 595dd27ab0

RUN apt-get update

# installed by build_oai with -I
RUN apt-get install -y libtasn1-6-dev libgnutls28-dev iproute2 libconfig-dev autoconf automake bison build-essential cmake cmake-curses-gui curl ninja-build doxygen doxygen-gui texlive-latex-base ethtool flex gdb git graphviz gtkwave guile-2.0-dev iperf iptables iptables-dev libatlas-base-dev libblas-dev liblapack-dev liblapacke-dev libffi-dev libforms-bin libforms-dev libgcrypt11-dev libgmp-dev libgtk-3-dev libidn2-0-dev libidn11-dev libmysqlclient-dev libpython2.7-dev libreadline-dev libsctp1 libsctp-dev libssl-dev libtool libusb-1.0-0-dev libxml2 libxml2-dev libxslt1-dev octave-signal openssh-client openssh-server openssl python subversion xmlstarlet python-pip pydb libyaml-dev wget libxpm-dev libboost-all-dev
RUN apt-get install -y nettle-dev nettle-bin

# RUN cd /root/builds/openairinterface5g/ && which bash
RUN cd /root/builds/openairinterface5g/ && /bin/bash oaienv && cd /root/builds/openairinterface5g/cmake_targets && \
./build_oai -I

RUN cd /root/builds/openairinterface5g/ && /bin/bash oaienv && cd /root/builds/openairinterface5g/cmake_targets && \
./build_oai --eNB --UE --verbose-compile

# ./build_oai -I --eNB --UE --verbose-compile


# ./build_oai -I --phy_simulators --verbose-compile
# ./build_oai -w USRP --eNB --UE --verbose-compile
# ./build_oai --eNB --UE --verbose-compile



# -I | --install-external-packages
#    Installs required packages such as LibXML, asn1.1 compiler, freediameter, ...
#    This option will require root password
# --install-optional-packages
#    Install useful but not mandatory packages such as valgrind
# -i | --install-system-files
#    Install OpenAirInterface required files in Linux system
#    This option will require root password
# -g | --run-with-gdb <Release | RelWithDebInfo | MinSizeRel | Debug
#   specify the build mode used by cmake. defaults to Debug mode if -g is used alone, with no mode parameter
#   if -g is not specifies, Release mode is used.
# -G | --cmaketrace
#    enable cmake debugging messages
# --eNB
#   Makes the LTE softmodem
# --eNBocp
#   Makes the OCP LTE softmodem
# --gNB
#   Makes the NR softmodem



# cat /var/log/apt/history.log