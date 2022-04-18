- [Detener correctamente](#detener-correctamente)
  - [SHELL](#shell)
  - [EXEC](#exec)
- [Ejecutar correctamente](#ejecutar-correctamente)
  - [EntryPoint](#entrypoint)
  - [CMD](#cmd)
- [Contexto de build](#contexto-de-build)
- [Multi-stage build](#multi-stage-build)
- [Docker in Docker](#docker-in-docker)

# Detener correctamente

Vamos a usar la iamgen construida en el la carpeta [docker_avanzado/loop](./docker_avanzado/loop/Dockerfile)

Esta imagen levanta un proceso loop que termina al momento de mandarle un "**SIGTERM**" a la consola del contenedor.

> Creamos y ejecutamos la imagen para crear un contenedor:

1. docker build -t loop .
2. docker run -d --name looper loop

> Ahora le enviamos un sigterm al contenedor

1. docker stop looper

La imagen está construita para ejecutar comandos con el formato **SHELL** o con el formato **EXEC**.

La diferencia entre ambos sucede a nivel de procesos internos dentro del contenedor.

## SHELL

Este formato se ejecuta como proceso principal y crea un proceso hijo para el comando que le mandamos. Al cual no le avisa cuando terminamos el proceso principal.


## EXEC

Este formato se ejecuta como proceso principal

# Ejecutar correctamente

## EntryPoint

## CMD

# Contexto de build

# Multi-stage build

# Docker in Docker