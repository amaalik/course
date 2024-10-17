**Installing docker on Ubuntu**
((this can not work on a container, only VMs))

1 sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

2 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 

3 sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"

4 sudo apt-get update

5 sudo apt-get install docker.ce

6. sudo docker run hello-world (this is to test docker)


**pulling a container image**

1. docker image pull nginx:latest

**running an image as a container**

1. docker container run -itd --name web-server-nginx -p 8080:80 nginx:latest
		or
docker run -itd --name web-server-nginx -p 8080:80 nginx:latest
		or
docker container run -itd --name web-server-nginx -P nginx:latest (this will aloow docker to automatically map the ports for us)

docker container port web-werver-nginx (this will show you the port that is running)

## docker container run: this is to run an image as conatainer
## -it: to make in interactive, so that you can interact with it
## -d: detach mode
## --name: to name the container
## -p: to map ports ie, 8080 is the outside port, while the 80 in the port of the app in the container. so what is running with port 80 in the container, will be access as port 8080 using the IP of the host.
## nginx:latest:  the images to use to run the container and the version

**Build a docker file** to build an image
1 docker build -t img_from .
## docker build: this is use to build docker image from a docker file
## -t img_from: -t is ude to tag the container, and in this case the tag is img_from
## .: this is the location of the dockerfile.



**Getting access to a container**

1. docker exec -it [container name or ID] bash
   docker container attach my-busybox (but if you exit from here, the conataine will be stopped) 


**To Search on docker**

1 docker search python:3.6

2 docker search --filter "is-official=true" registry (this is to search for official images)

3 docker image pull nginx:alpine  (this is to pull images from docker hub to your local machine)

4 docker login (this is used to login into your docker account from the host machines, which can enable you to push images).

5 docker tag nginx:latest malikdevop/repo-nginx:cc-nginx 
(this is image tagging, before you push an image you need to tag it with the way you named it on your docker repo, docker tag is the command to tag, nginx:latest the image to be tagged, malikdevop/repo-nginx:cc-nginx is the new tag.

6  docker push malikdevop/repo-nginx:cc-nginx (this will push it to your docker hub repo)

7. docker image rm nginx:latest or docker rmi nginx:latest (this is used to remove images)


**CONATIER**
1 docker container create -it --name cc-busybox-A busybox:latest (this is will only create a container but not run it)
	to run/start it, you then say: docker container start cc-busybox-A

	--rm (to remove an image after the container has been deleted)
	docker container rename cc-busybox-A my-busybox (to rename a container)
	to stop a container use: docker container stop cc-busybox-A
2 docker container run -itd --name cc-busybox-A busybox:latest (this is will create and run it)

3 docker exec -it my-busybox bash

4 docker container rm cc-busybox-A (or you can us ethe container ID)

docker container stop cc-busybox-A --force
docker container prune


**CREATING NETWORKS IN DOCKER**
docker network create --driver bridge my-bridge
docker network create --driver bridge --subnet=192.168.0.0/16 --ip-range=192.168.5.0/24 my-bridge-1
docker network ls (this is use to list your networks)
docker network ls --filter driver=bridge
docker network connect my-bridge-1(network name) main-busyox(container name)
docker container inspect main-busybox (this is to check your networking settings)

docker network inspect my-bridge-1
docker network disconnect my-bridge-1 nginx


**DOCKER VOLUME**

docker volume create vol-busybox (creating a volume)
docker run -d --volume vol-ubuntu:/tmp ubuntu (to create and mount volume)
docker volume ls (to view all volumes)
docker volume rm vol-ubuntu (can only remove a volume that is not in use, 


docker run -v /opt/datadir:/var/lib/mysql MySQL (external volume is /opt/datadir)


docker run -itd --name cont-ubuntu --volume vol-ubuntu:/var/log ubuntu:latest

sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose (installing docker compose) then, sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version (to check your compose version)








		BASIC DOCKER COMMAND
##docker run nginx (used to run a docker container, it will run and exit, since it is not running a servie or apilcaition)
#docker run -it centos bash (to login direclt into the container)
##docker ps (this is will all running containers only)
##docker run -d centos sleep 20 (sleep the centos for 20 secs before going off, and the -d flag is to run it in background, ie detached mode)
##docker rm nervouse_tesla, or docker rm 345 or docker rm 345 e0a 773 - this will remove multiple containers, with those that begins with those IDs                                                                           (removing container )
##docker images (this will list imsges that are present)
##docker rmi ubuntu (this is to remove an images)
you need to delete imaged before removing the container
##docker run -d --name webapp nginx:1.14-alpine  (to run webapp with a name)

##docker run redis:4.0 (this will run redis with version of 4.0, if not specified, it will run the latest)

##docker inspect blissful_hopper (where blissful_hopper is the name of the container )
