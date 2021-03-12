FROM tomcat:8.5.47-jdk8-openjdk

MAINTAINER Richard Chesterwood "contact@virtualpairprogrammers.com"

EXPOSE 8080
#removing the default tomcat code 
RUN rm -rf ./webapps/* 


#COPY images
COPY target/fleetman-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war

#settting Spring profile 
ENV JAVA_OPTS="-Dspring.profiles.active=docker-demo"

RUN echo -e  "JAVA_OPTS is" $JAVA_OPTS

CMD ["catalina.sh", "run"]