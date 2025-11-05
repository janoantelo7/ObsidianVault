---
tags:
  - contenedores
  - docker
---
# Qué é?
Docker é unha plataforma que permite crear, enviar e executar aplicacións dentro de contedores. Estes contedores empaquetan todo o necesario para que a aplicación funcione de forma consistente en calquera entorno, facilitando a implementación e xestión de software.
# Conceptos básicos
## Contenedor
Un contenedor é unha instancia aislada e lixeira que agrupa unha aplicación xunto con todas as súas dependencias e configuracións necesarias para que funcione en calquer entorno. Os contenedores executanse sobre o sistema operativo host pero están aisalados uns de outros.
## Imágen
Unha imágen é unha plantilla inmutable que se utiliza para crear contenedores. Contén todos os componentes necesarios para executar a aplicación. Podemos consultar o seguinte [[02 - Docker Imágenes#Qué é?|documento]] para ter máis información acerca delas e de como traballar con elas.
## Volumen
Un volumen en Docker utilizase para almacenar datos persistentes aos contenedores. Esto permite que os datos se conserven incluso de o contenedor se elimina ou se reinicia. Podemos consultar o seguinte [[03 - Almacenamiento#Volumenes|documento]] para tar máis información acerca dos volumenes e o almacenamiento de Docker.
## Docker Compose
Docker compose é unha ferramenta que nos permite definir e executar aplicacións multicontenedor. A través de un fichero `docker-compose.yml`, podese describir cómo se deben configurar os contenedores e súas relacions entre sí. Podemos obter máis información no seguinte [[04 - Docker Compose#Qué é?|enlace]].
## Dockerfile
Os Dockerfiles son arquivos de texto que conteñen as instrucións para automatizar a creación dunha imaxe Docker. Podemos acceder ao seguinte [[02 - Docker Imágenes#Dockerfiles|documento]] para obter máis información.
# Instalación en Ubuntu
No siguiente bloque de código están os comandos necesarios para instalar docker en Ubuntu. Se queremos instalar docker en outros sistemas podemos seguir a guía oficial en este [enlace](https://docs.docker.com/engine/install/) .
```bash
# Añadimos a clave GPG de Docker
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Añadimos o repositorio
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Instalamos os paquetes necesarios de docker.
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
## Ejecutar comandos docker sin sudo
Por defecto, os comandos de Docker sólo poden ser ejecutados polo usuario `root` ou por un usuario do grupo `docker`. Para que o noso usuario poida ejecutar comados Docker sin utilizar `sudo` debemos añadirnos ao grupo `docker`.
```bash
sudo usermod -aG docker <username>
```
# Actualizar Docker
Cando traballamos con docker é importante manter docker actualizado, así que vamos a ver como volver a unha versión anterior e como actualizar docker.
## Volver a unha versión anterior
```bash
sudo systemctl stop docker
sudo apt-get remove -y docker-ce docker-ce-cli
sudo apt-get update
sudo apt-get install -y docker-ce=5:18.09.4~3-0~ubuntu-bionic docker-ce-cli=5:18.09.4~3-0~ubuntu-bionic

```
## Actualizar a unha nova versión
Para actualizar a unha nova versión solamente temos que instalar os novos paquetes.
```bash
sudo apt-get install -y docker-ce docker-ce-cli
```
