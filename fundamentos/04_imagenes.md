- [Imágenes](#imágenes)
  - [Crear tus propias imagenes](#crear-tus-propias-imagenes)
    - [Ejecutar un Dockerfile](#ejecutar-un-dockerfile)
  - [Sistema de capas](#sistema-de-capas)

# Imágenes

Las imágenes son un componente fundamental de Docker y sin ellas los contenedores no tendrían sentido.
<br>
Son fundamentalmente plantillas o templates.

> Debemos tener en cuenta es que las imágenes no van a cambiar, es decir que una vez este construida no la podremos cambiar.

> Al nombre de las imagenes se les dice repositorio.

<br>
Para obtener una imagen se usa el comando ***pull*** y el nombre de la imagen

```docker
docker pull redis
```

Para listar las imaganes que tienes actualmente se usa image ls

```docker
docker image ls
```

> Se puede especificar la version que deseas descargar
> ```docker
> docker pull ubuntu:18.04
> ```

## Crear tus propias imagenes

Vamos a crear nuestras propias imágenes, necesitamos un archivo llamado ***DockerFile*** que es la “***receta***” o "***molde*** que utiliza Docker para crear imágenes.

> Es importante que el DockerFile siempre empiece con un “FROM” y le indiquemos que imagen usará el contenedor.

```docker
FROM ubuntu

RUN touch /usr/src/helllo-world
```

>El comando "RUN" le indica una acción a docker

> El archivo de esta imagen esta [aquí](first_image_create/Dockerfile)

### Ejecutar un Dockerfile

Para ejecutar un dockerfile usamos

```docker
docker build -t ubuntu:prueba .
```

Donde **build** ejecuta **-t** le pone nombre y el tag (nombre:tag)  el **. (punto)** es el path, osea el contexto de build

Para poder cambiar el repositori:tag de una imagen podemos usar

```docker
docker tag ubuntu:prueba repo/ubuntu:prueba
```

Si queremos hacer push de una imagen a nuestro docker hub, debemos usar push

```docker
docker push repository:tag
```

## Sistema de capas

Se basa en los Layer, es decir todos los cambios del contenedor que adquiere desde el docker file.

Podemos ver el history de estos cambios con

```docker
docker history ubuntu:prueba
```

>Hay una herramienta para poder ver los leyer con una interfaz amigable, les dejo el link de Dive: https://github.com/wagoodman/dive

Lo que hay entender del sistemas de cambio es que cada layer esta compueso por los cambios del contenedor, para tener una idea de como funciona debes pensarlo como en un control de versiones.

Estas capas te indican que instrucciones, archivos y cambios a afectado al contenedor desde el dockerfile.

> Ejemplo:
>
> 1. Sí creo un archivo (layer 1)
> 2. Elimino el mismo archivo (layer 2)

Debes tener en cuenta que docker tiene un cache que ayuda al momento de build de una imagen
pero si alteras algo que esta relacionado a un layer, los demas comando despues de ese,
vuelven a cargar, es por eso que siempre debes optimizar el dockerfile como buena practica.