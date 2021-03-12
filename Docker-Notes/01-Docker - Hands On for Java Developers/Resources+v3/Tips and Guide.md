### ERRATA: You will need some extra config

Recently I've upgraded the sample project to use Spring Boot 2, so that the code can be compiled on modern JDKs from version 9 onwards.

One slight problem is that Spring Boot 2 now uses a different connection pool implementation by default. In order to stay backwards compatible with the MySQL5 that we're using on the course, you will need to add a further property to the application-docker-demo.properties file:

spring.datasource.driver-class-name=com.mysql.jdbc.Driver

Just add this after the username, password etc. If you get any connection problems, double check you've got this line correct!