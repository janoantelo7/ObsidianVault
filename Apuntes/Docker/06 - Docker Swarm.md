---
tags:
  - contenedores
  - docker
---
# Que é?
Docker Swarm é una ferramenta de [[Apuntes/Docker/01 - Introducción#Qué é?|Docker]] que proporciona a capacidade de administrar e coordinar múltiples contenedores desplegados en diferentes nodos. Esencialmente, **Docker Swarm** converte un **grupo de máquinas** Docker en un **clúster de contenedores** coherente. Con Swarm, podes manexar unha gran cantidade de contenedores de manera fácil y eficiente, y tamén proporciona funcions como o equilibrio de carga e servicios de alta disponibilidade.
# Iniciando o docker swarm
Para iniciar o docker swarm, necesitamos ter docker instalado, e executamos o seguinte comando que nos creará un swarm manager, que é o responsable de controlar e orquestar o Docker swarm. Este delega as cargas de traballo nos nodos traballadores (workers).
```bash
docker swarm init --advertise-addr <swarm manager private IP>
```

Asegurarse de empregar a ip privada coa que o manager ten conexión cos distintos nodos traballadores

En Docker swarm encontramonos cos seguintes comandos que son moi interesantes:
- **docker info**: Este comando mostra algunha información básica sobre o estado do cluster
- **docker node ls**: Este comando lista os actuales nodos no swarm e seu estado
# Unindo workers ao swarm
Os nodos worker son quenes reciben a carga de traballo do cluster de swarm. Para unilo a un manager debemos utilizar os siguientes comandos, tendo docker instalado nos workers tamén.

Primeiro debemos executar os seguintes comandos no manager para obter o token e o comando de join.
```bash
# Con este comando para generar o token para unir traballadores ao swarm
docker swarm join-token worker

# Con este comando para generar o token para unir managers ao swarm
docker swarm join-token manager
```

Unha vez que ejecutamos o anterior comando no manager, imos aos nodos traballadores e ejecutamos o siguiente comando
```bash
docker swarm join --token <token> <swarm manager private IP>:2377
```

No manager, podemos comprobar se se uniron correctamente os workers ao cluster swarm co seguinte comando
```bash
docker node ls
```
# Backup e restore do docker swarm
Traballando con un cluster de swarm é importante ser capaz de facer un backup e poder restaurar este. A continuación os pasos para poder realizar estos procesos. É interesante ter varios manager para garantizar **High Availability**, así mentres un crea a backup o outro sigue traballando e viceversa.
## Backup
Para crear unha backup no nodo manager do cluster swarm realizamos os seguintes comandos
```bash
# Primeiro paramos o servicio de docker
sudo systemctl stop docker
# Comprimimos todo o que haxa dentro da carpeta /var/lib/docker/swarm
sudo tar -zcvf backup.tar.gz -C /var/lib/docker/swarm .
# Volvemos a arrancar o servicio de docker
sudo systemctl start docker
```
## Restore
Cos seguites comandos, dentro do manager, podemos restaurar a backup que fixemos anteriormente
```bash
sudo systemctl stop docker
sudo rm -rf /var/lib/docker/swarm/*
sudo tar -zxvf backup.tar.gz -C /var/lib/docker/swarm/
sudo systemctl start docker
docker node ls
```
# Services
Os services son a maneira máis simple de utilizar un cluster de Docker Swarm. Un servicio é utilizado para ejecutar unha aplicación en un cluster de Docker Swarm. Especifica o número de replicas de tarefas que teñen que ejecutarse nos nodos traballadores. Estas tarefas son executadas nos nodos traballadores como [[Apuntes/Docker/01 - Introducción#Contenedor|contenedores]]. 
![Esquema|600x400](https://docs.docker.com/engine/swarm/images/services-diagram.webp)
## Componentes de un service
- **Tareas (tasks)**: Unha tarefa é unha instancia dun contenedor executándose. Cada tarefa é única e está asociada a un contenedor específico.
- **Réplicas**: Definen cantas instancias do contenedor se executarán simultáneamente no clúster.
- **Imagen**: O contenedor que se vai a executar.
## Comandos
Crear un servicio.
```bash
docker service create --name <nombre_service> --replicas <num_replicas> <nombre_imagen>
```

Modificar un servicio.
```bash
docker service update --replicas <num_replicas> <nombre_service>
```

Listar os servicios.
```bash
docker service ls
```

Mostrar detalles do servicio.
```bash
docker service ps <nombre_service>
```

Eliminar un servicio.
```bash
docker service rm <nombre_service>
```
# Stacks
Un stack é unha colección de servicios interconectados que poden ser desplegados e escalados como unha unidad. Os Docker stacks son similares a cando ejecutamos aplicacións multicontenedor con Docker Compose. Sin embargo, estos poden ser escalados e executados através do swarm como os servicios.
## Ejemplo de uso
Un stack definese utilizando un fichero `docker-compose.yml`. Similar ao utilizado por Docker Compose. Este fichero describe os servicios, redes e volumenes.

Empezamos creando un fichero `simple-stack.yml`.
```docker
services:
	web:
		image: nginx
	busybox:
		image: radial/busyboxplus:curl
		command: /bin/sh -c "while true; do echo Hello!; sleep 10; done"
```

Unha vez temos o fichero creado desplegamos o stack utilizando o seguinte comando.
```bash
docker stack deploy -C simple-stack.yml simple
```
## Comandos
Desplegar un stack.
```bash
docker stack deploy -c <nombre_fichero> <nombre_stack>
```

Listar os stacks.
```bash
docker stack ls
```

Listar as tareas de un stack.
```bash
docker stack ps <nombre_stack>
```

Listar os servicios asociados a un stack.
```bash
docker stack services <nombre_stack>
```

Eliminar un stack.
```bash
docker stack rm <nombre_stack>
```
