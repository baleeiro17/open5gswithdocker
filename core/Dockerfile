FROM ubuntu:18.04

RUN apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --no-install-recommends \
        python3-pip \
        python3-setuptools \
        python3-wheel \
        ninja-build \
        build-essential \
        flex \
        bison \
        git \
        meson \
        libsctp-dev \
        libgnutls28-dev \
        libgcrypt-dev \
        libssl-dev \
        libidn11-dev \
        libmongoc-dev \
        libbson-dev \
        libyaml-dev \
        libmicrohttpd-dev \
        libcurl4-gnutls-dev \
        iproute2 \
        ca-certificates \
        netbase \
        pkg-config && \
    apt-get clean

COPY iptables.sh /iptables.sh
RUN chmod +x /iptables.sh
RUN git clone https://github.com/open5gs/open5gs
RUN	cd open5gs && meson build --prefix=`pwd`/install && ninja -C build
RUN cd open5gs/build/ && ninja install
RUN echo $(cd $(dirname ./install/lib/x86_64-linux-gnu/) && pwd -P)/$(basename ./install/lib/x86_64-linux-gnu/) /home/acetcom/Documents/git/open5gs/install/lib/x86_64-linux-gnu
RUN export LD_LIBRARY_PATH=/home/acetcom/Documents/git/open5gs/install/lib/x86_64-linux-gnu
# RUN ldd ./open5gs/install/bin/open5gs-mmed
COPY mme.yaml  /open5gs/install/etc/open5gs/mme.yaml
COPY sgw.yaml  /open5gs/install/etc/open5gs/sgw.yaml
COPY hss.yaml  /open5gs/install/etc/open5gs/hss.yaml   
CMD /iptables.sh ; /open5gs/install/bin/open5gs-pcrfd -D; /open5gs/install/bin/open5gs-pgwd -D; /open5gs/install/bin/open5gs-sgwd -D; /open5gs/install/bin/open5gs-hssd -D; /open5gs/install/bin/open5gs-mmed

