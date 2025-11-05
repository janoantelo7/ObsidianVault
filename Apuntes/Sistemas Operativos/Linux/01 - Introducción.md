---
tags:
  - linux
---
# Gestión de usuarios
## Crear usuario
Para crear un usuario en linux utilizamos o siguiente comando.
```bash
useradd -g {grupo_primario} -G {grupo/s_secundario/s} -s /bin/bash -m {nombre_usuario}
```
## Borrar usuario
Se necesitamos borrar un usuario do sistema utilizamos o seguinte comando:
```bash
userdel -r {nombre_usuario}
```
## Desbloquear usuario
Se o usuario foi bloqueado mediante sistemas como `faillock`, podemos desbloquealo utilizando o seguinte comando:
```bash
sudo faillock --user <nombre_de_usuario> --reset
```
# Gestión de paquetes
## Actualizar paquetes
Para actualizar os paquetes dependendo da distro podemos utilizar os siguientes comandos
**Debian/Ubuntu**
```bash
sudo apt update
sudo apt upgrade
```

**RHEL**
```bash
sudo dnf update
```

**Arch**
```bash
# se utilizamos o gestor por defecto
sudo pacman -Syu

# se utilizamos yay
yay -Syu
```
## Instalar paquetes
Para instalar paquetes depenendo da distro podemos utilizar os siguientes comandos

**Debian/Ubuntu**
```bash
sudo apt install <package_name>
```

**RHEL**
```bash
sudo dnf install <package_name>
```

**Arch**
```bash
# se utilizamos o gestor por defecto
sudo pacman -S <package_name>

# se utilizamos yay
yay -S <package_name>
```
## Listar paquetes instalados
**Debian/Ubuntu**
```bash
sudo apt list --installed
```

**RHEL**
```bash
sudo dnf list installed
```

## Ver cambios de un paquete
Utilizamos este comando en distribucións de RHEL para ver se un paquete soluciona unha vulnerabilidad
```bash
rpm -q --changelog <package> | grep <CVE>
```
# Atallos teclado terminal
| Comando | Descripción                                                                       |
| ------- | --------------------------------------------------------------------------------- |
| ctrl+a  | Mover o cursor ao inicio da linea.                                                |
| ctrl+e  | Mover o cursor ao final da línea.                                                 |
| ctrl+r  | Buscar comandos utilizados anteriormente.                                         |
| ctrl+-> | Mover o cursor unha palabra hacia a dereita.                                      |
| ctrl+<- | Mover o cursor unha palabra hacia a esquerda.                                     |
| ctrl+u  | Cortar a línea desde o cursor ata o inicio da misma e enviar eso ao portapapeles. |
| ctrl+f  | Mover o cursor un carácter hacia a dereita.                                       |
| ctrl+b  | Mover o cursor un carácter hacia a esquerda.                                      |
| ctrl+l  | Limpiar a pantalla.                                                               |
