# steps to execute

## Using Tomcat as a base image from Dockerfile

##### **PRE** Chage `<packaging>war</packaging>` in pom.xml

0. `Go to /01-Docker - Hands On for Java Developers/Resources+v3/Chapter 7 /fleetman-webapp   ` run

> mvn package 

1. Run command

> docker build  -t fleetman-webapp .

2. Get docker IP for **WINDOWS os**

> docker-machine ip

3. RUN Application using

> docker container run -it fleetman-webapp

4. Don't forget to port mapping using -p <hostport>:<DockerPort>

> docker container run -p 8080:8080 -it fleetman-webapp 

5. For testing, open http://localhost:8080/ in browser 

----

## Using jdk as a base image from Dockerfile-jar-version

##### **PRE** Chage `<packaging>jar</packaging>` in pom.xml

0. `Go to /01-Docker - Hands On for Java Developers/Resources+v3/Chapter 7 /fleetman-webapp` run

> mvn package 

1. Run command

> docker build  -t fleetman-webapp-jar -f Dockerfile-jar-version .

2. Get docker IP for **WINDOWS os only**

> docker-machine ip

3. RUN Application using

> docker container run -it fleetman-webapp-jar

4. Don't forget to port mapping using -p <hostport>:<DockerPort>

> docker container run -p 8080:8080 -it fleetman-webapp-jar

5. For testing, open http://localhost:8080/ in browser 