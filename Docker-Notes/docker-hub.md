# Docker Hub

## Pre-requisite

- Create a accout for docker-hub

## Push Images to docker hub

1. Docker login

> docker login

2. Tag Docker Image using `docker image tag <original-image-name> <tagged-image-name>`

> docker image tag fleetman-webapp-jar pawarsatish/test

3. Docker push

> docker image push pawarsatish/test