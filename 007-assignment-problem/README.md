## 1) Create appropriate images for both apps (two separate images!).

HINT: Have a brief look at the app code to configure your images correctly!

#### a) Node-app

```dockerfile
-> Docker File

1.	FROM node 
2.	
3.	WORKDIR /app
4.	
5.	COPY package.json .
6.	
7.	RUN npm install
8.	
9.	COPY . .
10.	
11.	EXPOSE 3000
12.	
13.	CMD ["node", "server.js"]
```

-> Build image cmd:
```shell
$ docker build .
```


#### b) Python-app

-> Docker file
```dockerfile
FROM python
 
WORKDIR /app
 
COPY . /app
 
CMD [ "python", "bmi.py" ]
```
-> Build image cmd:
```shell
$ docker build .
```


## 2) Launch a container for each created image, making sure,

that the app inside the container works correctly and is usable.

#### a) Node-app

-> Run cmd:

```shell
$ docker run -p 3000:3000 <imageId>
```
#### b) Python-app

```shell
$ docker run -i -t <imageId>
```

## 3) Re-create both containers and assign names to both containers.

Use these names to stop and restart both containers.

#### a) Node-app
```shell
$ docker run -p 3000:3000 -d --name node_assignment <imageId>

$ docker stop node_assignment

$ docker start node_assignment
```

#### b) Python-app

```shell
$ docker run -it --name python_assignment <imageId>

$ docker stop python_assignment

$ docker start -a -i python_assignment
```


## 4) Clean up (remove) all stopped (and running) containers, clean up all created images.

```shell
$ docker rm <container_name> <container_name> <container_name>
# Also works to delete all containers
$ docker container rm $(docker ps -a -q)

# removes all unused Docker images from your system.
$ docker image prune -a
```

## 5) Re-build the images - this time with names and tags assigned to them.

#### a) Node-app

```shell
$ docker build -t node_image:latest .
```

#### b) Python-app

```shell
$ docker build -t python_image:latest .
```

```shell
# Check status
$ docker images
```

## 6) Run new containers based on the re-built images, ensuring that the containers are removed automatically when stopped.

#### a) Node-app

```shell
$ docker run -p 3000:3000 --rm --name node_assignment node_image:latest
```

#### b) Python-app
```shell
$ docker run -it --rm --name python_assignment python_image:latest
```

