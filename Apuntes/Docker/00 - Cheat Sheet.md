---
tags:
  - utilidades/docker
---
# Contenedores
Crear e ejecutar un [[Apuntes/Docker/01 - Introducción#Contenedor|contenedor]] con un nombre personalizado.
```bash
 docker run --name <nombre_contenedor> <nombre_imagen>
```

Crear e ejecutar un contenedor expoñendo un puerto.
```bash
docker run -p <host_port>:<puerto_contenedor> <nombre_imagen>
```

Ejecutar un contenedor en segundo plano.
```bash
docker run -d <nombre_imagen>
```

Eliminar todos os contenedores parados.
```bash
docker container prune
```

Iniciar ou detener un contenedor existente.
```bash
docker start|stop <nome_contenedor> (ou <id_contenedor>)
```

Eliminar un contenedor parado.
```bash
docker rm <nombre_contenedor> (ou <id_contenedor>)
```

Ejecutar unha shell dentro do contenedor.
```bash
docker exec -it <nombre_contenedor> bash
```

Ver os logs de un contenedor. A opción `-f` sirve para seguir os logs.
```bash
docker logs -f <nombre_contenedor>
```

Ver información de un contenedor en ejecución.
```bash
docker inspect <nombre_contenedor> (ou <id_contenedor>)
```

Listar todos os contenedores en ejecución.
```bash
docker ps
```

Listar todos os contenedores (en ejecución e parados).
```bash
docker ps -a
```

Ver as estadísticas de recursos.
```bash
docker container stats
```

Cambiar o nombre de un contenedor.
```bash
docker rename <nombre_contenedor> <novo_nombre>
```
# Imágenes
Construir unha [[Apuntes/Docker/01 - Introducción#Imágen|imagen]] desde un [[Apuntes/Docker/01 - Introducción#Dockerfile|Dockerfile]].
```bash
docker build -t <nombre_imagen>
```

Construir unha imágen desde un Dockerfile sin cache.
```bash
docker build -t <nombre_imagen> . -no-cache
```

Listar as imágenes locales.
```bash
docker images
```

Borrar unha imágen.
```bash
docker rmi <nombre_imagen>
```

Borrar todas as imágenes sin utilizar.
```bash
docker image prune
```
# Volúmenes
Crear un [[Apuntes/Docker/01 - Introducción#Volumen|volumen]].
```bash
docker volume create <nombre_volumen>
```

Mostrar información detallada de un volumen.
```bash
docker volume inspect <nombre_volumen>
```

Listar os volúmenes.
```bash
docker volume ls
```

Eliminar volúmenes.
```bash
docker volume rm <nombre_volumen
```

Eliminar volúmenes non utilizados.
```bash
docker volume prune
```

Montar un directorio local en un contenedor.
```bash
docker run -d -v /home/jano:/var/www/html <nombre_imagen>
```
# Sistema
Mostrar o uso de disco de [[Apuntes/Docker/01 - Introducción#Qué é?|Docker]].
```bash
docker df
```

Mostrar o uso de disco de Docker de maneira detallada.
```bash
docker system df -v
```

Mostrar información do sistema de Docker.
```bash
docker info
```

Mostrar a versión de Docker.
```bash
docker version
```
# Docker Compose
Crear e ejecutar os servicios.
```bash
docker compose up
```

Crear e ejecutar os servicios en segundo plano.
```bash
docker compose up -d
```

Ejecutar un comando único en un servicio.
```bash
docker compose run <servicio> <comando>
```

Parar todos os servicios.
```bash
docker compose stop
```

Eliminar todos os servicios.
```bash
docker compose down
```

Eliminar todos os servicios e os volumenes.
```bash
docker compose down -v
```

Listar os servicios.
```bash
docker compose ps
```

Listar solo os nombres dos servicios.
```bash
docker compose --services
```

Reiniciar os servicios.
```bash
docker compose restart
```

Parar e eliminar os servicios.
```bash
docker compose rm
```
# Docker Swarm
## Gestionar o swarm
Iniciar un swarm.
```bash
docker swarm init
```

Unirse a un swarm como nodo worker/manager (dependendo se se trata de un -token manager ou worker).
```bash
docker swarm init
```

Abandonar un swarm.
```bash
docker swarm leave
```

Actualizar un swarm.
```bash
docker swarm update
```

Gestionar os tokens.
```bash
docker swarm join-token
```
## Docker node
Mostrar información detallada de un ou máis nodos.
```bash
docker node inspect
```

Listar todos os nodos.
```bash
docker node ls
```

Ver as tareas que se ejecutan nos nodos.
```bash
docker node ps
```

Eliminar un nodo do swarm.
```bash
docker node rm
```

Actualizar un nodo.
```bash
docker node update
```

Promover un nodo worker a manager.
```bash
docker node promote <nodo>
```

Degradar un nodo manager a worker.
```bash
docker node demote <nodo>
```

Cambiar nodo a solo manager.
```bash
docker node update --availability drain <nodo>
```
## Docker service
Crear un novo servicio.
```bash
docker service create
```

Mostrar información detallada de un servicio.
```bash
docker service inspect
```

Obter os logs de un servicio.
```bash
docker service logs
```

Listar os servicios.
```bash
docker service ls
```

Listar as tareas de un ou máis servicios.
```bash
docker service ps
```

Eliminar un ou máis servicios.
```bash
docker service rm
```

Revertir os cambios na configuración de un servicio.
```bash
docker service rollback
```

Escalar as replicas dun ou máis servicios.
```bash
docker service scale
```

Actualizar un servicio.
```bash
docker service update
```
## Docker stack
Desplegar un stack.
```bash
docker stack deploy
```

Listar os stacks.
```bash
docker stack ls
```

Listar as tareas de un stack.
```bash
docker stack ps
```

Eliminar un ou máis stacks.
```bash
docker stack rm
```

Listar os servicios en un stack.
```bash
docker stack services
```
# Webgrafía
[GitHub - adrianlois/Docker-CheatSheet: Docker Cheat Sheet - Guía Referencia de Comandos Docker](https://github.com/adrianlois/Docker-CheatSheet)
