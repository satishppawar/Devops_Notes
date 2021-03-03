# Docker Images

## Basic Docker image

1. FROM 

It is the used to specify the base image

2. RUN

It is used to run a command into docker container

> 

```code docker

MAINTAINER satish pawar

FROM ubuntu: latest

RUN apt-get update && apt-get install -y openjdk-8-jdk

CMD ["/bin/bash"]

```