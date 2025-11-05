---
tags:
  - linux
---
# Explicación do sistema de ficheros
En Linux, entender o sistema de ficheros é crucial para a navegación e a administración de ficheros. O FHS (Filesystem Hierarchy Standard), é unha estructura definida que ayuda a prever que os ficheros se perdan polo sistema. Os principales directiorios que nos encontramos en Linux son os seguintes:
- `/`: Directorio Raíz, é o directorio de maior nivel no sistema de ficheros. Todos colgan de este.
- `/home`: Carpetas `home` dos usuarios.
- `/bin`: Binarios executables esenciales do sistema.
- `/sbin`: Binarios de administración do sistema.
- `/etc`: Ficheros de configuración.
- `/opt`: Aplicacións adicionales ás estándar.
- `/var`: Datos variables (logs, spool files...).
- `/usr`: Programas do usuario e datos.
- `/lib`: Librerías compartidas.
- `/tmp`: Ficheros temporales

Podemos obter máis información do sistema de ficheros nos siguientes enlaces:
- [3.2. Overview of File System Hierarchy Standard (FHS) | Red Hat Product Documentation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/4/html/reference_guide/s1-filesystem-fhs#s2-filesystem-fsstnd)
- [fhs-2.3.pdf](https://www.pathname.com/fhs/pub/fhs-2.3.pdf)
# Permisos de ficheros/carpetas
Para modificar permisos en linux utilizamos 3 comandos principales: `chown`, `chgrp` e `chmod`.
## Cambiar o owner dun fichero/carpeta
Para cambiar o owner utilizamos o comando `chown`.
```bash
chown {username} fichero/carpeta
```

Tamén podemos cambiar o grupo ao mismo tempo utilizando este comando.
```bash
chown {username}:{groupname} fichero/carpeta
```
## Cambiar o grupo dun fichero/carpeta
Para cambiar soamente o grupo utilizamos o comando `chgrp`.
```bash
chgrp {groupname} fichero/carpeta
```
## Cambiar permisos de acceso de ficheros/carpetas
Para asignar permisos a ficheros en Linux utilizamos o comando `chmod`. Este comando permite cambiar os permisos de lectura, escritura e execución para o propietario, o grupo e outros usuarios. Por exemplo, para dar permisos de lectura, escritura e execución ao propietario, e só de lectura ao grupo e outros, utilizamos:
```bash
chmod 755 ficheiro
```

Os permisos indícanse mediante un código numérico onde cada díxito representa os permisos para o propietario, o grupo, e outros, respectivamente. Este código sale da súma dos seguintes números en función do que permiso que queiramos otorgar:

| Lectura   | 4   |
| --------- | --- |
| Escritura | 2   |
| Execución | 1   |
En función do tipo de acceso que queiramos asignar debemos sumar estos 3 números para asignar o permiso axeitado.
## Link simbolicos
```bash
sudo ln -s {rutaOrixe} {rutaDestino}
```

Podemos cambiar o owner e grupo do link simbolico co seguinte comando
```bash
sudo chown -h {usuario}:{grupo} {link_simbolico}
```

> [!NOTE] Nota
> É importante recalcar que aunque se cree un link simbolico dunha carpeta, á hora de poñer a _rutaDestino_ non hai que poñer a `/` ao final da _rutaDestino_. Esto é igual para cando utilizamos o `chown`, a `/` ao final non hai que poñela.

