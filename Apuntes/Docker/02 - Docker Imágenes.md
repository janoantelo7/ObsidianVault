---
tags:
  - contenedores
  - docker
---
# Qué é?
Unha imagen [[Apuntes/Docker/01 - Introducción#Qué é?|Docker]] é un fichero que contén o código e os componentes necesarios para executar o software dentro do [[Apuntes/Docker/01 - Introducción#Contenedor|contenedor]].

Os contenedores e imágenes utilizan un sistema de ficheros en capas. Cada capa contén só a diferencia da anterior capa. A imagen consiste en unha ou máis read-only capas mentres que o contenedor engade a capa de escritura. Esto permite que os contenedores e as imagenes compartan capas obtendo o seguinte resultado: menor uso de disco, maior velocidade de transferencia de imagenes e maior velocidade á hora de construilas.
# Administración de imágenes
**Descargar novas imágenes**
Podemos baixarnos novas imágenes cara o noso sistema co comando de `docker image pull <imagen>`.  Se xa temos a imágen no noso sistema non a baixa.
```bash
docker image pull debian
```

**Listas as imágenes do sistema**
Para listar as imágenes que temos no noso sistema podemos facelo co seguinte comandos.
```bash
docker image ls

# tamén se pode utilizar a seguinte maneira abreviada
docker images
```

**Borrar imágenes do sistema**
Borramos imágenes do sistema co seguinte comando. Podemos utilizar tanto o id da imágen como o seu nombre.
```bash
docker image rm <imagen>
```

Tamén podemos utilizar `docker image prune` para eliminar todas as imágenes de Docker que están sin utilizar.
# Construcción de imágenes
## Dockerfiles
Os Dockerfiles son arquivos de texto que conteñen as instrucións para automatizar a creación dunha imaxe Docker. Estes permiten definir e documentar os pasos necesarios para crear o entorno dun contedor, incluíndo a base do sistema operativo, a instalación de programas e librerías, a configuración de variables de entorno, a exposición de portos, entre outros. Unha vez definido o Dockerfile, pódese usar o comando docker build para crear a imaxe.
### Directivas
As instruccións que van dentro de un Dockerfile chamanse directivas. Aquí podemos ver unha lista das directivas e para que sirven

| Directiva     | Explicación                                                                                                                                                         |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `From`        | Indica a imagen base do contenedor. Normalmente é a primeira directiva que se introduce no Dockerfile (coa excepción de ARG que pode ser posicionada antes de from) |
| `ENV`         | Marca as variables de entorno. Estas poden ser referenciadas no Dockerfile e son visibles á hora de ejecutar o contenedor                                           |
| `RUN`         | Crea una nova capa encima da anterior ejecutando un comando dentro da nova capa.                                                                                    |
| `CMD`         | Especifica o comando por defecto utilizado á hora de ejecutar o contenedor                                                                                          |
| `EXPOSE`      | Utilizase para documentar que puerto(s) son pensados que utilice o contenedor. Non ten ningún impacto no contenedor.                                                |
| `WORKDIR`     | Establece o directorio de traballo para as seguintes directivas: ADD, COPY, CMD, ENTRYPOINT.                                                                        |
| `COPY`        | Copia ficheros desde a máquina local á imagen                                                                                                                       |
| `ADD`         | Moi similar a COPY pero podese descargar ficheros de unha URL e extraer un fichero dentro da imagen                                                                 |
| `STOPSIGNAL`  | Especifica a señal que será utilizada para parar o contenedor                                                                                                       |
| `HEALTHCHECK` | Especifica o comando que se ejecutará para verificar que o contenedor está funcionando correctamente                                                                |
#### Ejemplos
##### Ejemplo 1 - Ngnix básico
Definimos o siguiente en un Dockerfile
```docker
FROM ubuntu:bionic

ENV NGINX_VERSION 1.14.0-0ubuntu1.11

RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx=$NGINX_VERSION

CMD ["nginx", "-g", "daemon off;"]
```

Para construir a imagen utilizamos os siguientes comandos
```bash
# -t no comando de abaixo significa o nombre que lle vamos dar
# a imagen que estamos construindo
docker build -t custom-nginx . 

# Ejecutamos un contenedor novo chamado "custom-nginx" que expon o puerto 8080
docker run --name custom-nginx -d -p 8080:80 custom-nginx

# Comprobamos que funciona
curl localhost:8080
```
##### Ejemplo 2 - Añadir ficheros
No siguiente ejemplo, modificamos o ejemplo anterior para añdir un fichero index.html
```docker
FROM ubuntu:bionic
ENV NGINX_VERSION 1.14.0-0ubuntu1.7
RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y nginx=$NGINX_VERSION
WORKDIR /var/www/html/
ADD index.html ./
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
STOPSIGNAL SIGTERM
HEALTHCHECK CMD curl localhost:80
```

Para construir a imagen utilizamos os siguientes comandos.
```bash
# -t no comando de abaixo significa o nombre que lle vamos dar
# a imagen que estamos construindo
docker build -t custom-nginx . 

# Ejecutamos un contenedor novo chamado "custom-nginx" que expon o puerto 8080
docker run --name custom-nginx -d -p 8080:80 custom-nginx

# Comprobamos que funciona e nos devolve o noso "hello world!"
curl localhost:8080
```
### Creación de Imágenes Eficientes con Multi-Stage Builds
Á hora de construir imágenes de Docker é importante asegurarnos de que os Dockerfiles producen imágenes pequenas e eficientes que non teñen datos innecesarios. Para eso podemos utilizar unha forma de construir imágenes chamada multi-stage builds para disminuir este tamaño en algunhas situacións.

Por exemplo, imágina que vamos a construir un contenedor que é unha aplicación "hello world" en Go.
```Docker
FROM golang:1.12.4
WORKDIR /helloworld
COPY helloworld.go .
RUN GOOS=linux go build -a -installsuffix cgo -o helloworld .
CMD ["./helloworld"]
```

Este Dockerfile daría como salida unha imágen que opcupa moito espacio no sistema xa que estamos a descargar unha imágen completa de Go para compliar o código e ejecutar o código. Sen embargo, podemos dividir o dockerfile en dous estados, un que se encargue de compilar e outro de ejecutar. No seguinte exemplo vemos como aplicar esta técnica.
```docker
FROM golang:1.12.4 AS compiler
WORKDIR /helloworld
COPY helloworld.go .
RUN GOOS=linux go build -a -installsuffix cgo -o helloworld .

FROM alpine:3.9.3
WORKDIR /root
COPY --from=compiler /helloworld/helloworld .
CMD ["./helloworld"]
```

Esto o que fai é que se utilice a primeira imágen á hora de compilar o fichero, pero a nosa imágen resultante será o alpine e o fichero executable de GO, producindo así unha imáxen moito máis pequena.
