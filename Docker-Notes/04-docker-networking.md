# Docker Networking

## Containers and DNS

### Creating MySql Container

### Create mysql container

> docker run -e MYSQL_ROOT_PASSWORD=password -d mysql:5

- Verify the mysql 

> docker container exec -it <mysql-container-id> sh

> mysql -uroot -ppassword

> mysql>show databases;

### Using mysql in fleetman app

> docker run -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=fleetman -d mysql:5

Try to ping to another mysql container created in above step from this one and it will not work.
Howerver, ping to google.com, it will work. To enable communication between different containers, we need to create a network and put container in the same network

### Docker Networking

- To enable communication between different containers, we need to create a network and put container in the same network

#### Commands - docker network

- list the networks

> docker network ls

- Creating a new network

> docker network create my-network

- Creating container using the network

> docker run --network my-network --name database -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=fleetman -d mysql:5

##### Demo

> docker run -d -p 80:8080 --network my-network --name fleetman-webapp
> docker container exec -it fleetman-webapp sh
> ping google.com
> ping database

-----
## Fleetman App HandsOn 

- Refer `/Docker-Notes/01-Docker - Hands On for Java Developers/Resources+v3/Chapter 7/fleetman-webapp-networking/Execution-guide.md`

- Edit `Docker-Notes/01-Docker - Hands On for Java Developers/Resources+v3/Chapter 7/fleetman-webapp-networking/src/main/resources/application-docker-demo.properties` as

```

#Re-enable for the full microservice version
spring.cloud.discovery.enabled=false

spring.jpa.properties.hibernate.hbm2ddl.auto=update
security.basic.enabled=false

spring.datasource.url=jdbc:mysql://database:3306/fleetman
spring.datasource.username=root
spring.datasource.password=password

logging.level.org.springframework=INFO
```

- Docker container list

> docker container ls
> docker container stop fleetman-webapp

-Build project from  ` Hands On for Java Developers/Resources+v3/Chapter 7/fleetman-webapp-networking/`

> mvn clean package

- Rebuild the image, go to `01-Docker - Hands On for Java Developers/Resources+v3/Chapter 7/fleetman-webapp-networking/Dockerfile-jar-version`

> docker rmi fleetman-webapp
> docker image build -t fleetman-webapp -f Dockerfile-jar-version .

- Run appplications

> docker container run -d -p 8080:8080 --network my-network --name fleetman-webapp --rm fleetman-webapp 

- check logs

>  docker container logs -f fleetman-webapp

- Verify Db

> docker container run -it --network my-network alpine
> apk add --no-cache mysql-client
> apk update mysql
> mysql -uroot -ppassword -hdatabase
> show databases;
> use fleetman;
> show tables;
> use fleetman;
> select * from vehicle;

----
