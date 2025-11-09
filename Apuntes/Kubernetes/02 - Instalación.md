---
tags:
  - contenedores
  - kubernetes
---
En esta guía recollense os comandos necesarios para poder realizar a instalación de un clúster de  [[Apuntes/Kubernetes/01 - Introducción#Qué é?|Kubernetes]] en Ubuntu.
# Instalación dos paquetes necesarios
Creación do archivo de configuración para containerd.
```bash
cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
```

Carga dos módulos.
```bash
sudo modprobe overlay
sudo modprobe br_netfilter
```

Establecer as configuracións para a networking de kubernetes.
```bash
cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF
```

Aplicar os novos axustes.
```bash
sudo sysctl --system
```

Instalar containerd.
```bash
sudo apt-get update && sudo apt-get install -y containerd.io
```

Crear o archivo de configuración por defecto de containerd.
```bash
sudo mkdir -p /etc/containerd
```

Generar a configuración por defecto e gardala no novo archivo por defecto.
```bash
sudo containerd config default | sudo tee /etc/containerd/config.toml
```

Reiniciar containerd para asegurarnos que utilizamos a nova configuración.
```bash
sudo systemctl restart containerd
sudo systemctl enable containerd
```

Verificar que containerd está executandose.
```bash
sudo systemctl status containerd
```

Deshabilitar a swap.
```bash
sudo swapoff -a
```

Instalar os paquetes de dependencias.
```bash
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
```

Descargar e añadir a clave GPG.
```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

Añadir kubernetes ao repositorio.
```bash
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

Actualizar a lista de paquetes.
```bash
sudo apt update
```

Instalar os paquetes de kubernetes.
```bash
sudo apt-get install -y kubelet kubeadm kubectl
```

# Inicializar o cluster no nodo controlador
Inicializamos o cluster de kubernetes no **[[Apuntes/Kubernetes/01 - Introducción#Componentes|nodo controlador]]**.
```bash
sudo kubeadm init --pod-network-cidr 192.168.0.0/16
```

Establecemos o acceso a kubectl.
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Probamos o acceso ao cluster.
```bash
kubectl get nodes
```

Instalamos calico network.
```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml
```

Comprobamos o estado do nodo controlador.
```bash
kubectl get nodes
```

# Unindo nodos ao cluster
No nodo controlador creamos o token e copiamos o comando de kubeadm join. Este comando vainos mostrar o comando "kubeadm join" que é o que debemos utilizar nos [[Apuntes/Kubernetes/01 - Introducción#Componentes|nodos]].
```bash
kubeadm token create --print-join-command
```

Executamos a saída do comando anterior nos **nodos traballadores** como sudo.
```bash
sudo kubeadm join…
```

No **nodo controlador** comprobamos o estado do cluster.
```bash
kubectl get nodes
```

# Actualizar a versión do cluster
En este ejemplo vamos a ver como se pode actualizar a versión de kubernetes que está a utilziar o noso cluster.
## Actualizar o controlador
Actualizamos kubeadm á version **1.27.2**, por exemplo.
```bash
sudo apt-get update && \ sudo apt-get install -y --allow-change-held-packages kubeadm=1.27.2-00
```

Drenamos o **nodo controlador** (significa que deixe de aceptar carga de traballo).
```bash
kubectl drain k8s-control --ignore-daemonsets
```

Planificamos a actualización.
```bash
sudo kubeadm upgrade plan v1.27.2
```

Aplicamos a actualización.
```bash
sudo kubeadm upgrade apply v1.27.2
```

Actualizamos kubelet e kubectl á versión 1.27.2
```bash
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubelet=1.27.2-00 kubectl=1.27.2-00
```

Reiniciamos kubelet.
```bash
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

Revertimos o estado de drenado do **nodo controlador**.
```bash
kubectl uncordon k8s-control
```

Verificamos que o **nodo controlador** está funcionando en estado ready.
```bash
kubectl get nodes
```
## Actualizar os traballadores
No **nodo controlador** drenamos o nodo traballador.
```bash
kubectl drain k8s-worker1 --ignore-daemonsets --force
```

Actualizamos kubeadm no **nodo traballador**.
```bash
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubeadm=1.27.2-00
```

Reiniciamos kubelet.
```bash
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

Revertimos o estado de drenado desde o **nodo controlador**.
```bash
kubectl uncordon k8s-worker1
```

