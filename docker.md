# Docker

## General 

http://paulbakker.io/docker/docker-osgi/

## Local

In project root dir:

./gradlew clean build skysail.core:export.core.int skysail.core:runnable

cd skysail.core/etc/release

docker build -t evandor/skysail-server .

## Sofia 

  




  


docker rmi $\(docker images -f "dangling=true" -q\)

docker stop $\(docker ps -a -q\)

docker container prune

docker run -ti --rm -p 9102:9102 evandor/skysail-server

docker login

docker push evandor/skysail-server

  


run on sofia:

sudo docker run --name skysail-server -ti --rm -p 9102:9102 evandor/skysail-server:latest

  


access running container on sofia

sudo docker exec -i -t skysail-server /bin/bash

