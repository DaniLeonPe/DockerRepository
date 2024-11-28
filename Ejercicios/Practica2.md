# Actividad2:

## **Objetivo**
Configurar un contenedor Docker que ejecute Apache Tomcat y que esté accesible desde un puerto específico en la máquina anfitriona.



## **Paso 1: Preparación del Entorno**

1. Verifica que Docker está instalado y funcionando:
  ```code/bash/textplan/console
   docker --version
```

## Paso 2: Descargar la imagen de Tomcat

 ```code/bash/textplan/console
   docker pull tomcat

```

Resultado:
```code/bash/textplan/console
   Using default tag: latest
latest: Pulling from library/tomcat
afad30e59d72: Pull complete
918d361e6529: Pull complete
cf4dd2a7e40b: Pull complete
d152af7a0148: Pull complete
a5d7958ebd69: Pull complete
409b41a58ed4: Pull complete
4f4fb700ef54: Pull complete
9eabaa92f491: Pull complete
Digest: sha256:2ade2b0a424a446601688adc36c4dc568dfe5198f75c99c93352c412186ba3c9
Status: Downloaded newer image for tomcat:latest
docker.io/library/tomcat:latest


```

se confirma si la imagen se ha descargado correctamente.

```code/bash/textplan/console
sudo docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
tomcat        latest    f77539e7e45f   2 weeks ago     467MB
hello-world   latest    d2c94e258dcb   19 months ago   13.3kB
```

## Paso 3: Ejecutar el contenedor de Tomcat

```code/bash/textplan/console
sudo docker run -d -p 9090:8080 --name tomcat-server tomcat
42281df4f20f08e8c7c6651604fa0152b0cd7ba8df848401bf0104b4a6de9e9c
```

```code/bash/textplan/console  
sudo docker ps
CONTAINER ID   IMAGE     COMMAND             CREATED          STATUS          PORTS                                       NAMES
42281df4f20f   tomcat    "catalina.sh run"   32 seconds ago   Up 31 seconds   0.0.0.0:9090->8080/tcp, :::9090->8080/tcp   tomcat-server
```


## Paso 4: Probar la configuracion

1. abre un navegador web y escribe la siguiente URL:

http://localhost:9090



2. Se accede a los logs para ver si el arranque ha sido correcto

```code/bash/textplan/console
sudo docker logs tomcat-server

27-Nov-2024 19:24:04.810 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in [142] milliseconds

```

## Paso 5: Detener y Eliminar el contenedor

1.Deten el contenedor
```code/bash/textplan/console
sudo docker stop tomcat-server
```
2. Eliminar el contenedor
```code/bash/textplan/console
sudo docker rm tomcat-server
```

3. Eliminar la imagen de tomcat
```code/bash/textplan/console
sudo docker rmi tomcat
```

## Reto Adicional
Arranca apache tomcat en otro puerto

```code/bash/textplan/console  
sudo docker run -d -p 9091:8080 --name tomcat-server tomcat
a13d1863a556be415f33a1741d05d18fc8fa8ea3ab44a6acfdb12029bd5adcf8
```


1-creamos un volumne Docker
```code/bash/textplan/console
sudo docker volume create tomcat-volume
```
2-creamos un contenedor con el tomcat y montamos el volumne
```code/bash/textplan/console
docker run -d -p 9090:8080 \
--name tomcat-server \
-v tomcat-data:/usr/local/tomcat/conf \
tomcat
```

Se comprueba en el navegador que el puerto 9090 está corriendo


3- se verifica los logs del servidor
```code/bash/textplan/console
sudo docker logs tomcat-server
27-Nov-2024 19:35:52.091 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in [181] milliseconds
```
