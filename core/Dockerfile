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
ADD https://api.github.com/repos/open5gs/open5gs/git/refs/heads/master /root/open5gs-ver.json
RUN	cd open5gs && \
	git fetch && git checkout -f -B master origin/master && \
    meson build && ninja -C build install
COPY mme.yaml  /etc/open5gs/mme.yaml
COPY sgw.yaml  /etc/open5gs/sgw.yaml
COPY hss.yaml  /etc/open5gs/hss.yaml   
CMD iptables.sh ; /usr/bin/open5gs-pcrfd -D; /usr/bin/open5gs-pgwd -D; /usr/bin/open5gs-sgwd -D; /usr/bin/open5gs-hssd -D; /usr/bin/open5gs-mmed

