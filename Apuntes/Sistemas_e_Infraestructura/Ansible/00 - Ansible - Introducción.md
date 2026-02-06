---
tags:
  - automatización
  - ansible
---
# Qué é?
Ansible é unha ferramenta que permite a administración remota de sistemas mediante código. Con ansible podemos crear recetas ([[02 - Básico de playbooks#Qué é?|playbooks]]) para a configuración da infraestructura, aprovisionamento de recursos e despliegue de aplicacións.
# Instalación
Para instalar ansible en Arch Linux utilizamos o siguiente comando (varia segundo a distribución):
```bash
yay -S ansible
```

Podemos encontrar máis exemplos de instalación no seguinte link: [Installing Ansible on specific operating systems — Ansible Community Documentation](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html). Se de maneira automática non nos crea a carpeta /etc/ansible creamola nos co seguinte comando:
```bash
# con este comando creamos a carpeta
sudo mkdir -p /etc/ansible

# convertimonos en root para generar un fichero de configuración comentado
sudo su -
cd /etc/ansible
ansible-config init --disabled > ansible.cfg
exit

# ahora generamos o fichero de hosts
sudo touch /etc/ansible/hosts
```
## Comprobar instalación
Para verificar que Ansible se instalou correctametne podemos ejecutar.
```bash
ansible --version
```

Podemos comprobar se todo funciona correctamente engadindo o host no fichero e facendolle ping co modulo de ansible
```bash
# primeiro copiamos a nosa clave ssh cara o host
ssh-copy-id jano@192.168.56.112
```

Ahora temos que engadir este hosts no fichero de hosts (/etc/ansible/hosts):
```conf
[test]
192.168.56.112
```

Unha vez feitos estos pasos previos podemos intentar facerlle ping co modulo de ansible
```bash
ansible all -m ping
```
# Enlace
[Curso de iniciación a Ansible para la automatización de operaciones (ualmtorres.github.io)](https://ualmtorres.github.io/CursoAnsible/tutorial/)

