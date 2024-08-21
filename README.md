# Docker & Kubernetes: The Practical Guide [2024 Edition]

## 2 - Images and Containers

- Images are the blueprint/templates for the container.

- Pre-Built vs Custom Images

- Creating & Managing Containers

<!-- Pull node from docker hub -->
```shell
docker run node 
```

<!-- Show container has been created -->
```shell
docker ps -a
```

<!-- Creates an interactive shell for the container -->
<!-- Runs node environment -->
 ```shell
docker run -it node
 ```

#### Build our own Image with a Dockerfile

```dockerfile
FROM node

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application files
COPY . /app

# Expose the port on which the app will run
EXPOSE 80

# Run the application
CMD ["node", "server.js"]
```

- Build docker
 ```shell
docker build .
 ```

- Testing docker, but will not run on port 80 for now
```shell
docker run sha256:####
```


- See docker processes
 ```shell
docker ps
 ```

 - Stop docker containers by name (it will take a while, be patient)
 ```shell
docker stop NAMES
 ```

- If docker container is stopped, you can check containers with the following command: NOTE: ps => process status and -a => all

```shell
docker ps -a
```

- TO run port, you have to PUBLISH with the -p flag (80 is the chosen Dockerfile EXPOSE value)
```shell
docker run -p 3000:80 sha256:####
```

- If changes are made in the code, we will need to rebuild the image to pick up external changes. Basically, an image is a closed template (READ ONLY). 

```shell
docker build .
```

- [x] Conceptualize and understand what attached vs detached containers are.

- Run a check on docker hub to see if an image of python etc. is available.

##### Python Docker File
```dockerfile
FROM python

WORKDIR /app

COPY . /app/

CMD ["python", "rng.py"]
```

- docker run sha256:#### will give an EOFError because user cannot make inputs.

- -i => interactive 
- -t => teletype tty

```shell
docker run -it sha256:####

docker start -a -i NAMEOFCONTAINER
```

Docker remove images simultaneously after container is stopped

```shell
docker run -p 3000:80 -d --rm IMAGEID
```

```shell
dockerk image inspect IMAGEID
```

How to specify a tag. -t option

```shell
docker build -t goals:latest .
docker build -t goals:1 .
docker build -t goals:2 .

docker run -p 3000:80  -d --rm --name goalsapp goals:latest
docker stop goalsapp
```

