- [Docker-compose](#docker-compose)
  - [Docker override](#docker-override)
  - [Escalar con docker-compose](#escalar-con-docker-compose)
  - [Docker ignore](#docker-ignore)


# Docker-compose

El archivo Compose es un archivo YAML que define servicios, redes y volúmenes para una aplicación Docker.

Docker compose es una herramienta que nos permite describir de forma declarativa la arquitectura de nuestra aplicación.

se usa en un arcivo ***docker-compose.yml*** Para saber mas de esto puedes leer:

- https://docs.docker.com/compose/install/#install-compose
- https://docs.docker.com/compose/compose-file/compose-versioning/
- https://docs.docker.com/compose/startup-order/

Tenemos un ejemplo dentro del [proyecto](./docker_desarrollo/docker-compose.yml) solo debes usar el siguiente comando para activarlo

```docker
docker-compose up -d
```

> Docker compose hara todo de maner automatica

Algunos comandos para docker-compose:

- docker-compose ps
- docker-compose up -d
- docker-compose down
- docker-compose logs -f nombreContenedor
- docker-compose logs -f nombreServicio1 nombreSetrvicio2

## Docker override

Este archivo debe ser definido como : **docker-compose.override.yml**

Este fichero sobreescribira y definira cosas sobre **docker-compose.yml** para poder hacer cambios de manera local sin afectar el fichero original que se usa regularmente en equipo.

para encontrar el archivo override click [aquí](./docker_desarrollo/docker-compose.override.yml)

## Escalar con docker-compose

Podemos escalar los servicios de docker-compose facilmente con solo un comando

```docker
  docker-compose up -d --scale app=2
```

> Esto nos permite crear contenedores replicas para escalar el servicio


## Docker ignore

docker ignore nos sirve par aignorar documentos y carpetas para que el contexto de build no lo note