![image](https://github.com/user-attachments/assets/f47074cb-e286-40e2-89f7-48a7412c6e76)
# Practica 6

##  Volúmenes en Docker


### Redes disponibles

listamos el conjunto de redes disponibles en el momento

```code/bash/textplan/console
docker network ls
NETWORK ID     NAME             DRIVER    SCOPE
195addfaef40   bridge           bridge    local
c8ff60fe92b3   host             host      local
0e3d991c8d01   none             null      local
15c8856d6552   tomcat-network   bridge    local


```
<img src=../img/vol1.PNG>


### Pasos a Seguir

#### Crear una Red personalizada

Creamos una red personalizada para que los contenedores puedan comunicarse entre sí

```code/bash/textplan/console
 docker network create mongodb-network
0cd64b1553f636633fd4557af81ba3a3b22174114be7207a245d05b8001915f9
 docker network ls
NETWORK ID     NAME              DRIVER    SCOPE
195addfaef40   bridge            bridge    local
c8ff60fe92b3   host              host      local
0cd64b1553f6   mongodb-network   bridge    local
0e3d991c8d01   none              null      local
15c8856d6552   tomcat-network    bridge    local


```

<img src=../img/vol2.PNG>

#### Crear un Volumen para MongoDB

Creamos un volumen para mongoDB 
```code/bash/textplan/console
docker volume create mongodb-data
mongodb-data
alumno@alumno-aed:~$ docker volume ls
DRIVER    VOLUME NAME
local     33352a59b2f87aad29d07d823de9e6bfcf93d2b58054ae914e75d376a08711ea
local     b04f97b8d432fd616b8e12186d0a74a1f1ed0096bc4351228d7a21acd0163fa7
local     mongodb-data
local     tomcat-data

```

<img src=../img/vol3.PNG>


#### Levantar el Contenedor MongoDB

Usamos el siguiente comando para ejecutar MongoDB con el volumen y la red configurados
```code/bash/textplan/console
docker run -d --name mongodb-container \
>   --network mongodb-network \
>   -e MONGO_INITDB_ROOT_USERNAME=admin \
>   -e MONGO_INITDB_ROOT_PASSWORD=admin123 \
>   -v mongodb-data:/data/db \
>   -p 27017:27017 \
>   mongo:latest
Unable to find image 'mongo:latest' locally
latest: Pulling from library/mongo
de44b265507a: Pull complete 
4d73348b9ac0: Pull complete 
6f1309d23164: Pull complete 
e4bde7d374c0: Pull complete 
9a0eb01246c7: Pull complete 
d2b3dabec753: Pull complete 
8606fc5459f6: Pull complete 
8f50be4b980b: Pull complete 
Digest: sha256:8565ecda5b221016d70f7745ac1ba0b97ccb05836157f8a343e987338fdc8350
Status: Downloaded newer image for mongo:latest
2d75780cd7f04823a86dc9269dc06d3a3f3e9e81a17a070c4e5be42281b14ebb

```
<img src=../img/vol4.PNG>



#### Levantar el Contenedor Mongo Express

Usamos el siguiente comando para levantar el contenedor
```code/bash/textplan/console
docker run -d --name mongo-express-container \
>   --network mongodb-network \
>   -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
>   -e ME_CONFIG_MONGODB_ADMINPASSWORD=admin123 \
>   -e ME_CONFIG_MONGODB_SERVER=mongodb-container \
>   -p 8081:8081 \
>   mongo-express:latest
Unable to find image 'mongo-express:latest' locally
latest: Pulling from library/mongo-express
619be1103602: Pull complete 
7e9a007eb24b: Pull complete 
5189255e31c8: Pull complete 
88f4f8a6bc8d: Pull complete 
d8305ae32c95: Pull complete 
45b24ec126f9: Pull complete 
9f7f59574f7d: Pull complete 
0bf3571b6cd7: Pull complete 
Digest: sha256:1b23d7976f0210dbec74045c209e52fbb26d29b2e873d6c6fa3d3f0ae32c2a64
Status: Downloaded newer image for mongo-express:latest
9030f1624ba5e6be05bc5050224ed02b3ec81c8b1f10116f578ea2cc08151307


```
<img src=../img/vol5.PNG>



#### Verificar los contenedores activos
Listamos los contenedores activos

```code/bash/textplan/console
docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS              PORTS                                           NAMES
9030f1624ba5   mongo-express:latest   "/sbin/tini -- /dock…"   About a minute ago   Up About a minute   0.0.0.0:8081->8081/tcp, :::8081->8081/tcp       mongo-express-container
2d75780cd7f0   mongo:latest           "docker-entrypoint.s…"   2 minutes ago        Up 2 minutes        0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   mongodb-container

```
<img src=../img/vol6.PNG>

#### Verificar los logs de Mongo Express

Verificamos los logs de Mongo Express:


```code/bash/textplan/console
docker logs mongo-express-container
Waiting for mongo:27017...
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:35:57 UTC 2024 retrying to connect to mongo:27017 (2/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:03 UTC 2024 retrying to connect to mongo:27017 (3/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:09 UTC 2024 retrying to connect to mongo:27017 (4/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:15 UTC 2024 retrying to connect to mongo:27017 (5/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:21 UTC 2024 retrying to connect to mongo:27017 (6/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:27 UTC 2024 retrying to connect to mongo:27017 (7/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:33 UTC 2024 retrying to connect to mongo:27017 (8/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:39 UTC 2024 retrying to connect to mongo:27017 (9/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:45 UTC 2024 retrying to connect to mongo:27017 (10/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
No custom config.js found, loading config.default.js
Welcome to mongo-express 1.0.2
------------------------


Mongo Express server listening at http://0.0.0.0:8081
Server is open to allow connections from anyone (0.0.0.0)
basicAuth credentials are "admin:pass", it is recommended you change this in your config.js!

```
Verificamos en el navegador la siguiente direccion:

localhost:8081


<img src=../img/vol7.PNG>

al hacer nuevamente el log al entrar en la direccion y verificando el nombre de usuario y la contraseña el logs seria el siguiente:


```code/bash/textplan/console
docker logs mongo-express-container
Waiting for mongo:27017...
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:35:57 UTC 2024 retrying to connect to mongo:27017 (2/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:03 UTC 2024 retrying to connect to mongo:27017 (3/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:09 UTC 2024 retrying to connect to mongo:27017 (4/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:15 UTC 2024 retrying to connect to mongo:27017 (5/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:21 UTC 2024 retrying to connect to mongo:27017 (6/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:27 UTC 2024 retrying to connect to mongo:27017 (7/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:33 UTC 2024 retrying to connect to mongo:27017 (8/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:39 UTC 2024 retrying to connect to mongo:27017 (9/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
Wed Dec  4 07:36:45 UTC 2024 retrying to connect to mongo:27017 (10/10)
/docker-entrypoint.sh: line 15: mongo: Try again
/docker-entrypoint.sh: line 15: /dev/tcp/mongo/27017: Invalid argument
No custom config.js found, loading config.default.js
Welcome to mongo-express 1.0.2
------------------------


Mongo Express server listening at http://0.0.0.0:8081
Server is open to allow connections from anyone (0.0.0.0)
basicAuth credentials are "admin:pass", it is recommended you change this in your config.js!
GET / 200 123.877 ms - 9260
GET /public/css/bootstrap.min.css 200 3.041 ms - 121457
GET /public/css/bootstrap-theme.min.css 200 0.865 ms - 23411
GET /public/css/style.css 200 1.194 ms - 1883
GET /public/img/mongo-express-logo.png 200 0.550 ms - 17847
GET /public/vendor-93f5fc3ae20e0dfd68cb.min.js 200 0.702 ms - 131153
GET /public/index-56afe067afbbbde795be.min.js 200 0.975 ms - 936
GET /public/fonts/glyphicons-halflings-regular.woff2 200 1.095 ms - 18028
GET /public/img/gears.gif 200 0.784 ms - 50281


```
### Prueba la persistencia de BBDD

Accedemos a MongoDB desde el cliente y creamos una base de datos:

<img src=../img/vol8.PNG>

#### Crear la coleccion users

creamos la coleccion users:

<img src=../img/vol9.PNG>


#### Añadir Documentos a la colección users

-Abrimos la collección users
-Hacemos click en Add Document
-Escribimos un documento JSON, por ejemplo:


```code/bash/textplan/console
{
    "name": "John Doe",
    "email": "john@example.com",
    "age": 30
}

```
Por ultimo hacemos click en Save


<img src=../img/vol10.PNG>




### Verificacion

#### Red
Lanzamos el diagnóstico de red a través del siguiente comando:

```code/bash/textplan/console
docker network inspect mongodb-network
[
    {
        "Name": "mongodb-network",
        "Id": "0cd64b1553f636633fd4557af81ba3a3b22174114be7207a245d05b8001915f9",
        "Created": "2024-12-04T07:31:33.208544412Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "2d75780cd7f04823a86dc9269dc06d3a3f3e9e81a17a070c4e5be42281b14ebb": {
                "Name": "mongodb-container",
                "EndpointID": "12dd9c6c9c51c0c8e83efe421fe9c742d6c0bc89179e310ecb130eb2f649e64a",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            },
            "9030f1624ba5e6be05bc5050224ed02b3ec81c8b1f10116f578ea2cc08151307": {
                "Name": "mongo-express-container",
                "EndpointID": "d7b3049f0edf49dac747f2c15c810047c23dfbacd1f8fe5e4c477b09b53ff771",
                "MacAddress": "02:42:ac:13:00:03",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]


```

<img src=../img/vol11.PNG>


#### Conectividad con la BBDD

Realizamos la verificación con la BBDD:

```code/bash/textplan/console
docker exec -it mongodb-container mongosh -u admin -p admin123
Current Mongosh Log ID:	675009b50cce66c276e94969
Connecting to:		mongodb://<credentials>@127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.3.4
Using MongoDB:		8.0.3
Using Mongosh:		2.3.4

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/


To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
You can opt-out by running the disableTelemetry() command.

------
   The server generated these startup warnings when booting
   2024-12-04T07:34:31.302+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
   2024-12-04T07:34:32.063+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2024-12-04T07:34:32.063+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2024-12-04T07:34:32.063+00:00: We suggest setting the contents of sysfsFile to 0.
   2024-12-04T07:34:32.063+00:00: Your system has glibc support for rseq built in, which is not yet supported by tcmalloc-google and has critical performance implications. Please set the environment variable GLIBC_TUNABLES=glibc.pthread.rseq=0
   2024-12-04T07:34:32.063+00:00: vm.max_map_count is too low
   2024-12-04T07:34:32.063+00:00: We suggest setting swappiness to 0 or 1, as swapping can cause performance problems.
------

test> 

```

<img src=../img/vol12.PNG>

utilizamos la bbdd testdb:


```code/bash/textplan/console
use testdb
```
<img src=../img/vol13.PNG>

Listamos las colecciones que hay disponibles:

```code/bash/textplan/console
show collections
```
<img src=../img/vol14.PNG>


Añadimos un nuevo documento a la coleccion:

```code/bash/textplan/console
db.users.insertOne({
    name: "Pepe",
    email: "quiero-ser-como-pepe@example.com",
    age: 65
})
```
Mostramos los valores almacenados:

```code/bash/textplan/console
testdb> db.users.find()
[
  {
    _id: ObjectId('675008d649f911fd44cdb22c'),
    name: 'John Doe',
    email: 'john@example.com',
    age: 30
  },
  {
    _id: ObjectId('67500a870cce66c276e9496a'),
    name: 'Pepe',
    email: 'quiero-ser-como-pepe@example.com',
    age: 65
  }
]

```
<img src=../img/vol15.PNG>

Ejecutamos exit para salir


### Detener y eliminar contenedores
Paramos y eliminamos el contenedor MongoDB

```code/bash/textplan/console
docker stop mongo-express-container
mongo-express-container
docker rm mongo-express-container
mongo-express-container
docker stop mongodb-container
mongodb-container
docker rm mongodb-container
mongodb-container
docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

### Instalacion de los contenedores
Se realiza nuevamente la instalacion de los contenedors y se verifica el estado de la bbdd testdb viendo que sigue estando la base de datos exactamente igual

<img src=../img/vol16.PNG>
