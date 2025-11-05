---
tags:
  - contenedores
  - kubernetes
---
# Definición
Un deployment é un recurso de [[Apuntes/Kubernetes/01 - Introducción#Qué é?|Kubernetes]] que nos permite definir o estado deseado da aplicación, e deixar que Kubernetes se encargue de levala ao estado automáticamente. Un deployment asegurase de que o número desexado de réplicas dunha aplicación esté en funcionamento.

Os **usos típicos** dos deployments son:
- Escalar fácilmente unha aplicación para arriba ou para abaixo cambiando o número de réplicas
- Crear actualizacións da nova versión do software
- Realizar rollbacks a versións previas
# Ejemplo
Creamos un fichero chamado `nginx-deployment.yaml` que será o deployment desplegará un nginx.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

Para lanzar o deployment no noso clúster utilizamos o seguinte comando.
```bash
kubectl apply -f nginx-deployment.yaml
```

Para escalar o deployment podemos utilizar o seguinte comando.
```bash
kubectl scale deployment/nginx-deployment --replicas=10
```

Para realizar un rollback a unha versión previa do deployment podemos utilizar
```bash
kubectl rollout undo deployment/nginx-deployment
```

Tamén podemos especificar a que versión queremos retroceder engadindo o seguinte `--to-revision`.
```bash
kubectl rollout undo deployment/nginx-deployment --to-revision=2
```

Podemos ver todas as versións ás que podemos facer rollout co seguinte comando.
```bash
kubectl rollout history deployment/nginx-deployment
```
