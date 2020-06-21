From ubuntu:18.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt install -y nodejs
RUN git clone https://github.com/open5gs/open5gs
WORKDIR /open5gs/webui
RUN npm install
CMD npm run dev
