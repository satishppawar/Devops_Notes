# Docker Images and instruction

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

COPY test-program.jar .

ENTRYPOINT ["java", "-jar", "test-program.jar"]
```

> EXECUTE COMMAND - docker build --no-cache -t jdk-image -f Dockerfile-jdk .

>> --no-cache do not use layers from previous image 

> EXECUTE COMMAND - docker build  -t jdk-image -f Dockerfile-jdk .

>  EXECUTE COMMAND - docker run -it jdk-image
### COPY vs ADD

- ADD works with remote URL and it can have extra capabilities such as unzip etc.

- COPY is recommended by docker as it is simple

### ENTRYPOINT vs CMD

- `ENTRYPOINT` will always run whereas 
- `CMD` is just defult command in container and it can be overwritten

> create Dockerfile-cmd

```docker
FROM ubuntu:latest

RUN apt-get update && apt-get install -y openjdk-8-jdk

WORKDIR /usr/local/bin/

COPY test-program.jar .

CMD ["java", "-jar", "test-program.jar"]
```

-----

> EXECUTE COMMAND
>> docker build  -t docker-cmd-image -f Dockerfile-cmd .
>> docker run -it docker-cmd-image

> EXECUTE COMMAND
>> docker build  -t docker-cmd-image -f Dockerfile-cmd .

>> docker run -it docker-cmd-image /bin/bash

>  EXECUTE COMMAND - docker run -it jdk-image /bin/bash
>> `jdk-image` uses ENTRYPOINT, /bin/bash can not be executed

**NOTE -**  CMD is default command and it can be overwritten where as ENTRYPOINT can not be overwritten, and ENTRYPOINT will always run even if we overwrite with other commands


---

MAINTAINER vs LABLE

- `MAINTAINER` is deprecated

- `LABEL` is flexible version and user key and value. we can add maintainer using LABEL

e.g LABEL maintainer="Satish"

LABEL date="02.03.2021"

> Create docker-label file 
```docker

FROM ubuntu:latest
LABEL version="1.0"
LABEL maintainer="Satish"
LABEL date="02.03.2021"
LABEL key="value"
RUN apt-get update && apt-get install -y openjdk-8-jdk
WORKDIR /usr/local/bin/
COPY test-program.jar .
CMD ["java", "-jar", "test-program.jar"]
```
> EXECUTE COMMAND
>> docker build  -t docker-label-image -f Dockerfile-label .

---
### EXPOSE instruction

- specify/informs docker that container listens on the specified network ports at runtime.