# Docker



## Installation

- Easy way to get started with docker is to install Docker Destop app. Need to install docker-compose separately if you are using linux, latest version of desktop app have an option to do just that in settings. 

  

## commands

- `docker run nginx` If the image already exists then runs the image/container. if there is no image it downloads from hub
- `docker ps` list all running containers
- `docker ps -a`   - List out all containers
- `docker stop dockername`
- `docker rm dockername` to remove a container
  - `docker rm containerName -f`  Used to forcefully remove (stop a running container and then remove). 
  - `docker rm containerName -fv`     To remove volumes associated with the container

- `docker images`  or `docker image ls` list out downloaded images
- `docker rmi nginx` to remove an image. make sure there are no running containers off that image.
- `docker pull nginx` to only pull the image from hub and not run.

- We can run docker from terminal in either attached or detached mode
  - Detached mode  `docker run -d nginx`  so that your terminal is free and open to input/run other commands.
  - start in attach mode with `-d` flag or attach to an already running container using its hash `docker attach hash`
- View logs in a container even if was stopped running `docker logs node-app`
- `docker volume ls`  - List of all volumes
- `docker prune` Removes all local volumes not used by at least one container
- `docker command --help`  - For cli docs or  **Help**



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

```dockerfile
FROM node:16 

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . ./

## EXPOSE command is just for documentation, it actually does nothing. 
## Its just to explicitly show that we like to port forwarding to this port.
## EXPOSE 3000 

 
## create a env variable to be used inside the container
## ENV PORT 3000   ## old way to define evn in dockerfile

EXPOSE $PORT

## CMD ["npm", "start"] to run on production

## After using bind volumes to restart the server using npm script which runs nodemon
CMD ["npm", "run", "dev"]
```

- **NOTE:** In Dockerfile each statement is a layer executed line by line from top to bottom. Each layer is cached ie, upon building the image, if the nothing is changed in a layer compared with the previous image then it uses the cached data/layer. If a layer is changed it does it anew and caches it. This the reason why `COPY package*.json` is place above `COPY . ./`
- cd into the root folder where Dockerfile resides and to build the docker image run `docker build .`   View the image using `docker image ls`
- To build an image with a name, run `docker build -t node-app-image .`
- Create a container using a given image by 
  - `docker run node-app-image` . Here node-app-image is the name of image we created earlier.
  - `docker run -d --name node-app node-app-image` Here using --name flg to name this container. `-d` flag to run in detached mode
  - `docker run -p 8080:3000 -d --name node-app node-app-image` Here -p flag for forwarding 3000 which is docker container's port to 8080 which is localhost machines port or outside port.
- **Note**: Your docker container can have access to outside ports ( meaning not just internet but also local host machine) but outside ports cannot directly access to ports inside docker.  
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
  - Cause we are syncing  and running from containe, we dont need node_modules folder but deleting it in local, deletes it in container. So prevent this we run add another volume to preserve nod_modules using anothe -v flag. `docker run -v ~/path/to/project:/app -v /app/node_modules -p 8080:3000 -d --name node-app node-app-image`
  - **NOTE**: docker volumes takes specifity as precedence. meaning if the path is more specific then it overrides other -v flag in our case bind mount. 
  - **NOTE:** Bind volume is a two way sync. meaning any new file added in container reflects your local machine folder. Address this by adding read only sync. 
  - Make read only by adding `:ro` container path. ` docker run -v ~/path/to/project:/app:ro -v /app/node_modules -p 8080:3000 -d --name node-app node-app-image`
- Pass environment variable using `-e` or `--env`  flag. Usage `--env PORT=4000`
  - Standard convention to store  many env variable is by using `.env` file
- At this point the command to run is long with  many flags and all. To fix this and also manage multiple docker images we use **docker-compose**



### docker-compose.yml

```yaml
verison: "3"
services:				# Each container is referred to as a service
	node-app:			# user defined name for a container
		build: .		# specify what image to build ie. get dockerfile
        ports:			# provide list of ports to open
        	- "3000:3000"
        volumes:
        	- ./:/app	# we can pass ro flag and use relative paths
        	- /app/node_modules
        # environment:
        #	- PORT=300
        env_file:
        	- ./.env
        	
```

- `docker-compose -d up` Build an image if doesn't exist and run containers based on yaml file.
- Naming convention: `<projeject-root-dirname>_<container/service-name>`
- `docker-compose down -v` removes all the containers and also removes volumes associated with the containers cause of  `-v` flag
- On the second  run of `docker-compose  up`  It looks for an image and starts running containers. It don't look for changes and doesn't build an image before running. So we need to explicity build if any change was made to images. 
- `docker-compose up -d --build` forces to build an new image.



#### Development vs Production configs

This can be done either by using mulitple docker-compose yaml files or by using a single yaml file. 

- Using Mulitple yaml files
  - Create docker-compose.yml to store common config
  - create `docker-compose.dev.yml` , `docker-compose.prod.yml` , `docker-compose.staging.yml` etc for each environment
  - Now up the docker using `docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d` . Note: order of files in important.
  - To not install dev dependencies in the prod build follow this [workaround](https://youtu.be/9zUHg7xjIqQ?t=6062)





----



### useful links

- https://nodejs.org/en/docs/guides/nodejs-docker-webapp/
- [docker-compose nodejs and mongodb - bezkoder](https://www.bezkoder.com/docker-compose-nodejs-mongodb/)
- [Freecodecamp: Learn Docker - DevOps with Nodejs & Express](https://www.youtube.com/watch?v=9zUHg7xjIqQ)
- https://www.youtube.com/watch?v=hP77Rua1E0c
- Example docker-compose.mongo.yml https://gist.github.com/gterdem/ac5b0f135fba034333dd4597edd2e278
- [react-express-mongodb-docker](https://www.freecodecamp.org/news/create-a-fullstack-react-express-mongodb-app-using-docker-c3e3e21c4074/)
- https://linuxhandbook.com/remove-docker-images/\
- https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
- https://auth0.com/blog/use-docker-to-create-a-node-development-environment/
