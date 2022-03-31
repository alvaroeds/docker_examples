# Datos en Docker

Esta herramienta nos permite recuperar datos que podíamos dar por perdido.
Existen tres maneras de hacer permanencia de datos:

- [Datos en Docker](#datos-en-docker)
  - [Mounts](#mounts)
  - [Volumns](#volumns)
  - [tmpfs (temporary file system mount)](#tmpfs-temporary-file-system-mount)
- [Insertar y extraer archivos de un contenedor](#insertar-y-extraer-archivos-de-un-contenedor)

Si queremos usar un contenedor que necesita datos, como una base de datos por ejemmplo podemos
solucionarlo con

## Mounts

Con esto podemos montar una carpeta externa dentro del contenedor y guardar data en ella que sera la misma tanto en el host como en en contenedor.

> Se suelen usar para hacer cambios rápidos desde el host hacia el contenedor.

Se usa con el comando -v

```docker
docker run -d -v /user/alvaro/prueba:/data/db --name mongodb_prueba mongo
docker run -d -v rutaHost:rutaContenedor --name nombreContenedor imagenContenedor
```

## Volumns

A diferencia de mount docker escribe en un ***docker area*** donde el resto de los procesos del host no deberian interactuar.

>Se suelen usar para compartir datos entre contenedores.

Para crear un volumen nuevo:

```docker
docker volume create nombreVolumen
```

Para ver los volumenes de docker usamos:

```docker
docker volume ls
```

Para borrar todos los volumenes que no están en uso por ningun contenedor:

```docker
docker volume prune
```

Con ***--mount*** podemos montar un volumen a un contenedor especifico.
<br>
Usamos la bandera ***src*** para el nombre del volumen a montar y el ***dst*** es la parte del contenedor donde se va a monatar el volumen. (**se separan por una ,**)

Podemos utilizar el siguiente comando:

```docker
docker run -d --name (name) --mount src=(nombreVolumen),dst=(RutaContenedor) mongo
docker run -d --name db --mount src=dbdata,dst=/data/db mongo
```

## tmpfs (temporary file system mount)

Guarda los archivos temporalmente y persiste los datos en la memoria del contenedor, cuando muera el contenedor mueren los datos.

# Insertar y extraer archivos de un contenedor

Usamos el comando ***docker cp*** para manipular datos de un contendor.

Para insertar datos a un contenedor usamos:

```docker
docker cp archivo.txt nombreContenedor:/testing/test.txt
```

Para extraer datos de un contenedor usamos:

```docker
docker cp nombreContenedor:/testing rutalocal
```