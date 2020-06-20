FROM ubuntu:18.04

RUN apt-get update
RUN apt-get -y install software-properties-common
RUN add-apt-repository ppa:open5gs/latest
RUN apt-get update
RUN apt-get -y install open5gs
RUN apt-get -y install curl
RUN apt-get -y install iptables
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get -y install nodejs
RUN curl -sL https://open5gs.org/open5gs/assets/webui/install | bash -
COPY mme.yaml  /etc/open5gs/mme.yaml
COPY sgw.yaml  /etc/open5gs/sgw.yaml
COPY exec.sh /exec.sh
COPY iptables.sh /iptables.sh
RUN chmod +x /exec.sh
RUN chmod +x /iptables.sh
CMD iptables.sh ; exec.sh 