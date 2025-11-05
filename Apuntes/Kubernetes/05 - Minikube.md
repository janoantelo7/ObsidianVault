---
tags:
  - kubernetes
---
Minikube é unha maneira de aprender [[Apuntes/Kubernetes/01 - Introducción|kubernetes]] de forma local. Está centrado para ser unha maneira sencilla de aprender kubernetes. 

Os requisitios para minikube son os seguintes:
- 2 CPU's
- 2 GB de RAM
- 20 GB de disco
- Conexión a internet
- [[Apuntes/Docker/01 - Introducción|Docker]]
# Instalación
Unha vez temos Docker instalado executamos os seguintes comandos:
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb
```

Unha vez feitos esos comandos podemos ver que xa temos minikube instalado:
```bash
jano@vbox ~ % minikube version
minikube version: v1.35.0
commit: dd5d320e41b5451cdf3c01891bc4e13d189586ed-dirty
```
## Instalando kubectl
Unha vez feitos os pasos anteriores podemos administrar minikube co seu comando especifico pero, no noso caso vamos a instalar `kubectl`. Xa que é a ferramenta que se utiliza para administrar kubernetes.
```bash
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
```

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
```

```bash
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly
```

```bash
sudo apt-get update

# e finalmente instalamos kubectl
sudo apt-get install -y kubectl
```

# Arrancando minikube
Unha vez feitos todos os pasos anteriores, podemos proceder a arrancar o servicio de minikube.
```bash
minikube start --driver=docker
```
