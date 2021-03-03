# Docker Images

## Basic Docker image

1. FROM 

It is the used to specify the base image

2. RUN

It is used to run a command into docker container

> Create Dockerfile-base

```code docker
FROM ubuntu:latest
RUN apt-get update && apt-get install -y openjdk-8-jdk
CMD ["/bin/bash"]
```
> EXECUTE COMMAND docker build --no-cache -t base-image -f Dockerfile-base .

----
## COPY command demo

> Create Dockerfile-jdk

```
FROM ubuntu:latest

RUN apt-get update && apt-get install -y openjdk-8-jdk

WORKDIR /usr/local/bin/

COPY ../handsOn/test-program.jar .

ENTRYPOINT ["java", "-jar", "test-program.jar"]
```

> EXECUTE COMMAND - docker build --no-cache -t jdk-image -f Dockerfile-jdk .

>> --no-cache do not use layers from previous image 

> EXECUTE COMMAND - docker build  -t jdk-image -f Dockerfile-jdk .

>  EXECUTE COMMAND - docker run -it jdk-image

---

