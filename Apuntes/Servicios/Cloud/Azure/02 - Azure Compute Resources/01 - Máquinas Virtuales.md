---
tags:
  - azure
---
# Máquinas virtuales en Azure (IaaS)
As máquinas virtuales en Azure son un servicio de **infraestructura como servicio** (IaaS) que permite crear e executar servidores virtuales na nube.

Unha VM de Azure é realmente similar a unha VM que poderíamos ter on-premise, salvo que nos non temos que gestionar o hipervisor. En ela podemos elexir, o sistema operativo, os recursos de hardware, o almacenamiento e a rede. Cando nos decidimos a contratar unha VM en Azure ofrecennos dous tipos de modelos de pago:
- **Pay-as-you-go:** que implica que só pagamos polos recursos que consumimos.
- **Instancia reservada:** que implica que nos vamos a comprometer a utilizar a VM por un período de tempo determinado, e de esta forma ofrecennos descontos significativos.

A maiores, este tipo de recursos permiten a **escalabilidade vertical** aumentando o seu tamaño ou ben a **escalabilidade horizontal** engadindo máis VM.

Cando creamos unha máquina virtual necesitamos os seguintes componentes:
- **Máquina virtual:** o recurso que representa o servidor.
- **Disco do sistema operativo:** onde vai ser instalado o SO.
- **Disco de datos:** almacenamento adicional para os datos.
- **Interfaz de rede (NIC):** para permitir que a VM se conecte con outras redes.
- **Dirección IP pública:** esto fai que poidamos acceder á nosa VM dende internet. (Opcional)
- **Rede Virtual (Vnet):** rede privada á que se conecta a VM.
## Discos virtuales
Os discos virtuales (VHD) son un fichero que é unha representación de un disco duro. Estos VHD son construidos sobre páginas blobs de Azure Storage, facilitándonos así a gestión dos discos ao abstraer as cuentas de almacenamento subyacentes.

Unha máquina virtual pode ter tres tipos de discos:
- **Disco do sistema operativo (OS Disk):** Almacena o sistema operativo da VM. Non é recomendable utilizalo para aplicacións ou datos.
- **Disco de datos:** É o utilizado para almacenar datos de aplicacions ou outro tipo de datos. Adxuntanse á VM como unidades SCSI e asignaselles unha letra ou punto de montaxe. 
- **Disco temporal:** Este disco ven por defecto na máquina virtual e é o encargado de almacenar datos temporales como os da swap.
### Encriptación
Á hora de encriptar os discos de unha VM en Azure podemos facelo de dúas maneiras:
- **Storage Service Encryption (SEE):** Esta é unha encriptación a nivel físico do disco no datacenter. Aquí nos non podemos gestionar nada. Está activado por defecto.
- **Azure Disk Encryption (ADE):**  Encriptado opcional para os VHDs da máquina virtual. Esto asegurase de que o disco só sexa accesible desde a VM intencionada. Emprega a encriptación do sistema como pode ser Bitlocker e dm-crypt.
## Alta disponibilidade de unha VM
Á hora de configurar a disponibilidade dunha máquina virtual temos que ter claros os seguintes conceptos:

* **Concepto de disponibilidade:** É a calidade do servizo. É a medida ou obxectivo de que o sistema ou VM estea operativo e en funcionamento cando se necesita. Os mecanismos de redundancia arquitectónica (como as Zonas de Dispoñibilidade) son os que garanten un **SLA (Acordo de Nivel de Servizo)** máis alto.
* **Concepto de geografía:** Esto é a región geográfica que todos conocemos. (ej: US ou EU).
* **Concepto de regións:** Esto é unha área que agrupa varias cidades. (ej: East US, North EU).
* **Concepto de availability zone:** Son centros de datos físicamente separados dentro de unha mesma región de Azure.
* **Concepto de availability sets:** Esto consiste en replicar máquinas virtuales dentro de un mesmo centro de datos. Dentro dos availability sets temos dous tipos:
	* **Fault Domain:** Agrupar os recursos dentro de un mesmo hardware. Se un componente de un FD falla, só as máquinas virtuales de ese FD se verán afectadas.
	* **Update Domain:** Agrupación lóxica de VMs que poden reiniciarse ao mesmo tempo durante o mantemento planificado de Azure. Cando Azure necesita realizar unha actualización, só un UD reiniciase á vez, o que permite que os outros UDs sigan funcionando e garante que a aplicación permaneza dispoñible.
* **Concepto de Escalabilidade:** a **escalabilidade** é a capacidade de un sistema para manexar o aumento predecible a largo plazo da carga do traballo sen que o seu rendemento se degrade. A menudo esto é unha acción manual ou planificada. Podemos lograla de dúas maneiras:
	* **Escalado vertical (_Scale Up/Down_):** Consiste en aumentar ou disminuir os recursos da VM.
	* **Escalado horizontal:** Implica añadir ou eliminar máis máquinas virtuales a un grupo de recursos para distribuir a carga.
* **Concepto de elasticidade (_Scale Out/In_):** É a capacidade de un sistema para adaptarse automáticamente aos cambios repentinos e impredecibles da carga do traballo. Aumentando ou disminuindo os recursos en tempo real. A elasticidade é unha forma de escalabilidade pero cun enfoque na **automatización** e na **capacidade de resposta instantánea**.
### Diferencia entre Avaliability Zone e Availability Sets
As **Availability Zones** protexen os servicios a nivel de **centro de datos** completo (protección contra fállaa dun edificio enteiro), mentres que os **Availability Sets** protexen de fallos a **nivel de hardware** ou rack dentro dun só centro de datos.  En rexións de Azure que teñen Availability Zones, recoméndase usar estas últimas, xa que ofrecen un nivel de protección superior e máis amplo.
