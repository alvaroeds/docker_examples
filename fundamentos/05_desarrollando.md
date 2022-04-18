- [Desarrollando con Docker](#desarrollando-con-docker)

# Desarrollando con Docker

Vamos a aplicar lo aprendido, y empezar a desarrollar con docker utlizando como base un proyecto desarrollado en node que lo puedes encontrar en la carpeta [docker_desarrollo](docker_desarrollo/).

Para ejecutar el dockerfile y crear una imagen hacemos docker 

```docker
build -t pruebanode .
```

Para crear un contenedor con la imagen que creamos

```docker
docker run --rm --name nombreContenedor -p 3000:3000 pruebanode
```

> **--rm** nos permite eliminar el contenedor una vez que se deje de ejecutar

Para poder correr nodemon (actualizar auitomaticamente) se debe montar el sistema de archivos con:

```docker
docker run --rm -p 3005:3000 -v rutaArchivos:rutaContenedor pruebanode
```

> Si todo salió bien, ahora puedes ir a [localhost:3000](http://localhost:3000) y ver tus cambios

> Aún vemos un error con una conexión a mongoDB. Usaremos networking para solucionar la comunicación entre contenedores.
