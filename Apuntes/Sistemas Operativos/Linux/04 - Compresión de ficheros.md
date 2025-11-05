---
tags:
  - linux
---
En este documento vamos a ver unha guía básica de como comprimir e descomprimir ficheros en sistemas operativos Linux. En esta vemos as ferramentas máis comúns como poden ser `tar`, `gzip` e `zip`.
# Tar
Con **tar** podemos traballar coas seguintes extensions de fichero: `.tar`, `.tar.gz` e `tar.bz2`. Esta ferramenta soe vir preeinstalada nas mayorías de distribucións.
## Comprimir en .tar
Para comprimir una carpeta en `.tar` temos que utilizar o seguinte comando.
```bash
tar -cvf archivo.tar /home/carpeta
```
## Comprimir en .tar.gz
Podemos comprimir unha carpeta en `.tar.gz` debemos utilizar o siguiente comando. Para traballar con ficheros `.tar.gz` debes añadir a opción `z`.
```bash
tar -cvzf archivo.tar.gz /home/carpeta
```

Se queremos comprimir varios ficheros podemos facelo da seguinte maneira
```bash
tar -cvzf archivo.tar.gz archivo1 archivo2 archivo3
```
## Comprimir en .tar.bz2
Podemos comprimir unha carpeta en `.tar.bz2` co seguinte comando. Para traballar con ficheros `.tar.bz2` debemos añadir a opción `j`.
```bash
tar -cvjf archivo.tar.bz2 /home/carpeta
```
## Comprimir en .tar.xz
Este formato de compresión é moi interesante, xa que aunque sexa lento ten un moi bo factor de compresión. Para comprimir podemos utilizar o seguinte comando:
```bash
tar -cvJf archivo.tar.xz /home/carpeta
```
## Descomprimir todos os ficheros
Se queremos descomprimir un dos ficheros que creamos anteriormente debemos utilizar o seguinte comando. Este comando sirve para os tres tipos de fichero que vimos.
```bash
tar -xvf archivo.tar
```

Este comando descomprime na misma ruta que estamos, pero tamén podemos querer descomprimir o fichero en outra ruta. Para eso utilizaremos a opción `-C`.
```bash
tar -xvf archivo.tar -C /home/FicherosExtraidos/
```
## Descomprimir un fichero
Se queremos extraer un único fichero de un archivo comprimido, podemos facelo co seguinte comando.
```bash
tar -xvf archivo.tar ejemplo.sh
```

Esto funciona para os tres tipos de fichero, se o fichero está dentro de varias carpetas podemos utilizar a opción `--strip-components`.
```bash
tar -xvf archivo.tar carpeta/ejemplo.sh --strip-components=1
```
## Listar o contenido
Podemos listar o contenido dos ficheros comprimidos co seguinte comando. Este comando funciona para os tres tipos de fichero.
```bash
tar -tvf archivo.tar
```
# Gzip
O comando **gzip** é utilizado para comprimir ficheros en formato `.gz`. A continuación vamos a ver o uso básico de este comando.  Esta ferramenta soe vir preinstalada na mayoría dos sistemas Linux.
## Comprimir un fichero
Para comprimir un fichero podemos utilizar o seguinte comando.
```bash
gzip <fichero>
```
## Mostrar información
Se utilizamos o parámetro `-l` podemos ver información sobre a relación de compresión ou canto se comprimiu do fichero.
```bash
gzip -l <fichero.gz>
```
## Descomprimir un fichero
Para descomprimir un fichero podemos facelo de dúas maneiras, co parámetro `-d` ou coa ferramenta `gunzip`. 

Se queremos facelo co parámetro `-d` facemolo da seguinte maneira.
```bash
gzip -d <fichero.gz>
```

Con `gunzip` facelomo da seguinte maneira.
```bash
gunzip <fichero.gz>
```
## Mostrar o contenido de un fichero
Podemos mostrar o contenido de un fichero co seguinte comando.
```bash
gunzip -l <fichero.gz>
```
## Mostrar o texto de un fichero comprimido
Se temos un fichero de texto comprimido podemos acceder ao contenido de este fichero utilizando o seguinte comando.
```bash
zcat <fichero.gz>
```
# Zip
Esta ferramenta utilizamola para traballar con ficheros `.zip`. Con ela podemos comprimir e descomprimir ficheros. É moi útil cando traballamos con ficheros entre Linux e Windows xa que funciona nos dous sistemas. Polo general en Linux non suele vir preinstalada esta ferramenta polo que a deberemos instalar co [[Apuntes/Sistemas Operativos/Linux/01 - Introducción#Gestión de paquetes|xestor de paquetes]] da nosa distrubución.
## Comprimir un fichero
Se queremos comprimir un fichero utilizamos o seguinte comando:
```bash
zip fichero.zip documento
```

En caso de que queiramos comprimir unha carpeta utilizamos o seguinte comando:
```bash
zip -r directorio.zip carpeta/
```
## Descomprimir un fichero
Podemos descomprimir un fichero zip na ruta na que estamos co seguinte comando:
```bash
unzip archivo.zip
```

Se queremos descomprimilo en outra ruta podemos utilizar a opción `-d` para indicar a ruta de descompresión. Podemos ver un exemplo no seguinte comando:
```bash
unzip archivo.zip -d carpeta/
```
Se xa existen os mismos ficheros na ruta de destino, podemos sobreescribilos todos coa opción `-o`.

