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