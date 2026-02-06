---
tags:
  - linux
---
# stdin, stdout e stderr
Á hora de falar de procesado de texto é importante coñecer ben os conceptos de `stdin`(entrada estándar), `stdout`(salida estándar) e `stderr`(estándar error).

Cada un destos canales ten a súa función específica. `stdout` é o canal polo que a maioría dos comandos da tarminal mandan información. `stderr` é o canal polo que se envían mensajes de error. Esta distinción é importante á hora de facer [[03 - Scripting con Bash|scripts]].  A continuación vamos a ver uns exemplos en como redirigir a salida de un comando aos distintos canales.
## Ejemplos
1. **Redirigir cada tipo de salida a un fichero distinto**
```bash
ls -l > stdout.txt 2> stderr.txt
```
En este exemplo redirigimos a salida estándar do `ls` a un fichero chamado "*stdout.txt*" e a salida de error de este comando a un fichero chamado "*stderr.txt*".

2. **Redirigir a salida de error á salida estándar**
Este é un caso de uso bastante interesante no que nos intersa gardar en un fichero, tanto a salida de estándar, como os posibles errores que nos poidamos atopar á hora de executar un comando ou un script.
```bash
ls archivo_que_no_existe > salida.txt 2>&1
```
# Buscando con grep
Buscar un patrón en un fichero
```bash
grep "[PATRON_BUSQUEDA]" ruta/ao/fichero
```

Búsqueda recursiva
```bash
grep -R "[PATRON_BUSQUEDA]" ruta/ao/fichero
```

Lineas que non coinciden co patrón de búsqueda
```bash
grep -v [PATRON_BUSQUEDA] ruta/ao/fichero
```
