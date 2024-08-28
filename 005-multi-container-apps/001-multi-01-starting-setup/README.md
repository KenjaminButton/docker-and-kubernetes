# Dockerizing a MERN App

## Dockerizing MongoDB Service

1. Google search for Docker Mongo Container [Docker Hub MongoDB Container](https://hub.docker.com/_/mongo)
2. Run the following terminal command:

```shell
$ docker run --name mongodb --rm -d -p 27017:27017 mongo
$ docker ps 
$ docker logs mongodb
```

## Dockerizing Node App (Backend folder)

1. Create a Dockerfile
2. Dockerfile code is as follows:

```dockerfile
FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 80

CMD ["node", "app.js"]
```

3. Run the following shell commands:

```shell
$ docker image prune -a
$ docker build -t goals-node .
$ docker run --name goals-backend --rm goals-node
```

3. Connecting to localhost:27017 throws an error. 

4. In app.js

```js
'mongodb://localhost:27017/course-goals',

// Change to the following: 
'mongodb://host.docker.internal:27017/course-goals',
```
5. Rebuild the image

```shell
# Change source code first from step 4
$ docker build -t goals-node .
# Run container again
$ docker run --name goals-backend --rm goals-node
```

6. New Problem:
- Front end app (React) cannot communicate with backend container
```shell
# Stop backend container
$ docker stop goals-backend
# Restart backend container with correct ports published:
$ docker run --name goals-backend --rm -d -p 80:80 goals-node

```

## Dockerizing React SPA into a container

1. cd into frotnend folder
2. Create Dockerfile with the following:

```dockerfile
FROM node

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

3. Build 

```shell
$ docker build -t goals-react .
```

4. Run a Container

```shell
$ docker run --name goals-frontend --rm -d -p 3000:3000 -it goals-react 
```

- Stop all containers now as we need to polish the docker containers
```shell
# $ docker stop NAMES
$ docker stop goals-react
$ docker stop goals-node
$ docker stop mongodb
```

## Adding Docker Networks for Efficient Cross-Container Communication