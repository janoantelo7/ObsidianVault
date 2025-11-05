---
tags:
  - contenedores
  - kubernetes
---
# Definición
Un **namespace** ou espacio de nombres é un mecanismo para dividir os recursos dentro de un clúster de Kubernetes en múltiples espacios lógicos. Utilizanse para separar e organizar os recursos de tal maneira que se poidan crear e gestionar en diferentes grupos, incluso se se encontran no mismo clúster.
# Comandos útiles
Crear espacio de nombres
```bash
kubectl create namesapce my-namespace
```

Obter a lista dos nombres
```bash
kubectl get namespace
```

Buscar os [[Apuntes/Kubernetes/01 - Introducción|pods]] en todos os namespaces
```bash
kubeclt get pods --all-namesapces
```

Buscar os [[Apuntes/Kubernetes/01 - Introducción|pods]] solo no espacio que nos interesa
```bash
kubectl get pods -n my-namespace
```
