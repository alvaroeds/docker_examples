
- [contenedores](#contenedores)
  - [El estado](#el-estado)
  - [Ejecutar un contenedor (docker run)](#ejecutar-un-contenedor-docker-run)
    - [Comando Interactivo -it](#comando-interactivo--it)
    - [Comando --detach (-d)](#comando---detach--d)
    - [Comando exec](#comando-exec)
  - [Eliminar un contenedor (docker rm)](#eliminar-un-contenedor-docker-rm)
  - [Logs del contenedor (docker logs)](#logs-del-contenedor-docker-logs)
  - [Exponer contenedores al mundo exterior](#exponer-contenedores-al-mundo-exterior)
  - [Variables de enorno](#variables-de-enorno)


# contenedores

- Son la pieza fundamental de docker.
- Todos los contenedores tienen un id único
- Es una agrupación de uno o más procesos
- Ejecuta sus procesos de forma nativa
- Los contenedores ven su universo y no fuera de el
- No tienen forma de consumir más recursos de las que el contenedor les permite

## El estado

Para listar todos los contenedores de Docker, utilizamos el comando :

```docker
    docker ps       # -> Lisra contenedores en uso
    docker ps -a    #-> Lista todos los contenedores
    docker ps -aq   #-> Lista los id de todos los contendores
```

Podemos inspeccionar un contenedor en específico utilizando **inspect**:

```docker
    docker inspect nombreDelContenedor
                   idDelContenedor
```

Podemos filtrar un contenido especifico de Docker con el comando **filter**:

```docker
                   -f '{{ json .contenido.especifico }}'
    docker inspect -f '{{ json .Config.Env }}' nombreDelContenedor
                                               idDelContenedor
```       

Podemos renombrar un contenedor con **rename**:

```docker
    docker rename nombreDelContenedor nuevoNombreContenedor
```

## Ejecutar un contenedor (docker run)

Siempre que queremos crear un contenedor se hace con el comando **docker run**

Podemos asignarle un nombre al momento de crear el contenedor

```docker
    docker run --name nombreContenedor imagenContedor
    docker run --name prueba hello-world
    docker run ubuntu
```

### Comando Interactivo -it

Para que ejecutar una imagen de forma interactiva podemos agregar en comando **-it**

```docker
    docker run -it ubuntu
```

### Comando --detach (-d)

Este comando es muy efecaz, porque permite olvidarte del como y dejar que docker resuelva si el contenedor
tiene un output (tail), es iteractivo (-it) y te devuelva el control de la terminal.

```docker
    docker run --detach --name nombreContenedor imagenContenedor
    docker run -d --name server nginx
    docker run -d ubuntu tail -f /dev/null
```

>Al usar comandos al iniciar un contenedor, se le asigna el Process ID 1 a ese comando

### Comando exec

Para ejecutar un comando en un contenedor existente se usa **exec**

```docker
    docker exec -it nombreContendor bash
```

## Eliminar un contenedor (docker rm)

Podemos eliminar un contendor con **docker rm**

```docker
    docker rm nombreContenedor
```

Para eliminar un contedor que está corriendo podemos usar **-f**

```docker
    docker rm -f nombreContenedor
```

Si queremos eliminar todos los contenedores existentes podemos usar

```docker 
    docker rm $(docker ps -aq)
```

## Logs del contenedor (docker logs)

Podemos ver el out-put de cualquier contendor se usa el comando **docker logs** (no lo ejecuta, solo imprime el log)

```docker
    docker logs nombre_o_ID_del_Contendor
    docker logs -f id_Del_Contenedor
```

## Exponer contenedores al mundo exterior

Los contenedores están aislados del sistema y a nivel de red, cada contenedor tiene su propio stack de net y sus propios puertos.

Debemos redirigir los puertos del contenedor a los de la computadora(host) y lo podemos hacer al utilizar el comando publish (-p) de la siguiente manera **-p puertoHost:puertoContedor"**:


        docker run -d --name nombreContenedor -p 8080:80 nombreImagen
        docker run -d --name webserver -p 8080:80 nginx

## Variables de enorno

> --env nos permite crear una variable de entorno al momento de crear el contenedor

```docker
docker run --rm d --env PRUEBA='datosPrueba' --name prueba ubuntu
```
