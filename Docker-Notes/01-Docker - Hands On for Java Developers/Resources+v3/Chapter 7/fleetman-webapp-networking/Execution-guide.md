# steps to execute

- Edit `Docker-Notes/01-Docker - Hands On for Java Developers/Resources+v3/Chapter 7/fleetman-webapp-networking/src/main/resources/application-docker-demo.properties` as

```


#Re-enable for the full microservice version
spring.cloud.discovery.enabled=false

spring.jpa.properties.hibernate.hbm2ddl.auto=update
security.basic.enabled=false

spring.datasource.url=jdbc:mysql://database:3306/fleetman
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.jdbc.Driver

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