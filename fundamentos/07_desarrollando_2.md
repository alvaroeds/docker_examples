- [Desarrollando con docker 2](#desarrollando-con-docker-2)

# Desarrollando con docker 2

Conectaremos nuestro ejemplo de desarollo a una base de datos mongo para que deje de darnos error.

1. Creamos un nuevo network para conectar nuestros contenedores

    ```docker
    docker network create pruebanet
    ```

2. Creamos un contenedor de mongo
   
    ```docker
    docker run -d --name db mongo
    ```

3. Conectamos el contenedor mongo a nuestra network

    ```docker
    docker network connect pruebanet db
    ```

4. Ejecutamos el contenedor de nuestra app de prueba (usar la imagen del proyecto de [prueba](./docker_desarrollo/Dockerfile))

    ```docker
    docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/test pruebanode
    ```

5. Conectamos el contenedor de nuestra app a nuestra network

    ```docker
    docker network connect pruebanet app
    ```

6. si todo salió bien, podrás ven el resultado en [localhost:3000](http://localhost:3000)