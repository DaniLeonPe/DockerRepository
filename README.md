# DockerRepository

# Tarea 1 Docker

### Paso1: Trabajar con imágenes de Docker

Para verificar si puede acceder a imágenes y descargarlas de Docker Hub, escriba lo siguiente:
```code/bash/textplan/console
docker run hello-world

```

Resultado:
```code/bash/textplan/console

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

### Paso2: Administrar contenedores de Docker

Para ver los activos, utilice lo siguiente:
```code/bash/textplan/console
docker ps

CONTAINER ID   IMAGE                   COMMAND                  CREATED      STATUS             PORTS                                   NAMES
fb0a99114c60   phpmyadmin/phpmyadmin   "/docker-entrypoint.…"   4 days ago   Up About an hour   0.0.0.0:8000->80/tcp, :::8000->80/tcp   pma
```
Para ver todos los contenedores, activos e inactivos, ejecute docker ps con el conmutador -a:
```code/bash/textplan/console
docker ps -a

CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS                      PORTS                                   NAMES
0b2f95d907c4   hello-world             "/hello"                 31 minutes ago   Exited (0) 31 minutes ago                                           sweet_hoover
fb0a99114c60   phpmyadmin/phpmyadmin   "/docker-entrypoint.…"   4 days ago       Up About an hour            0.0.0.0:8000->80/tcp, :::8000->80/tcp   pma
8dff75ac4ab6   mysql                   "docker-entrypoint.s…"   4 days ago       Exited (0) 4 days ago                                               dbmysql
41a9143b4ca8   hello-world             "/hello"                 7 days ago       Exited (0) 7 days ago                                               kind_black
2615b0eef522   imagenphpcli            "docker-php-entrypoi…"   7 days ago       Exited (0) 7 days ago                                               charming_williams
```
Para ver el último contenedor que creó, páselo al conmutador -l:
```code/bash/textplan/console
docker ps -l

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
0b2f95d907c4   hello-world   "/hello"   32 minutes ago   Exited (0) 32 minutes ago             sweet_hoover

```

Listar las imagenes de Docker

```code/bash/textplan/console
docker images

REPOSITORY                    TAG                 IMAGE ID       CREATED         SIZE
app-editor-texto-image        latest              ea8337537317   6 days ago      641MB
atprodriguez/hexcodle-react   1                   1bde24db0e10   7 days ago      49.3MB
danileonpe/pokemon            1.0                 f48a33765cb6   7 days ago      52.9MB
pokemon                       latest              f48a33765cb6   7 days ago      52.9MB
imagenphpweb                  latest              c94c0c519a2b   7 days ago      502MB
imagenphpcli                  latest              9e0a5ab34cef   7 days ago      527MB
composer                      latest              64067ce2baf5   7 days ago      195MB
tomcat                        9.0                 6dbc2b16532f   2 weeks ago     469MB
ubuntu                        latest              fec8bfd95b54   5 weeks ago     78.1MB
php                           8.1-fpm             766a4ae6785e   8 weeks ago     492MB
nginx                         stable-alpine3.20   60847f99ea69   3 months ago    48.8MB
phpmyadmin                    5.2.1               8a4be2b65a71   7 months ago    568MB
mysql                         8.3.0               65f3f983cb08   8 months ago    632MB
mysql                         latest              82563e0cbf18   8 months ago    632MB
gvenzl/oracle-xe              18                  32036241439d   12 months ago   2.58GB
phpmyadmin/phpmyadmin         latest              933569f3a9f6   16 months ago   562MB
hello-world                   latest              d2c94e258dcb   19 months ago   13.3kB


```




