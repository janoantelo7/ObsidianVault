---
tags:
  - utilidades/linux
---
**Tmux** é un multiplexador de terminal, o que significa que permite aos usuarios abrir múltiples terminais independentes dentro dunha única ventana. Estas terminais poden ser usadas simultáneamente e tamén poden ser divididas en paneis dentro da mesma ventana.

Ademais, tmux permite aos usuarios cambiar facilmente entre as diferentes terminais e paneis, o que o fai unha ferramenta moi útil para os desarrolladores que necesitan manter diferentes procesos en execución ao mesmo tempo. Tmux tamén permite que as sesións sexan desconectadas e reconectadas facilmente, o que significa que podes continuar traballando onde o deixaches, mesmo despois de cerrar a túa conexión.
# Instalación
Para instalar tmux nos distintos sistemas operativos podemos facelo da seguinte maneira:

| Plataforma                                                  | Comando de instalación |
| ----------------------------------------------------------- | ---------------------- |
| [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes\|Arch Linxu]]    | `pacman -S tmux`       |
| [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes\|Debian/Ubuntu]] | `apt install tmux`     |
| [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes\|Fedora]]        | `dnf install tmux`     |
| [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes\|RHEL]]          | `dnf install tmux`     |
| macOS                                                       | `brew install tmux`    |
# Comandos
Os distintos comandos que podemos utilizar para manexar tmux desde a terminal son:
- `tmux ls`: Permítenos listas as sesións activas.
- `tmux new -s <nombre>`: Creamos unha nova sesión de tmux con nombre.
- `tmux a`: Permítenos volver á última sesión de tmux que utilizamos.
- `tmux a -t <nombre>`: Permítenos escoller a que sesión nos queremos conectar.
# Atallos de teclado
Unha vez dentro de **tmux** temos varios comandos que podemos utilizar, os cales son:
- `ctrl+b+d`: Este comando permítenos deixar a sesión dettached. É decir, permitenos salir da terminal e cando queiramos podemos recuperar a sesión.
- `ctrl+b+%`: Dividir una ventana de tmux en verticales.
- `ctrl+b+"`: Dividir unha ventana de tmux en palenes horizontales.
- `ctrl+b+flecha`: Cambiarnos entre distintos paneles (mover en función da dirección do panel ao que queremos ir).
- `ctrl+b+x`: Cerrar o panel actual.
- `ctrl+b+c`: Crear unha nova ventana.
- `ctrl+b+n`: Pasar á siguiente ventana según o número.
- `ctrl+b+p`: Volver á ventana anterior.
- `ctrl+b+?`: Mostrar todos os atallos.
- `ctrl+b+w`: Listar todas as ventanas da sesión actual.
# Habilitar o uso do ratón
Se queremos habilitar o uso do ratón en **tmux** debemos facer os seguintes pasos:
1. Creamos un fichero chamado `.tmux.conf` que gardará a nosa configuración de `tmux`.
```bash
touch ~/.tmux.conf
```
2. En este fichero escribimos o seguinte:
```bash
set -g mouse on
```
3. Salimos das sesións de **tmux** e matamos o servidor con `tmux kill-server` para que recargue a configuración.

Unha vez feitos estos pasos a próxima vez que iniciemos **tmux** podremos utilizar o ratón para movernos entre os paneles e facer scroll coa roda na terminal.
# Links
* [Cómo usar tmux: cheat sheet con consejos útiles (hostinger.es)](https://www.hostinger.es/tutoriales/usar-tmux-cheat-sheet) 