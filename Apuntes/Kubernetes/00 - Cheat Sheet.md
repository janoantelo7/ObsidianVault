---
tags:
  - contenedores
  - kubernetes
---
# Deployments
## Desplegar en un namespace
para crear un [[03 - Deployments|deployment]] en un [[04 - Espacio de nombres|namespace]] concreto.
```bash
kubectl apply -f [DEPLOYMENT.yaml] -n [NAMESPACE]
```

# Listar volumenes
Listar os volumenes que temos creados.
```bash
kubectl get pv

# tamén podemos sacar esa misma información en formato yaml
kubectl get pv -o yaml
```

Podemos sacar a lista de volumenes ordenada por capacidad.
```bash
kubectl get pv --sort-by=.spec.capacity.storage
```

# Executar comandos nos pods
Podemos utilizar `kubectl exec` para executar comandos dentro dos [[Apuntes/Kubernetes/01 - Introducción#Componentes|pods]].
```bash
kubectl exec quark -n beebox-mobile -- cat /etc/key/key.txt
```

Neste comando '**quark**' é o nombre do pod e '**beebox-mobile**' é o espacio de nombres onde están os pods, e `cat /etc/key/key.txt` o comando a exectutar.

# Listar os pods con maior información
Podemos listar os pods que temos no clúster recibindo máis información co seguinte comando.
```bash
kubectl get pods -o wide
```


