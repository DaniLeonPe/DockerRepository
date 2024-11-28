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

A la hora de intentar acceder a localhost:8978 se queda cargando la pagina 
