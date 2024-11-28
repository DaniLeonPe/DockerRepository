# Tarea 4


## Descargar e iniciar un contenedor MariaDB


Se ejecuta el siguiente comando para descargar la imagen de MariaDB:
```code/bash/textplan/console  
docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=exampledb -p 3306:3306 -d mariadb:latest
````

se utiliza el comando
```code/bash/textplan/console  
sudo docker ps -a
sudo docker ps -a
CONTAINER ID   IMAGE            COMMAND                  CREATED          STATUS                      PORTS     NAMES
76d3784a5e76   mariadb:latest   "docker-entrypoint.s…"   15 seconds ago   Created                               mariadb-container
```

## Descargar un cliente de base de datos para MariaDB (Adminer)

### Descargar y ejecutar CloudBeaver en Docker

```code/bash/textplan/console      
docker run -d --name cloudbeaver -p 8978:8978 dbeaver/cloudbeaver:latest

Unable to find image 'dbeaver/cloudbeaver:latest' locally
latest: Pulling from dbeaver/cloudbeaver
9c704ecd0c69: Pull complete
1ecaf9f47d12: Pull complete
f771417f3e38: Pull complete
e74eee18d850: Pull complete
4f4fb700ef54: Pull complete
364eab3afb5a: Pull complete
e724359f8e7e: Pull complete
28cbd2fcb78e: Pull complete
Digest: sha256:be0b0b8e16a5ba5abbeec3dc18e2bb18e1d2f6bb04135e32faace799a78b17c4
Status: Downloaded newer image for dbeaver/cloudbeaver:latest
59a93bb48126d171eedcf1c5b7f53a4d6755a9d8a9404ea8b9b3f86b598783f8

```

se verifica que el contenedor este corriendo

```code/bash/textplan/console
docker ps -a
CONTAINER ID   IMAGE                        COMMAND                  CREATED              STATUS                   PORTS                                       NAMES
09018787f1a9   dbeaver/cloudbeaver:latest   "./run-server.sh"        6 seconds ago        Up 3 seconds             0.0.0.0:8978->8978/tcp, :::8978->8978/tcp   cloudbeaver
```

Accedemos a la direccion http://localhost:8978 
<img src=../img/CLOUDBEAVER1.png>


Realizamos la configuracion del cliente

<img src=../img/cloudBeaver2.png>


Hacemos una conexion con mariadb

<img src=../img/3.png>

Y verificamos que estamos conectados

<img src=../img/4.png>


### Detener y eliminar contenedores

Detenemos y eliminamos los contenedores


```code/bash/textplan/console

 docker stop mariadb-container
    mariadb-container
 docker stop cloudbeaver
    cloudbeaver
 
 docker rm mariadb-container
    mariadb-container
 docker rm cloudbeaver
    cloudbeaver
 docker ps
    CONTAINER ID   IMAGE                   COMMAND                  CREATED      STATUS             PORTS                                   NAMES
    fb0a99114c60   phpmyadmin/phpmyadmin   "/docker-entrypoint.…"   6 days ago   Up About an hour   0.0.0.0:8000->80/tcp, :::8000->80/tcp   pma

```
