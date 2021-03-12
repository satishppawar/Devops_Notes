# Docker Services

## Usecase - Adding DB service to application

- By default, single Docker image only exposed one service. 

- If we need to add multiple services inside the single docker image, we might add additional required services as daemon service. This is not recommended

- [Why can't I use Docker CMD multiple times to run multiple services?
](https://stackoverflow.com/questions/23692470/why-cant-i-use-docker-cmd-multiple-times-to-run-multiple-services#:~:text=At%20all%20times%2C%20there%20can%20be%20only%20one%20CMD.&text=You%20are%20right%2C%20the%20second,specify%20one%20command%20to%20run.)


- [DOCKERFILE: Running multiple CMD. (Starting NGINX and PHP) [duplicate]
](https://stackoverflow.com/questions/49630960/dockerfile-running-multiple-cmd-starting-nginx-and-php?noredirect=1&lq=1)

- It is possible to add multiple services to single container image. But,this is not recommended. Because, there are different problems
    - Start time will be more
    - Will need continuous health checks.
    -  Hard to manage, build ,test, run

- As a `Best Practise` in docker, a `container shold only expose and run single services`. Think microservice arch.
    - Easy to manage, build ,test, run

