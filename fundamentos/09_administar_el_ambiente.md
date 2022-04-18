- [Administrar tu ambiente](#administrar-tu-ambiente)
  - [Eliminar recursos que están frenados](#eliminar-recursos-que-están-frenados)
  - [Limpiar todo el sistema](#limpiar-todo-el-sistema)
  - [Limites de memoria](#limites-de-memoria)

# Administrar tu ambiente

Para adminsitrar nuestro ambiente podemos usar comandos que nos ayudan a limpiar rapidamente nuestro sistema.

## Eliminar recursos que están frenados

Usamos Prune en cualquier recurso como containers, volumnes, imagenes

```docker
docker container prune
docker image prune
docker network prune
...
```

## Limpiar todo el sistema

Para limpiar todo el sistema docker podemos usar

```docker
docker system prune
```

## Limites de memoria

Podemos asignar limites de memoria a un contenedor al momento de ser ejecurato

```docker
docker run -d --name nombreContenedor --memmory 1g ubuntu
```

> Podemos ver la memoria del recurso con el comando: ***docker stats***