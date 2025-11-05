---
source: https://www.digitalocean.com/community/tutorials/how-to-use-vault-to-protect-sensitive-ansible-data
---

Cando queremos traballar en [[Apuntes/Ansible/01 - Introducción#Qué é?|Ansible]] con varios hosts nos que temos distintos usuarios con distintas contraseñas podemos facelo da seguinte maneria:

Na carpeta do proyecto, onde temos o playbook creado, creamos unha carpeta chamada "*host_vars*"
```bash
mkdir host_vars
```
