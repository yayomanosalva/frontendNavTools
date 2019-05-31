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
| ver ip docker                           | $ sudo docker inspect id_container                                        |                                                         |
