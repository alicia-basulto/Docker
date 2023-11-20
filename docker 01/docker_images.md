# DOCKER Cheat Sheet
## Setup
https://docs.docker.com/engine/install/ubuntu/
## Commands
### Images

list images
```
docker images   
```
inspect images
```
docker inspect [idImage/nameImage]
```
remove image forcing it

```
docker image rm [idImage/nameImage] -f
```

rename tag image 
```
docker image tag [idImage/nameImage] [newName]
```

name tag image from build
```
docker build -t [newName:1.0]
```
build image from Dockerfile in current directory
```
docker build  .  
```
build image from Dockerfile in current directory
```
docker build  .  
```

### Containers
#### Characteristics
* ephemeral content, we lost info inside when container is stopped
* 
list active containers
```
docker ps   
```

list containers in all states
```
docker ps -a
```

* Up (started)
* Exited (stopped)
* Created
list active containers


run container  
```
docker start [idContainer/name]
```

stop container  
```
docker stop [idContainer/name]
```
create container with a coustomized name and not a random one  
```
docker create [idImage/nameImage] --name [nameContainer]
```
remove container  forcing it
```
docker rm [idContainer/nameContainer] -f
```
### Ports
It isn't practical to expose the port of the container because every time we restart, the IP will change. Because of that, we map the ports from the container to the host machine.

Mapping/Publishing port 80 of container to 8080 od host machine. The port configuration will mantain despite the restart phases
```
docker create -p 8080:80 --name webserver helloworld
```


This keep in metadata that the principal port of the image is the 80
```
EXPOSE 80 in Dockerfile
```
Where the port map is: Finds all running processes and filters the list to only show processes that contain "proxy" in their process information. DOCKER-PROXY
```
ps aux | grep proxy
```

### Inside Containers
Start an interactive Bash shell inside a running Docker container.
```
docker exec --it [idContainer/nameContainer] /bin/bash
```

- `docker exec `runs a command inside a running container
- `-it `starts an interactive terminal session


```
docker exec [idContainer/nameContainer] bash -c "sleep 10"
```
### Volumes
#### Method Bind
* deprecated
* only in DEV environments

Create a new container with some bind mounts configured.
```
docker create --name dev01 --mount type=bind, source="$(pwd)/app", target=/app nginx:latest
```
* `docker create` will create a new container but not start it
* `--name dev01` names the container dev01
* `--mount` configures a bind mount from the host into the container
* `type=bind` specifies this is a bind mount
* `source="$(pwd)/app"` binds the host's current directory ./app into the container
* `target=/app` mounts the host path into /app in the container
* `nginx:latest` uses the latest Nginx image