
# Practica 6

## Configuración de un balanceador de carga nginx con dos servidores tomcat


### Redes disponibles

listamos el conjunto de redes disponibles en el momento

```code/bash/textplan/console
sudo docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
64aa82badc9b   bridge    bridge    local
c8ff60fe92b3   host      host      local
0e3d991c8d01   none      null      local

```


### Pasos a Seguir

#### crear una Red Docker

Creamos una red personalizada para que los contenedores puedan comunicarse entre sí

```code/bash/textplan/console
sudo docker network create tomcat-network
15c8856d65523056cd5f47c6be4a89d82ecd2159d2a1374854876a5a3cbaba18

```

#### Levanta los Servidores Tomcat

levantamos dos contenedores tomcat conectandolos a la red 
```code/bash/textplan/console
sudo docker run -d --name tomcat1 --network tomcat-network -p 8081:8080 tomcat:latest
c273ea4ef2d173b05d77fcd315555a1bcedcdd9f34129935f7c15ddd253e20ee

sudo docker run -d --name tomcat2 --network tomcat-network -p 8082:8080 tomcat:latest
3fa58aac9a68a5b9781f5a154a973d4c862c99ce553cdc71f937fb39c37c51e5

```

Hacemos la comprobacion de que estan activos y disponibles

```code/bash/textplan/console
sudo docker ps
CONTAINER ID   IMAGE           COMMAND             CREATED              STATUS              PORTS                                       NAMES
3fa58aac9a68   tomcat:latest   "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:8082->8080/tcp, :::8082->8080/tcp   tomcat2
c273ea4ef2d1   tomcat:latest   "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:8081->8080/tcp, :::8081->8080/tcp   tomcat1
```
#### Fichero de configuracion de balanceador NGINX

creamos el fichero de balance nginx.conf en el mismo directorio donde estamos ejecutando la consola de comandos
```code/bash/textplan/console
nano nginx.conf

events {}

http {
    upstream tomcat_backend {
        server tomcat1:8080;
        server tomcat2:8080;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://tomcat_backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
}
```

Creamos un contenedor con la ultima version de __NGINX__ y asociamos el contenedor a la red personalizada tomcat-network utilizando el archivo de configuracion  personalizado __nginx.conf__

```code/bash/textplan/console
sudo docker run -d --name nginx --network tomcat-network -p 82:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf nginx:latest
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
2d429b9e73a6: Pull complete 
20c8b3871098: Pull complete 
06da587a7970: Pull complete 
f7895e95e2d4: Pull complete 
7b25f3e99685: Pull complete 
dffc1412b7c8: Pull complete 
d550bb6d1800: Pull complete 
Digest: sha256:0c86dddac19f2ce4fd716ac58c0fd87bf69bfd4edabfd6971fb885bafd12a00b
Status: Downloaded newer image for nginx:latest
ed11f4452a85795696faf4660b069499000a601e30f000f07279efcca3e74c68

````

### Verificar que todo esta en funcionamiento

#### Servidor NGINX

Se verifica el comportamiento en:
```code/bash/textplan/console
http://localhost:8081

```
<img src=../img/nginx1.PNG>

```code/bash/textplan/console
http://localhost:8082

```
<img src=../img/nginx2.PNG>

```code/bash/textplan/console
http://localhost:82

```
<img src=../img/nginx3.PNG>






Realizamos el despliege de la aplicacion sample en ambos contenedores

```code/bash/textplan/console
sudo docker cp /home/alumno/Escritorio/sample.war tomcat1:/usr/local/tomcat/webapps/
Successfully copied 6.66kB to tomcat1:/usr/local/tomcat/webapps/
sudo docker cp /home/alumno/Escritorio/sample.war tomcat2:/usr/local/tomcat/webapps/
Successfully copied 6.66kB to tomcat2:/usr/local/tomcat/webapps/
```

volvemos a verificar el comportamiento en:

```code/bash/textplan/console
http://localhost:8081

```
<img src=../img/nginx4.PNG>

```code/bash/textplan/console
http://localhost:8082

```
<img src=../img/nginx5.PNG>

```code/bash/textplan/console
http://localhost:82

```
<img src=../img/nginx6.PNG>


### Detener y eliminar contenedores
Detenemos y eliminamos los conetendores con los siguientes comandos
```code/bash/textplan/console
 sudo docker stop tomcat1
tomcat1

 sudo docker stop tomcat2
tomcat2

 sudo docker rm tomcat1
tomcat1

 sudo docker rm tomcat2
tomcat2

 sudo docker stop nginx
nginx

 sudo docker rm nginx
nginx

 sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

