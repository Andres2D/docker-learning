## Docker course 🚚📦️
This is a repo to follow [this](https://www.udemy.com/course/docker-kubernetes-the-practical-guide/learn/lecture/22625176#overview) this docker course.

### Installation ⬇️
* [Docker desktop](https://docs.docker.com/desktop/install/mac-install/).

### The Dockerfile 🦺
Base structure:
```
FROM baseImage // ex: node || node:version


WORKDIR /app //Path from all the commands will be executed

COPY package.json /app // Copy only the package.json to enable cache on dependencies

RUN npm install // run a command inside the image

COPY . /app // First path(.): all the files in the current path
         // Second path(/app): Where is going to be copy in the image, in the workdir path 

ARG ARGUMENT_NAME=ARGUMENT_VALUE // Set argument values

ENV PORT 80 // Add env variables (ENV Variable_name default value)

EXPOSE 80 // Expose from the container the port 80 to our local environment

VOLUME [ "/path_file_to_persist/" ] //persist data from container path

CMD ["node", "server.js"] // starts the container or project. Different from RUN command. RUN for image and CMD to container.
```

### .dockerignore
To specify which folders and files we don't want to copy with the COPY instruction in the Dockerfile
```
node_modules
Dockerfile
.git
```

### DockerHub
Share an image
```
docker push image_name
```
Pull an image
```
docker pull image_name
```

### Docker network
Special host to connect docker container with the local machine
```
host.docker.internal
```
Example with mongo DB:
```
'mongodb://host.docker.internal:27017/swfavorites'
```

Communication between containers:
1. Run the mongo image
```
docker run -d --name mongodb mongo
```
2. Inspect the mongodb container
```
docker container inspect mongodb
```
3. Get the IPAddress from the inspect data and change it in the app connection
```
ex: 'mongodb://172.17.0.2/swfavorites',
```

Other option os to create container networks

1. Create a network
```
docker network create network_name
``` 
2. Start a container with the network specification
```
docker run -d --name mongodb --network favorites-net mongo
```
3. Specify the container network in the code
Connect with a container network 'mongodb://docker_container_name:27017/swfavorites',

4. Start the other container in the same network
```
docker run --name favorites -d --network favorites-net --rm -p 3000:3000 favorites-node
```

### Commands 🧑‍💻
Builds an image with the Dockerfile configuration
```
docker build .
```
To create and run a new container base on an image in attached way
```
docker run -p local-port:image-port (-d to start it in detached way) (-rm to remove when stopped) sha256_id
```
List of images running (-a to see all images)
```
docker ps
```
Stops the image by name
```
docker stop image_name
```
Run a specific software with interactive shell
```
docker run -it image_name
```
Start a previous created container in detached way
```
docker start (-a to start in attached mode) (-i to interactive shell) container_name
```
Attach terminal to a running container
```
docker attach container_name
```
Get the history logs of a detached container
```
docker logs container_name (-f to attach terminal for future logs)
```
Remove containers
```
docker rm container_name container_name container_name ... 
```
List images
```
docker images
```
Remove images
```
docker rmi image_id image_id image_id
```
Remove all stopped containers
```
docker container prune
```
Inspect an image
```
docker image inspect image_id
```
Copy assets into a container
```
docker cp path_from(outside of the container) container_name:/path_to(inside the container)
```
Get assets from container
```
docker cp container_name:/path_from(inside the container) path_to(outside of the container)
```
Name a container
```
docker run --name containerName
```
Name an image
```
docker build -t tagName:tagVersion .
```
Rename a docker image
```
docker tag old_name:old_tag new_name:new_tag
```
List all volumes
```
docker volume ls 
```
Create volume with name
```
docker run -v volume_name:/volume/path (inside of container) image_name
```
Remove anonymous volumes
```
docker volume prune
```
Create bind volume to listen changes
```
docker run -v "full_path/":/app image_name
```
Work with node modules and bind volumes
```
docker run -v "full_path/:/app:ro(if is read only)" image_name -v /app/node_modules
```
Docker binds full command example
```
docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "/Users/andresalcaraz/Development/docker/data-volumes-01-starting-setup":/app -v /app/temp -v /app/node_modules feedback-node:volumes
```
Create a new volume
```
docker volume create volume_name
```
Remove a volume
```
docker volume rm volume_name
```
Setting ENV values in docker run
```
docker run (...) --env PORT=8000 (...)
```
Setting ENV from file
```
docker run (...) --env-file ./.env (...)
``` 
Build an image with a specified argument
```
docker build (...) --build-arg ARGUMENT_NAME=ARGUMENT_VALUE .
```
List networks 
```
docker network ls
```