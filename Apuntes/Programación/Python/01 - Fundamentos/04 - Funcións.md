---
tags:
  - python/fundamentos
---
# Funcions
Unha **función** é un bloque de código reutilizable que realiza unha tarefa específica cando se chama, está composta por un nombre e parámetros (opcionales). As funcions permitennos modularizar o código, mellorar  a legibilidade e facilitar o mantemento ao dividir o programa en bloques máis pequenos e manexables. Para definir unha función en python utilizase a palabra clave “def”, seguida do nombre da función.
## Creación dunha función
Definición de función básica.
```python
def hola():
	print("hola mundo!!")

hola()
```
## Pasarlle parámetros a unha función
Unha función tamén pode recibir parámetros para usalos dentro dela como variables.
```python
def hola(nombre):
	print(f"hola {nombre}")

hola("jano")
```
