# frontendNavTools

#### Link list Docker Command line
https://docs.docker.com/engine/reference/commandline/docker/

| Plugin                                  | README                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------- |
| installDocker                           | http://docs.dopcker.com                                                   |
| Download Images                         | http://hub.docker.com                                                     |
| images have tag or branch               | $ docker pull ubuntu:16.04                                                |
| list images                             | $ docker images                                                           |
| Genrar Containers                       | $ docker run -i -t ubuntu:16.04                                           |
| -i                                      | interaccion con el contenedor                                             |
| -t                                      | utiliza una seudo terminal                                                |
| exit                                    | salir del contenedor                                                      |
| list containers                         | $ docker ps -a                                                            |
| utilizar contenedor                     | $ docker start id_contenedor                                              |
| utilizar contenedor                     | $ docker attach id_contenedor                                             |
| install python in container             | $ apt-get update                                                          |
| install python in container             | $ apt-get install python                                                  |
| Eliminar contenedor                     | $ docker rm id_contenedor                                                 |
| Descargar imagen que está en dockerfile | $ docker-compose up -d                                                    |
| ingresar a terminal de  contenedor      | $ docker-compose exec ubuntu /bin/bash                                    |
| ver ip docker                           | $ sudo docker inspect id_container                                        |
|Compartir container en dockerhub         | $ sudo docker tag nameContainerLocal usernamedockerhub/namecontainer
|push para compartir                      | $ sudo docker push usernamedockerhub/namecontainer
                                          | 

#step by step build docker cointainer and images

#Step 1: Building an image
#Syntax: docker build -t <image-name> <location of dockerfile>
-------------------------------------------------------------------
docker build -t my-nginx .

#Step 2: List all the images
#Syntax: docker images
-------------------------------------------------------------------
docker images

#Step 3: Running a container from the image
#Syntax: docker run -itd --name <container-name> -p <host-port>:<port in container> image-name:tag
# note in the above syntax:
# -d : represents (detached mode), note that if you dont run this in detached mode, the life of the container will be the life of the terminal in which you are executing it.
# -p : represents the host-port to container-port mapping, if you substitute it with -P you will get a random port allocated by docker
# --name : represents the name of the container 
-------------------------------------------------------------------
docker run -itd --name my-nginx-container-1 -p 7777:80 my-nginx:latest
docker run -itd --name my-nginx-container-2 -p 7778:80 my-nginx:latest

Step 4: View all the containers
-------------------------------------------------------------------
# Shows all the containers which are running
docker ps 

#Shows all the containers stopped and running
docker ps -a

Step 5: Logging into the container
-------------------------------------------------------------------
#Note: The container must be started before we can do this.
docker exec -it <container-id> /bin/bash

Step 6: Logging into Dockerhub account on the terminal
-------------------------------------------------------------------
docker login 
docker tag <currentimage>:<tag> <repository-name>/<image-name>:<tag>
docker push <repository-name>/<image-name>:<tag>
docker commit <container-id> <repository-name>/<image-name>:<tag>

docker pull <repository-name>/<image-name>:<tag>




Step 11: Remove all the containers and images
-------------------------------------------------------------------
#Note: To remove an image the corresponding container built from that image will need to be removed.

#Remove a specific container
docker rm <container-id>

#Remove all containers
docker rm $(docker ps -a -q)

# remove image (note: no containers for this image should be running)
docker rmi <image-id>

# remove all images
docker rmi $(docker images -q)
