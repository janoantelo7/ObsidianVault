---
tags:
  - utilidades
---
# Instalación
Vim é un editor de texto presente na maioría dos sistemas Unix. A instalación de Vim varía segundo o sistema operativo que esteas a utilizar. En moitas distribucións de Linux, Vim xa está preinstalado, aínda que pode ser unha versión mínima. No caso de non estar instalado ou de querer unha versión máis recente, podes instalarlo facilmente a través do [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Instalar paquetes|gestor de paquetes]] da túa distribución. 

Por exemplo en Debian podemos instalalo co seguinte comando:
```bash
sudo apt install vim
```
# Edición de ficheros
## Remplazar
En vim para remplazar podemos utilizar expresións regulares. A sintaxis de remplazar en vim é a siguiente:
```bash
:[rango]s/patron/reemplazo/[opcions]
```

O rango pode ser un dos siguientes:
- **Número:** Indicar un núemero de línea onde facer o remplazo
- **inicio,fin:** Indicar a línea de inicio e a línea de fin para o remplazo
- **$:** A última línea do fichero
- **%:** Todo o fichero

As opcións das que dispoñemos son:
- **c:** Obligate a confirmar cada un dos remplazos
- **g:** Remplaza todas as ocurrencias que aparezcan por línea. Se non se añade esto solo o fará para a primeira que aparezca
- **i:** Non distingue entre mayúsculas e minúsculas
- **l:** diferencia entre mayúsculas e minúsculas
