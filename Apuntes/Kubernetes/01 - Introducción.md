---
tags:
  - contenedores
  - kubernetes
---
# Qué é?
Kubernetes é como un administrador intelixente que axuda a organizar e xestionar estas aplicacións en todas as computadoras.
# Componentes
- **Máquinas (Nodos):** Son as computadoras reais ou virtuais nas que se executarán as túas aplicacións. Podes ter varias destas máquinas no teu "grupo".
- **Kubernetes Master (Control Plane):** É como o cerebro de todo o sistema. Manexa as decisións e supervisa todo. Ten tres compoñentes principais:
	- **API Server:** Actúa como o punto de entrada para controlar Kubernetes. Díselle ao API Server o que desexas que faga.
	- **Scheduler:** Decide en que máquina debe executarse cada aplicación. Como un planificador que escolle o mellor computador para cada tarefa.
	- **Controller Manager:** Mantén o estado desexado do sistema. Se algo vai mal, o Controller Manager intentará corrixilo.
- **Etcd:** É como unha base de datos especial que almacena a configuración e o estado de todo o clúster de Kubernetes. Funciona como a memoria a longo prazo do sistema.
- **Kubelet:** É o "axudante" en cada máquina. Asegúrase de que os contedores estean executándose nas súas respectivas máquinas e comunícase co Mestre.
- **Kube Proxy:** Axuda aos contedores a comunicarse entre si e co mundo exterior. Xestiona a rede dentro do clúster.
- **Pods:** Son como envoltorios para os teus [[Apuntes/Docker/01 - Introducción#Contenedor|contenedores]]. Poden conter un ou máis contedores relacionados que traballan xuntos e comparten cousas como a rede.

En resumen, Kubernetes é como un sistema de xestión que organiza as túas aplicacións (contedores) nun grupo de computadoras (nodos). O Mestre toma decisións e mantén todo en orde, mentres que os Kubelets nas máquinas individuais aseguran que as aplicacións se executen correctamente. Os Pods son como caixas que conteñen as túas aplicacións e axudan a mantelas organizadas.