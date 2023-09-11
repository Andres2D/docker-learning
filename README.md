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
To run the container
```
docker run -p local-port:image-port sha256_id
```
List of images running
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
