# Docker

## Installation

- Easy way to get started with docker is to install Docker Destop app. Need to install docker-compose separately if you are using linux, latest version of desktop app have an option to do just that in settings. 

  

## commands

- `docker run nginx` If the image already exists then runs the image/container. if there is no image it downloads from hub
- `docker ps` list out running containers
- `docker ps -a`   - List out all running containers
- `docker stop dockername`
- `docker rm dockername` to remove a container permanently
- `docker images` list out downloaded images
- `docker rmi nginx` to remove an image. make sure there are no running containers off that image.
- `docker pull nginx` to only pull the image from hub and not run.

- We can run docker from terminal in either attached or detached mode
  - Detached mode  `docker run -d nginx`
  - start in attach mode with `-d` flag or attach to an already running container using its hash `docker attach hash`



### Build 

`docker build -t username/app-name`

Running with port forwarding

`docker run -p LOCAL_PORT:CONTAINER_PORT imageID`



### Docker compose

- https://docs.docker.com/compose/

`docker-compose build`

`docker-compose up`

`docker-compose down`





### useful links

- https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

- [docker-compose nodejs and mongodb - bezkoder](https://www.bezkoder.com/docker-compose-nodejs-mongodb/)
- https://www.youtube.com/watch?v=hP77Rua1E0c

- Example docker-compose.mongo.yml https://gist.github.com/gterdem/ac5b0f135fba034333dd4597edd2e278
- [react-express-mongodb-docker](https://www.freecodecamp.org/news/create-a-fullstack-react-express-mongodb-app-using-docker-c3e3e21c4074/)
- https://linuxhandbook.com/remove-docker-images/\
- https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
- https://auth0.com/blog/use-docker-to-create-a-node-development-environment/

