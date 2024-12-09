
# Practica 7

##  Code, Learn & Practice(Docker: Construcción de un Dockerfile con Tomcat, MariaDB y Cliente de Base de Datos)


### Objetivo

El objetivo de este ejercicio es crear un entorno con Docker que incluya un servidor Tomcat, una base de datos MariaDB y un cliente para acceder a la base de datos. Para esto, configuraremos los contenedores con redes personalizadas y un volumen común para persistir datos.

### Requisitos

Crear una red Docker personalizada para los contenedores.
Crear un contenedor Tomcat para desplegar una aplicación web.
Crear un contenedor MariaDB para gestionar la base de datos.
Utilizar un volumen común para persistir los datos de la base de datos.


### Pasos a Seguir

#### Paso 1: Crear la red personalizada

Creamos una red personalizada para que los contenedores puedan comunicarse entre sí

```code/bash/textplan/console
 docker network create my_network
d7c17ec33df392709953f0200b71032884a83ae0f940b20b5a22a17234fcbbd0
 docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
4f9160b72fd6   bridge            bridge    local
c8ff60fe92b3   host              host      local
0cd64b1553f6   mongodb-network   bridge    local
d7c17ec33df3   my_network        bridge    local
0e3d991c8d01   none              null      local
15c8856d6552   tomcat-network    bridge    local



```

#### Paso 2: Crear un volumen común
docker 

Creamos un volumen para en comun
```code/bash/textplan/console
docker volume create mdb
mdb
alumno@alumno-aed:~$ docker volume ls
DRIVER    VOLUME NAME
local     8194a374d46cea3852e7295209160dfb49bbd03ef81bcf705b5a8075cf841f86
local     33352a59b2f87aad29d07d823de9e6bfcf93d2b58054ae914e75d376a08711ea
local     b04f97b8d432fd616b8e12186d0a74a1f1ed0096bc4351228d7a21acd0163fa7
local     ea1add76142e43a1db82045b08d4395d800fd144a7b324396d3357ae3b387eaa
local     fb3ffbaf29c12c48e14d2c0a91fd404372f70b06642c2540388b22e3a18facfa
local     mdb
local     mongodb-data
local     tomcat-data



```


### Paso 3: Crear el Dockerfile

A continuación, creamos un Dockerfile que instalará Tomcat, MariaDB y CloudBeaver.

```code/bash/textplan/console
# Usar una imagen base de Ubuntu para las instalaciones adicionales
FROM ubuntu:20.04

# Instalar dependencias necesarias (como wget y curl)
RUN apt-get update -y && \
    apt-get install -y \
    wget \
    curl \
    unzip \
    mysql-client \
    && rm -rf /var/lib/apt/lists/*

# Configurar MariaDB usando la imagen oficial
FROM mariadb:10.5

# Configurar Tomcat usando la imagen oficial
FROM tomcat:9.0

# Descargar y configurar CloudBeaver utilizando la imagen oficial de CloudBeaver desde Docker Hub
FROM dbeaver/cloudbeaver:latest

# Exponer puertos
EXPOSE 8080 8081

# Volúmenes para MariaDB
VOLUME /var/lib/mysql

# Configuración de MariaDB: Establecer la contraseña root y crear la base de datos (esto es suficiente con las variables de entorno)
ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=exampledb

# Iniciar los servicios de MariaDB, Tomcat y CloudBeaver
CMD service mysql start && \
    /opt/tomcat/bin/catalina.sh run & \
    /opt/cloudbeaver/cloudbeaver/bin/cloudbeaver & \
    wait
```




### Paso 4: Construir y ejecutar la imagen

Para construir la imagen desde el Dockerfile, usa el siguiente comando:


```code/bash/textplan/console
docker build -t tomcat-mariadb-cloudbeaver .
```
Lista los contenedores que tienes en tu equipo:
```code/bash/textplan/console
docker ps -a 
CONTAINER ID   IMAGE                                        COMMAND                  CREATED       STATUS                     PORTS                                                 NAMES
dcc136de57f5   mongo-express:latest                         "/sbin/tini -- /dock…"   5 days ago    Exited (143) 5 days ago                                                          mongo-express-container
8d9fa0acf9ba   mongo:latest                                 "docker-entrypoint.s…"   5 days ago    Exited (0) 5 days ago                                                            mongodb-container
450f16bedf5d   danileonpe/app-pujas-nginx-webserver-image   "/docker-entrypoint.…"   7 days ago    Exited (1) 7 days ago                                                            pujas-server2
4916518c1a19   danileonpe/app-pujas-image                   "docker-php-entrypoi…"   7 days ago    Exited (255) 5 days ago    9000/tcp, 0.0.0.0:9091->8080/tcp, :::9091->8080/tcp   pujas-server
59a93bb48126   dbeaver/cloudbeaver:latest                   "./run-server.sh"        11 days ago   Exited (143) 11 days ago                                                         cloudbeaver
76d3784a5e76   mariadb:latest                               "docker-entrypoint.s…"   11 days ago   Created                                                                          mariadb-container
0d09c052db37   hello-world                                  "/hello"                 11 days ago   Exited (0) 11 days ago                                                           great_goldwasser

```
Luego, para ejecutar el contenedor que contiene Tomcat, MariaDB y CloudBeaver, usa:
```code/bash/textplan/console
docker run -d -p 8080:8080 -p 8081:8081 tomcat-mariadb-cloudbeaver
677798b4b41adb19e7e2bcd5544d463ab262afe0576a643c55ab53415ece4da0
```

### Detener y eliminar contenedores
Cuando termines de trabajar con CloudBeaver/MariaBD, puedes detener y eliminar el contenedor con los siguientes comandos:

```code/bash/textplan/console
docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED          STATUS          PORTS                                                                                                      NAMES
595f05c4a1d1   tomcat-mariadb-cloudbeaver   "./run-server.sh /bi…"   29 seconds ago   Up 27 seconds   0.0.0.0:8080-8081->8080-8081/tcp, :::8080-8081->8080-8081/tcp, 0.0.0.0:8978->8978/tcp, :::8978->8978/tcp   funny_black
docker stop funny_black
funny_black
docker rm funny_black
funny_black
```



