---
tags:
  - python/fundamentos
---
# Variables
As variables son elementos que nos posibilitan almacenar valores para o seu uso posterior. De forma general, a asignación dunha variable ten a seguinte sintaxis: `variable = expresion`.

O nombre dunha variable é o seu **identificador**. Para que un identificador sexa válido debe estar formado por letras, númeors (non pode empezar por números) ou con barra baixa (`_`). Como convención suelense utilizar nomes en minúsculas e cando usamos varias palabras unimolas mediante `_`. Por exemplo: `variable_dos_palabras = valor`.

Se necesitamos crear unha variable valeira en Python podemos facelo coa seguinte sintaxis: `variable = None`.
# Tipos de datos
## Númericos
En Python podemos ter varios tipos de números, entre os que distinguimos os seguintes:
- Números enteiros (`int`): Podemos almacenar números enteiros de calquer longitud
- Números flotantes (`float`): Emplea precisión doble (Estándar: IEEE-754 bin64)  
- Números complexos (`complex`): Ten parte (**.real**) e parte imaginaria (**.imag**) do tipo float. Teñen a siguiente forma: `parte_real + parte_imaginaria*j`
	- Unha parte real: 3
	- Parte imaginaria: 5j

A maiores de estos, a librería estándar de Python tamén conten tipos de datos adicionais para:
- Fraccions (`fraction`)
- Números decimales de precisión configurable (`decimal`)

```python
# suma de dous enteiros
a = 3 + 2
print(a)

# a division genera un float
b = 5/5
print(b)

# a función type permitenos determinar o tipo dun literal ou expresión
c = 1 + 3j
print(type(c))
print(type(c.real))
print(type(c.imag))
```

Output:
```shell
5
1.0
<class 'complex'>
<class 'float'>
<class 'float'>
```
### Operadores aritméticos
| Operacion       | Operador | Asociatividad | Precedencia |
| --------------- | -------- | ------------- | ----------- |
| Exponencial     | **       | derecha       | 1           |
| Cambio de signo | -        |               | 2           |
| Multiplicación  | *        | izquierda     | 3           |
| División        | /        | izquierda     | 3           |
| División entera | //       | izquierda     | 3           |
| Módulo (resto)  | %        | izquierda     | 3           |
| Suma            | +        | izquierda     | 4           |
| Resta           | -        | izquierda     | 4           |
- **Asociatividad**: define o **orden de execución** cando hai varios **operadores iguais** e non hai paréntesis. Por exemplo: `2**3**2` evaluase como `2**(3**2)`. As operacións con asociatividade á esquerda utilizan o estándar das operacións aritméticas.
- **Precedencia**: Establece a **prioridad** de unhas operacións sobre outras. Os números máis baixos teñen máis prioridade e executanse primeiro.
### Representación de enteiros
A maiores de en base 10, tamén podemos representar números en base binaria, octal e hexadecimal. Para indicar as bases temos que antepoñer o prefijo ao número correspondente: **0b** (binario), **0o** (octal), **0x** (hexadecimal). Por exemplo: `a = 0b110101`.
## Valores lóxicos
En Python podemos utilizar o tipo **bool** para representar os valores lóxicos. Os dous valores posibles de estos tipos son: **True** e **False**. Estos tipos son utilizados para representar o resultado de operacións lóxicas.
### Operadores lóxicos
Python proporcionanos tres operadores lóxicos, os cales son:

| Operación  | Operador | Precedencia |
| ---------- | -------- | ----------- |
| negación   | not      | 1           |
| 'y' lógico | and      | 2           |
| 'o' lógico | or       | 3           |
Cando traballamos con estos operadores é importante ter en conta as seguintes **tablas de verdade**:
* ***and**

| and   | False | True  |
| ----- | ----- | ----- |
| False | False | False |
| True  | False | True  |
- **or**

| or    | False | True |
| ----- | ----- | ---- |
| False | False | True |
| True  | True  | True |
- **not**

|not|False|True|
|---|---|---|
||True|False|
### Operadores de comparación
En Python temos dispoñibles os seguintes operadores de comparación que devolven un resultado booleano **True** ou **False**. Todos teñen a mesma precedencia, maior que a dos opreadores lóxicos.

| Operador   | Descripción             |
| ---------- | ----------------------- |
| `<`        | Menor que               |
| `<=`       | Menor ou igual que      |
| `>`        | Maior que               |
| `>=`       | Maior ou igual que      |
| `==`       | Igual que               |
| `!=`       | Distinto a              |
| `is [not]` | Igualdad entre obxetos  |
| `[not] in` | Pertenencia á colección |

## Strings
Os **strings** ou cadenas de carácteres, son cadenas de texto. Para definir un string en python podemos utilizar comillas simples ou comillas dobles. Así `'hola'` é igual que `"hola"`. 

Podemos mostrar a cadena de texto coa función `print`.
```python
print("Hola Mundo!")
```

Se queremos definir un string de varias líneas temos que facelo con 3 comillas, valendo tanto simples como dobles.
```python
texto = """
Esta é unha cadea de texto que ocupa varias líneas, para definila debemos utilizar 3 comillas sexan dobles ou simples.
"""
print(texto)
```
### Operacións con strings
En Python podemos realizar varias operacións con strings como pode ser **concatenar** varias cadenas de texto. Para eso, utilizamos o operador da suma (`+`)
```python
cadea1 = "Hola "
cadea2 = cadea1 + "Mundo!"
print(cadea2)
```

Output:
```shell
Hola Mundo!
```
### Modificando os strings
Python ten varios **métodos** para modificar os strings. 
#### Mayúsculas
O método `upper()` devolvenos a cadea de texto en mayúsculas.
```python
texto = "Hola Mundo!"
print(texto.upper())
```
#### Minúsculas
O método `lower()` devolve a cadea de texto en mínusculas.
```python
texto = "Hola Mundo!"
print(texto.lower())
```
#### Eliminar espacios en branco
Podemos eliminar os espacios en branco antes e despois do texto co método `strip()`
```python
texto = " Hola Mundo! "
print(texto.strip())
```
#### Separar o string
O método `split()` devolvenos unha lista que contén o texto que está entre o separador que indicamos.
```python
texto = "Hola, Mundo!"
print(texto.split(","))
```
# Pip
**Pip** é un gestor de paquetes de python. Os comandos que podemos utilizar en pip son os siguientes:
- **`pip install {package_name}`** : Instalar un paquete.
- **`pip uninstall {package_name}`**: Desinstalar un paquete.
- **`pip install --upgrade package_name`**: Actualizar un paquete.
# Virtualenv
**Virtualenv** é unha ferramenta de python para crear un sandbox de python e así poder separar os paquetes de python dos paquetes do sistema. É bastante recomendable utilizar esto. Os comandos que podemos utilizar para administrar venvs son os siguientes: 

Crear un novo virtual enviroment.
```bash
python3 -m venv <ruta_destino>/<nombre>
```

Activar venv en Linux.
```bash
source <ruta_destino>/<nombre>/bin/activate
```

Activar venv en Windows.
```powershell
.\<ruta_destino>\<nombre>\Scripts\Activate.ps1
```

Desactivar un venv.
```bash
deactivate
```
