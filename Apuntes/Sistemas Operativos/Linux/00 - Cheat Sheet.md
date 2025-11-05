---
tags:
  - utilidades/linux
---
# Usuarios
## Desbloquear usuario
Se o usuario foi bloqueado mediante sistemas como `faillock`, podemos desbloquealo utilizando o seguinte comando:
```bash
sudo faillock --user <nombre_de_usuario> --reset
```

> [!NOTE] Nota
> Podemos saber máis da gestión de usuarios no seguinte [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Gestión de usuarios|enlace]].
# Sistema de ficheros
## Espacio ocupado por carpetas
Podemos filtrar o que ocupan todas as carpetas de unha ruta co seguinte comando:
```bash
sudo du -hd 1 /home
```
En este caso facemolo de `/home` pero podríamos facelo con calquer outra ruta do sistema.

A maiores podemos ver que carpetas ocupan máis de _x_ cantidade de espacio:
```bash
sudo du -h --threshold=50M /home/* | sort -hr
```
## Creacion Link Simbolicos
```bash
sudo ln -s {rutaOrixe} {rutaDestino}
```
## Búsqueda ficheros
Buscar todos os ficheros en unha ruta e sumar o tamaño máximo de eles
```bash
sudo find /var/log/httpd/ -maxdepth 1 -type f -name "vhost_*" -printf "%s\n" | awk '{total_size+=$1} END {print total_size}' | numfmt --to=iec-bytes
```

Buscar ficheros con regex
```bash
sudo find /var/log/httpd/ -type f -regex ".*\.log$\|.*\.log\.20250523$\|.*2025-04-02\.log$"
```

> [!NOTE] Nota
> Podemos saber máis do sistema de ficheros de linux no seguinte [[02 - Sistema de ficheros|enlace]].
# Redes
## Saber ip publica
Para saber a ip pública de un servidor/máquina por terminal podemos executar o seguinte comando.
```bash
curl ifconfig.me
```
## Ver  todos os puertos nos que escoita a máquina
Podemos ver todos os puertos `tcp` e `udp` nos que está escoitando a máquina, así como o numero de proceso para saber que aplicación escoita nese puerto.
```bash
ss -tulpn
```
# Cifrado de discos
## Comprobar contraseña de luks
Cando temos un disco podemos comprobar a súa contraseña de encriptado de luks co seguinte comando.
```bash
sudo cryptsetup --verbose open --test-passphrase /dev/{particion_encriptada}
```
# AWS CLI
## Subir ficheros a s3 mediante aws cli
Con este comando podemos subir un fichero especifico a aws. Se no include usamos `*.extension` podemos subir varios ficheros con unha determinada extension, en este caso debería ir entrecomillado.
```bash
aws s3 cp . s3://aws-s3-bucket-uri --recursive --exclude "*" --include random.txt --profile profile-name
```

Ejemplo subindo varios ficheros cunha extensión
```bash
aws s3 cp . s3://aws-s3-bucket-uri --recursive --exclude "*" --include "*.zip" --dryrun
```

Podemos eliminar o `--dryrun` se queremos **subilos** de **verdade** ao bucket.

> [!warning] Atención
> O orden das flags `exclude` e `include` influye no resultado da operación. Se primeiro poñemos o flag `exclude`, excluense todos os ficheros excepto o que poñemos no `include`. Se polo contrario, primeiro poñemos `include` non se enviará ningún fichero xa que ao ir despois o `exclude` tamén se exclue o que incluimos explicitamente.
# Varios
## CheatSheets
Podemos obter unha cheatsheet de casi calquer comando na terminal co seguinte comando:
```bash
curl cheat.sh/[COMANDO]
```

Tamén é unha web que podemos consultar no navegador.
## Comprobar certificados
Podemos comprobar se un certificado está ben formado co seguinte comando:
```shell
openssl x509 -in certificado.crt -text -noout
```

Tamén podemos comprobar se unha key coincide co certificado cos seguintes comandos:
```shell
openssl x509 -in certificado.crt -noout -modulus | openssl md5
# esto devolve un hash
openssl rsa -in key_certificado.key -noout -modulus | openssl md5
# esto devolve outro hash
```

Se esos dous hash que devolven esos comandos coinciden a clave é a de ese certificado.
# WSL
Podemos instalar a distribución de WSL que queiramos en Windows ejecutando o seguinte comando:
```powershell
wsl.exe --install --distribution [NOMBRE_DISTRO]
```

Se queremos que a distribución se instale en outro disco podemos facelo co seguinte comando: 
```powershell
wsl --install --distribution Ubuntu --location d:/wsl/ubuntu/
```
## Montar Google Drive en unha distro
Podemos montar a carpeta de Google Drive dentro de WSL co seguinte comando: 
```bash
sudo mount -t drvfs H: /mnt/h
```
