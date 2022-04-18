- [Networking](#networking)
    - [Listar las redes de docker](#listar-las-redes-de-docker)
    - [Crear una nueva network](#crear-una-nueva-network)
    - [Poner un contenedor dentro de una network](#poner-un-contenedor-dentro-de-una-network)

# Networking

Podemos conectar varios contenedores de una manera fácil sencilla y rapida mediante una red creada por docker llamada ***network***.


### Listar las redes de docker

```docker
docker network ls
```

Los network que vienen con docker son:

- **bridge**:
  -  Es la red donde por defecto se pueden conectar los contenedores.
- **host**: 
  - Es la forma que tiene docker para representar la red de mi maquina.
- **none**: 
  - Es el "/dev/null", basicamente si corremos un contenedor con este network deshabilitamos el networking para este.

### Crear una nueva network

```docker
docker network create --attachable nombreNetwork
```

> El comando **--attachable** es para que mas de un contenedor pueda ser asignado a la red.


### Poner un contenedor dentro de una network

```docker
docker network connect nombreNetwork nombreContenedor
```

> Para ver que contenedores tiene conectado a una red especifica podemos usar

```docker
docker network inspect nombreNetwork
```

> **IMPORTANTE**:
> 
> Los contenedores pueden verse entre sí, solo si estan conectados a la misma red. <br>
> Y pueden usar su nombre de contenedor como hostname (direccion de la computadora)