---
tags:
  - scripting/python
---
# Uso de argumentos na línea de comandos
Empregaremos dúas ferramentas esenciais: `sys.argv` e `argparse`. Estas dúas axudas permiten transmitir datos directamente dende a liña de comandos, ofrecendo un medio poderoso para personalizar o comportamento dos nosos programas. Ao entender como funcionan estas técnicas, poderemos construír aplicativos máis interactivos e versátiles, capaces de adaptarse ás necesidades específicas dos usuarios.
## sys.argv
Podemos utilizar o modulo `sys`, co atributo `argv` para acceder á [[01 - Datos e operadores#Listas|lista]] de argumentos que lle envias ao script. Esta non é a maneira máis robusta de escribir scripts que reciban argumentos pero é bastante sencilla para facelo.
### Ejemplo
O que fai `sys.argv` é gardar en unha lista os parámetros todos que se envian co script, polo tanto podemos xogar con eles ao igual que xogaríamos con calquer outra lista de python.

```python
#!/usr/bin/env python

import sys

print(f"lista de argumentos: {sys.argv}")
print(f"primeiro argumento usable da lista: {sys.argv[1]}")
print(f"lista sin o nombre do script: {sys.argv[1:0]}")
```

Salida de execución
 ```
(venv) DESKTOP-OI7MJLM:poc jano$ ./test.py hola jano "que tal"
lista de argumentos: ['./test.py', 'hola', 'jano', 'que tal']
primeiro argumento usable da lista: hola
lista sin o nombre do script: ['hola', 'jano', 'que tal']
```
## argparse
`argparse` é un módulo incorporado en python para facilitar a creación de interfaces de liña de comandos. Esta ferramenta permite definir os argumentos que o teu script pode recibir, xestionar as mensaxes de axuda e os erros de forma automática. É máis completo e flexible que `sys.argv` e é recomendado para scripts máis complexos.
### Ejemplos
#### Ejemplo 1 - Básico
Script básico que mostra o funcionamento de argparse, en recibese o nombre de un fichero e recibe como parámetro opcional o número de líneas.

```python
#!/usr/bin/env python

import argparse

# iniciamos o argumento parser que analizará os argumentos
parser = argparse.ArgumentParser(description="Programa de prueba")

# añadimos argumentos posicionales
parser.add_argument("filename", help="Introduce o nombre do fichero")

# añadimos argumentos opcionales
parser.add_argument("--limit", "-l", type=int,help="número de lineas a leer")

# creamos un objeto args para acceder aos argumentos
# é necesario para que funcionen os parametros
args = parser.parse_args()

print(f"Lista de argumentos: {args}")
print(f"Nombre do fichero: {args.filename}")
print(f"Número de lineas: {args.limit}")
```

Salida de execución
```
(venv) DESKTOP-OI7MJLM:poc jano$ ./test.py -l 10 hola.txt
Lista de argumentos: Namespace(filename='hola.txt', limit=10)
Nombre do fichero: hola.txt
Número de lineas: 10
```
#### Ejemplo 2 - Versionar script
En este ejemplo vemos como añadir a versión do programa, é un elemento moi frecuente e interesante manter o versionado das nosas ferramentas para que o usuario poida saber se está a utilizar a última versión.

```python
#!/usr/bin/env python

import argparse

# iniciamos o argumento parser que analizará os argumentos
parser = argparse.ArgumentParser(description="Programa de prueba", prog="lector")

# añadimos argumentos posicionales
parser.add_argument("filename", help="Introduce o nombre do fichero")

# añadimos argumentos opcionales
parser.add_argument("--limit", "-l", type=int,help="número de lineas a leer")

# añadimos un argumento opcional que mostra o nombre do programa definido en "prog" e mostra a version
parser.add_argument("--version", "-v", action="version", version="%(prog)s 1.0")

# creamos un objeto args para acceder comodamente aos argumentos
args = parser.parse_args()

print(f"Lista de argumentos: {args}")
print(f"Nombre do fichero: {args.filename}")
print(f"Número de lineas: {args.limit}")
```

Salida de execución:
```
 (venv) DESKTOP-OI7MJLM:poc jano$ ./lector.py -v
lector 1.0
```
#### Ejemplo 3 - Descripción Multilínea
En este ejemplo vemos como podemos crear unha descripción con varias líneas con argparse.

```python
#!/usr/bin/env python

import csv
import argparse
import textwrap
import os
import sys


description = textwrap.dedent('''\
This script receives a CSV file containing user information and generates SQL queries to create users in Snowflake and grant them specific roles.
The generated SQL queries are written to two separate files: one to create the users and another to grant them roles.

The CSV file must follow the following format:
display name, last name, email, given name    
''')

parser = argparse.ArgumentParser(formatter_class=argparse.RawDescriptionHelpFormatter,description=description, prog="queryCreator")
parser.add_argument("filename", help="The name of the CSV file")
parser.add_argument("--file1", "-f", default="create.sql", help="The name of the output file for create queries (default: create.sql)")
parser.add_argument("--file2", "-F", default="grant.sql", help="The name of the output file for grant queries (default: grant.sql)")
parser.add_argument("--version", "-v", action="version", version="%(prog)s 1.6")
args = parser.parse_args()

if not os.path.isfile(args.filename):
    print(f"Error: {args.filename} file not found")
    sys.exit(1)


f = open(args.file1,"w")
f2 = open(args.file2,"w")


with open(args.filename, mode="r") as csv_file:
    users = csv.DictReader(csv_file)
    
    for user in users:
        login = user["mail"].split("@")[0]
        f.write(f"CREATE OR REPLACE USER {login} PASSWORD='' LOGIN_NAME='{user['mail']}' DISPLAY_NAME='{user['displayName']}' DEFAULT_ROLE='PUBLIC' DEFAULT_WAREHOUSE='SE_DEMO_WH_XS' FIRST_NAME='{user['givenName']}' LAST_NAME='{user['surname']}' EMAIL='{user['mail']}' MUST_CHANGE_PASSWORD=FALSE;\n")
        f2.write(f"GRANT ROLE SE_USER_ROLE TO USER {login};\n")


f.close()
f2.close()
```

Salida do script cando mostramos a axuda con `-h`
```bash
DESKTOP-OI7MJLM:snowflake jano$ ./queryCreator.py -h
usage: queryCreator [-h] [--file1 FILE1] [--file2 FILE2] [--version] filename

This script receives a CSV file containing user information and generates SQL queries to create users in Snowflake and grant them specific roles.
The generated SQL queries are written to two separate files: one to create the users and another to grant them roles.

The CSV file must follow the following format:
display name, last name, email, given name

positional arguments:
  filename              The name of the CSV file

options:
  -h, --help            show this help message and exit
  --file1 FILE1, -f FILE1
                        The name of the output file for create queries (default: create.sql)
  --file2 FILE2, -F FILE2
                        The name of the output file for grant queries (default: grant.sql)
  --version, -v         show program's version number and exit
```
# Compresión de listas
A comprensión de listas en Python é unha maneira concisa e elegante de crear [[01 - Datos e operadores#Listas|listas]]. Permite construír unha lista aplicando unha expresión a cada elemento dunha secuencia (como outra lista, unha cadea de caracteres ou un rango) ou filtrando elementos dunha secuencia utilizando unha condición. Isto reduce a necesidade de escribir bucles explícitos e fai que o código sexa máis claro e conciso.
## Ejemplo
No siguiente ejemplo mostramos como construir unha lista cos números pares en base a unha lista que contén os números do 1 ao 15.

```python
#!/usr/bin/env python

# creamos a lista de números
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]

# creamos a lista pares a partir da lista de números
pares = [numero for numero in numeros if numero % 2 == 0]

# imprimimos a lista para ver o resultado
print(pares)
```

Salida de execución
```
DESKTOP-OI7MJLM:poc jano$ ./lector.py
[2, 4, 6, 8, 10, 12, 14]
```

A compresión de listas permitenos reducir as lineas de código e facer o código moito máis legible que a maneira tradicional de recorrer listas e crear unha nova, como se ve no exemplo inferior.

```python
#!/usr/bin/env python

# creamos a lista de números
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]

# creamos a lista pares vacia que recibirá os numeros pares
pares = []

# creamos o bucle que itera sobre a lista numero e añade os pares á lista pares
for numero in numeros:
    if numero % 2 == 0:
        pares.append(numero)

# imprimimos a lista para ver o resultado
print(pares)
```
# Librerías estándar útiles
En este apartado vamos a mencionar varias librerías útiles á hora de facer scripts en python as cales son `shutil` e `glob`.
## shutil
É un módulo en python que proporciona funcions de alto nivel para realizar operacions comuns con ficheros e directorios. As funcions principales de shutil son copiar ficheros, mover ficheros, eliminar ficheros e crear directorios.
### Ejemplo
```python
#!/usr/bin/env python

import shutil

# Copiar archivo
shutil.copy("archivo.txt", "copia.txt")

# Mover archivo
shutil.move("archivo.txt", "/nuevo/directorio")

# Eliminar directorio
shutil.rmtree("/tmp/directorio")

# Crear directorio
shutil.mkdir("/nuevo/directorio")
```
## glob
glob é un módulo en python que che permite busar e encontrar arquivos no teu sistema utilizando patróns de busqueda. glob utiliza comodins para representar caracteres nos nombres de arquivo, os máis comuns son:
- `*`: Coincide con calquer número de caracteres
- `?`: Coincide con un solo caracter.
- `[ ]`: Coincide con calquer caracter dentro dos corchetes, moi utilizado para os rangos
### Ejemplos
#### Ejemplo 1 - Básico
En este ejemplo podemos ver como mostramos os ficheros `*.py` que existen dentro da carpeta `/home/jano/src/poc`.  O que fai `glob.glob` é devolver unha lista que contén a ruta dos ficheros como se pode ver na salida do script.
```python
import glob

pattern = "*.py"

py_files = glob.glob("/home/jano/src/poc/"+pattern)

for file in py_files:
    print(file)
```

Salida de execución
```bash
> (venv) DESKTOP-OI7MJLM:poc jano$ ./script.py               
/home/jano/src/poc/script.py
```
#### Ejemplo 2 - Recursivo a unha ruta
Basandonos no ejemplo anterior, modificamos un pouco o script para añadir recursividad e que busque os ficheros `*.ps1` en toda a ruta indicada.
```python
import glob

pattern = "*.ps1"

py_files = glob.glob("/home/jano/src/**/"+pattern, recursive=True)

for file in py_files:
    print(file)
```

Salida de execución
```
(venv) DESKTOP-OI7MJLM:poc jano$ ./script.py
/home/jano/src/poc/venv/bin/Activate.ps1
/home/jano/src/dt-sysscripts/hosts/datahub8/scripts/virtuallabs/Rocky9_Datahub8.ps1
/home/jano/src/dt-sysscripts/poc/autopilot/autopilot-computer_report.ps1
/home/jano/src/dt-sysscripts/poc/autopilot/GetInstalledApplications.ps1
/home/jano/src/dt-sysscripts/poc/autopilot/Update_Windows_OS.ps1
/home/jano/src/dt-sysscripts/poc/autopilot/Get_HWID.ps1
/home/jano/src/dt-sysscripts/poc/autopilot/Autopilot_Computer-Report(email).ps1
/home/jano/src/dt-sysscripts/poc/intune-reporting/GetDeviceApps.ps1
/home/jano/src/dt-sysscripts/poc/intune-reporting/GetDetectedApps.ps1
/home/jano/src/dt-sysscripts/poc/MS-Graph/old/scriptazure.ps1
/home/jano/src/dt-sysscripts/poc/MS-Graph/old/scriptReto.ps1
/home/jano/src/dt-sysscripts/poc/MS-Graph/bulk_create-user/Bulk-new_users.ps1
/home/jano/src/dt-sysscripts/poc/MS-Graph/bulk_update-user/update_user-mail.ps1
/home/jano/src/dt-sysscripts/it-services/workstations/london_audit_report/Computer Report.ps1
```
