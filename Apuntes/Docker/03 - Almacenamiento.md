---
tags:
  - docker
  - contenedores
---
[[Apuntes/Docker/01 - Introducción#Qué é?|Docker]] ten dúas opcións para que os contenedores almacenen ficheros na máquina hosts. Así estos ficheros persisten incluso aunque o [[Apuntes/Docker/01 - Introducción#Contenedor|contenedor]] se pare. Estas opcións son volumenes e bind mounts.
# Volumenes
Un volumen en Docker é unha entidade externa ao contenedor, creada e xestionada por Docker, onde se poden almacenar datos de maneria persistente. Podemos crear un volumen utilizando o comando `docker voluem create`. 
## Características
As características principais dos volumenes son:
- **Persistencia de datos**: A razón principal de utilizar volumenes é permitir que os datos persistan máis aló do ciclo de vida do contenedor.
- **Independencia do contenedor**: Os volumenes están separados do sistema de ficheros do contenedor. Esto significa que varios contenedores poden acceder aos mesmos datos simultaneamente.
## Caso de uso
Deberíamos utilizar volumenes nos seguintes casos:
- Cando necesitemos que os datos persistan máis aló do ciclo de vida dun contenedor.
- Cando queiramos compartir datos entre varios contenedores.
## Comandos
Os comandos que podemos utilizar á hora de traballar con volumenes son os seguintes

Crear un volumen:
```bash
docker volume create <nombre_volumen>
```

Listar os volumenes existentes
```bash
docker volume ls
```

Inspeccionar un volumen específico
```bash
docker volume inspect <nombre_volumen>
```

Usar un volumen nun contenedor
```bash
docker run -d --name <contenedor> -v <nombre_volumen>:/datos <contenedor>
```

Eliminar un volumen:
```bash
docker volume rm <nombre_volumen>
```

Eliminar os volumenes non utilizados
```bash
docker volume prune
```

# Bind mounts
Os bind mounts en Docker son outra forma de almacenar datos de maneira persistente. Os bind mounts permiten montar unha ruta específica do sistema de ficheros do anfitrión directamente dentro do contenedor. Esto significa que o contenedor pode acceder e modificar arquivos directamente no sistema de ficheros do anfitrión.
## Características
As principais características dos bind mounts son:
- **Maior control sobre a localización dos datos**: Ao contrario que os volumenes, os bind mounts permítenche decidir exactamente onde se almacenan os datos no sistema host. Esto é últil cando xa tes datos nunha localización específica que queres usar dentro do contenedor.
- **Flexibilidade e risco de seguridade**: Os bind mounts son moi flexibles, pero tamén poden ser máis complexos e inseguros. O contenedor terá acceso ao sistema de ficheiros do host, o que pode introducir riscos se o contenedor está comprometido ou se os permisos non están configurados correctamente.
## Casos de uso
En general, deberíamos utilizar volumenes cando fose posible. Os bind mounts son apropiados nos seguintes casos:
- Compartir ficheros de confiruación entre a máquina host e os contenedores. 
- Cando o fichero ou o directorio do host esté garantizado que vai ser consistente e permanecer disponible para o contenedor.
## Comandos
Os bind mounts non proporcionan comandos específicos á hora de traballar con eles. Se queremos utilizar un bind mount cos nosos contenedores podemos facelo da seguinte maneira.
```bash
docker run -v <ruta_host>:<ruta_contenedor> <nombre_imagen>
```
# Almacenamiento en un cluster
Á hora de traballar cun [[06 - Docker Swarm#Que é?|cluster de swarm]], pode que necesitemos compartir un volumen de Docker entre os nodos de ese cluster. Algunhas de estas opción son:
- Usar lógica de aplicación para almacenar datos nun almacenamento externo.
- Utilizar un driver de volume que nos permita crear un volumen que sexa externo a calquera das máquinas do cluster.

Para este cometido vamos a utilizar un plugin de Docker que se chama `vieux/sshfs`. Podemos instalar este plugin da seguinte maneira en **todos** os nodos do swarm:
```bash
docker plugin install --grant-all-permissions vieux/sshfs
```

No manager do swarm, temos que crear un volumen de Docker que utilice o almacenamiento do servidor de almacenamiento. Para eso utilizamos o seguinte comando:
```bash
docker volume create --driver vieux/sshfs \
-o sshcmd=<usuario>@<ip_server_almacenamiento>:/home/usuario/externo \
-o password=<contraseña> \
sshvolume
```
Non olvidarnos de crear no servidor de almacenamiento a carpeta á que apuntamos en este comando.

Unha vez creado o volumen no manager xa podemos crear o [[06 - Docker Swarm#Services|servicio]] co seguinte comando:
```bash
docker service create \
--replicas=3 \
--name servicio_almacenamiento \
-- mount volume-driver=vieux/sshfs,source=cluster-volume,destination=/app,volume-opt=sshcmd=<usuario>@<ip_server_almacenamiento>:/home/usuario/external,volume-opt=password=<contraseña> <imagen> cat /app/mensaje.txt
```


