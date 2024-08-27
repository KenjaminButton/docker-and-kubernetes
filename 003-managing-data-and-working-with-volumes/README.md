# Writing, Reading, and Persisting Data

```dockerfile
# Dockerfile
FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

CMD ["node", "server.js"]
```

```shell
$ docker build -t feedback-node:latest .

$ docker run -p 3000:80 -d --name feedback-app --rm feedback-node:volumes
```

### Creating a named volume when running a container

```shell
$ docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback  --rm feedback-node:volumes

$ docker stop feedback-app

$ docker volume ls

$ docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback  --rm feedback-node:volumes
```

#### Removing Anonymous Volumes
```shell
docker volume rm VOL_NAME

docker volume prune
```

#### Bind Mounts

[Mounting Docker volumes with Docker Toolbox for Windows](https://headsigned.com/posts/mounting-docker-volumes-with-docker-toolbox-for-windows/)

```shell
$ docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback  -v "DockerFileCopyPath:/app" feedback-node:volumes
```

docker run -p 3000:80 -d --name feedback-app -v feedback:/app/feedback  -v "/Users/kenjaminbutton/Desktop/2024_Software_Engineer/008-docker-and-kubernetes-2024/003-managing-data-and-working-with-volumes/002-data-volumes-03-adj-node-code:/app" feedback-node:volumes

#### Bind Mounts - Shortcuts

#### macOS / Linux
```shell
-v $(pwd):/app
```

