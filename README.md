## Docker course 🚚📦️
This is a repo to follow [this](https://www.udemy.com/course/docker-kubernetes-the-practical-guide/learn/lecture/22625176#overview) this docker course.

### Installation ⬇️
* [Docker desktop](https://docs.docker.com/desktop/install/mac-install/).

### The Dockerfile 🦺
Base structure:
```
FROM baseImage // ex: node

WORKDIR /app //Path from all the commands will be executed

COPY package.json /app // Copy only the package.json to enable cache on dependencies

RUN npm install // run a command inside the image

COPY . /app // First path(.): all the files in the current path
         // Second path(/app): Where is going to be copy in the image, in the workdir path 


EXPOSE 80 // Expose from the container the port 80 to our local environment

CMD ["node", "server.js"] // starts the container or project. Different from RUN command. RUN for image and CMD to container.
```

### Commands 🧑‍💻
Builds an image with the Dockerfile configuration
```
docker build .
```
To create and run a new container base on an image in attached way
```
docker run -p local-port:image-port (-d to start it in detached way) sha256_id
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
