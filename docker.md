# Docker



## Installation

- Easy way to get started with docker is to install Docker Destop app. Need to install docker-compose separately if you are using linux, latest version of desktop app have an option to do just that in settings. 

  

## commands

- `docker run nginx` If the image already exists then runs the image/container. if there is no image it downloads from hub
- `docker ps` list out running containers
- `docker ps -a`   - List out all running containers
- `docker stop dockername`
- `docker rm dockername` to remove a container
  - `docker rm containerName -f`  Used to forcefully remove (stop a running container and then remove). 

- `docker images`  or `docker image ls` list out downloaded images
- `docker rmi nginx` to remove an image. make sure there are no running containers off that image.
- `docker pull nginx` to only pull the image from hub and not run.

- We can run docker from terminal in either attached or detached mode
  - Detached mode  `docker run -d nginx`  so that your terminal is free and open to input/run other commands.
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



## Docker with NodeJs

### Dockerfile

```
FROM node:16 

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . ./

## EXPOSE command is just for documentation, it actually does nothing. 
## Its just to explicitly show that we like to port forwarding to this port.
EXPOSE 3000

## CMD ["npm", "start"] to run on production

## After using bind volumes to restart the server using npm script which runs nodemon
CMD ["npm", "run", "dev"]
```

- cd into the root folder where Dockerfile resides and to build the docker image run `docker build .`   View the image using `docker image ls`
- To build an image with a name, run `docker build -t node-app-image .`
- Create a container using a given image by 
  - `docker run node-app-image` . Here node-app-image is the name of image we created earlier.
  - `docker run -d --name node-app node-app-image` Here using --name flg to name this container. `-d` flag to run in detached mode
  - `docker run -p 8080:3000 -d --name node-app node-app-image` Here -p flag for forwarding 3000 which is docker container's port to 8080 which is localhost machines port or outside port.
- Note: Your docker container can have access to outside ports ( meaning not just internet but also local host machine) but outside ports cannot directly access to ports inside docker.  
- To Interact with docker container `docker exec -it node-app bash`
- Create a new `.dockerignore` to list all the files/folders which to be ignored while copying.
- [**METHOD 1**] To reflect changes in source code in docker container
  - FIrst delete the container `docker rm node-app -f`
  - Build the container`docker build -t node-app-image .`
  - Run the container using `docker run -p 8080:3000 -d --name node-app node-app-image`
  - This method slows development speed and is tedious, so follow Method 2
- **[METHOD 2]** Using bind volume
  - In docker to persist data and share it between multiple containers, we use something called a Volume
  - There are different types of volumes based and In this case we make use of bind volume. In simple terms it syncs a selected folder/data in your local machine to a selected folder in your container. using `-v` flag
  - `docker run -v pathtofolderinlocalmachine:pathincontainer -p 8080:3000 -d --name node-app node-app-image`
  - `docker run -v ~/path/to/project:/app -p 8080:3000 -d --name node-app node-app-image` Here `.` relative path doesn't work.  Instead you can use 
    - For windows command shell `-v %cd%:/app` . Grabs current working directory
    - For windows powershell `-v ${pwd}:app`
    - 

### useful links

- https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

- [docker-compose nodejs and mongodb - bezkoder](https://www.bezkoder.com/docker-compose-nodejs-mongodb/)
- https://www.youtube.com/watch?v=hP77Rua1E0c

- Example docker-compose.mongo.yml https://gist.github.com/gterdem/ac5b0f135fba034333dd4597edd2e278
- [react-express-mongodb-docker](https://www.freecodecamp.org/news/create-a-fullstack-react-express-mongodb-app-using-docker-c3e3e21c4074/)
- https://linuxhandbook.com/remove-docker-images/\
- https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
- https://auth0.com/blog/use-docker-to-create-a-node-development-environment/

