## OAISIM + Open5gs with Docker.

## Project Description

In this repository, we developed an environment for simulating UE and ENB using l2NFAPI simulator from Open Air interface connected into 4g core from open5gscore. This work is on-going.

For more information:
* [Open5gs](https://open5gs.org/)
* [Open Air Interface](https://www.openairinterface.org/)


## Dependencies

* [Docker](https://docs.docker.com/install/)
* [Docker Compose](https://docs.docker.com/compose/install/)


Each box of project is based on a compiled oaisim image. To build this image use the follow command:
``cd oaisim-base sudo docker build -t oaisim-base  .``


## Running
To run all boxes and Web interface use the follow command:
``sudo docker-compose up -d``
