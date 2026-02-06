---
tags:
  - docker
  - contenedores
---
Docker por defecto, danos distintos tipos de drivers de rede. Os cales son: Host, Bridge e Overlay.
# Host
O Driver de rede **host** permitenos utilizar a rede do host directamente, esto ten as seguintes características:
- Os contenedores utilizan os recursos de rede do host directamente.
- Non hai sandboxes, todos os contenedores no host comparten o mismo espacio de nombres na rede.
- Non pode haber dous contenedores utilizando o mismo puerto.
- **Casos de uso**: Instalación simple e para solo un contenedor ou uns poucos na máquina host.
# Bridge
O driver de rede **bridge** utiliza as redes bridge de Linux para darlle conectividade aos contenedores do mismo host. Ten as seguintes características:
- Este é o driver **por defecto** para os contenedores en un **mismo host**.
- Crea un Linux Bridge por cada rede de Docker.
- Crea un Linux Bridge por defecto chamado "_bridge0'_". Os contenedores son automáticamente conectados a este se non se especifíca outra rede.
- **Casos de uso**: Aislamiento de rede entre os contenedores de un mismo host.
# Overlay
O driver de rede **overlay** proporciona conectividade entre contenedores através de distintos hosts de Docker. Por exemplo, en un [[06 - Docker Swarm#Que é?|Docker Swarm]]. As súas características son:
- Usa un plano de VXLAN data, que permite enviar datos entre hosts.
- Automáticamente configura as interfaces de rede, bridges, etc. en cada host según se necesite.
- **Casos de uso**: Permitir o networking através de contenedores en un swarm.
