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

WORKDIR /app

COPY . ./app

RUN npm install

EXPOSE 80

CMD ["node", "server.js"]
```







 ```shell

 ```