---
tags:
  - python/fundamentos
---
Python proporcionanos os seguintes tipos estructurados:

|                   | ARRAY | TUPLA | LISTA |     SET      | DICCIONARIO |
| ----------------- | ----- | :---: | :---: | :----------: | :---------: |
| ORDENADO (index.) | X     |   X   |   X   |              |             |
| NO ORDENADO       |       |       |       |      X       |      X      |
| MUTABLE           | X     |       |   X   | X (sin dup.) |      X      |
| INMUTABLE         |       |   X   |       |              |             |
# Secuencias
Varios dos tipos estructurados para o manexo de coleccións son de tipo **secuencia** (array, lista, tupla, string). Cada elemento da colección encontrase nunha posición concreta (índice) dentro da secuencia.
## Operacións Comúns
- `x [not] in s`: `True` se x {non} é igual a un ítem de S. `False` no caso contrario.
- `s + t`: Concatenación das secuencias S e T.
- `s * n`: Repetición da secuencia _S_ un número _n_ de veces.
- `s[i]`: Ítem na posición `i` da secuencia. Sendo `0` o índice do primeiro elemento.
- `s[i:j]`: Fragmento da secuencia desde `i` ata (J-1).
- `s[i:j:k]`: Fragmento da secuencia desde `i` ata (J-1) con salto `k`.
- `len(s)`: Lonxitude (número de elementos) de S.
- `min(s)`: Valor menor de S.
- `max(s)`: Valor maior de S.
- `s.index(x)`: Índice da primeira ocurrencia de _X_ en S.
- `s.count(x)`: Número total de ocurrencias do valor _X_ na secuencia S.
## Operacións en secuencias mutables
- `s[i] = x`: O ítem na posición `i` é reemplazado por X.
- `s[i:j] = t`: O fragmento de S desde `i` ata `j` é reemplazado polo contido do iterable T.
- `del s[i]`: Elimina o ítem da posición `i`.
- `del s[i:j]`: Elimina os items desde a posición `i` ata a posición `j`.
- `del s[i:j:k]`: Elimina os items desde a posición `i` ata a posición `j` con salto `k`.
- `s.append(x)`: Añade _X_ ao final da secuencia S.
- `s.clear()`: Elimina todos os ítems de S (non dispoñible en _array_).
- `s.copy()`: Crea unha copia de S (shallow copy).
- `s.insert(i, x)`: Inserta _X_ na posición `i` da secuencia S.
- `s.pop()`: Elimina da secuencia o último ítem. **Devolve** o ítem eliminado.
- `s.pop(i)`: Elimina da secuencia o ítem da posición `i`. **Devolve** o ítem eliminado.
- `s.remove(x)`: Elimina da secuencia a primeira ocurrencia de _X_.
- `s.reverse()`: Invirte o orden da secuencia.
## Iteración sobre a secuencia
Unha das características de estas estructuras de datos, ao igual que os [[01 - Datos e operadores#Strings|Strings]], é que soportan a iteración a través dos seus elementos. Esto permitenos recorrelos fácilmente mediante bucles do tipo [[02 - Estructuras de control#Bucle `for-in`|For]] como podemos ver nos seguintes exemplos:

```python
# recorremos un string
for char in "hola mundo!":
	print(char, end=" ")
```

```python
# recorremos unha lista
for elemento in [1,2,3]:
	print(elemento)
```

```python
# recorremos unha tupla

t = (1,2,3)

for i in t:
	print(i)
```

```python
# recorremos un set
for x in {1,2,3}:
	print(x)
```

```python
# recorremos un diccionario
dic = {'un': 1, 'dous': 2, 'tres': 3}

for key in dic:
	print(key, dic[key])
```
# Arrays
Os **arrays** son o método tradicional de crear coleccións de datos primitivos, onde todos os datos da colección son do **mesmo tipo**.

Polo xeral, cando a xente fala de arrays en Python, soen referirse a listas. Sen embargo, son estructuras de datos diferentes. En Python, os arrays podense ver como unha maneira **eficiente** de almacenar certas listas de datos onde todos os elementos son do mesmo tipo. Ainda así, seu uso é escaso e limitado a determinados campos (por exemplo, I/O). A día de hoxe, se buscamos almacenamento e procesado eficiente de coleccións (especialmente de tipos númericos), empleamos librerías como numpy.

En Python, o sporte de arrays proporcionaos o **módulo array** que debe ser importado antes de poder inicializalos e usalos. Durante a creación do array, debemos indicar o seu **tipo** de dato, **limitando** desta maneira o **rango** e tipo de valores almacenados.
## Tabla de tipos
| CÓDIGO DE TIPO | TIPO-C EQUIVALENTE | TIPO PYTHON | TAMAÑO (bytes) | RANGO DE VALORES |
| :---: | --- | --- | :---: | :---: |
| 'b' | signed char | int | 1 | [-2<sup>7</sup>, 2<sup>7</sup>-1]<br><br>[-128, 127] |
| 'B' | unsigned char | int | 1 | [0, 2<sup>8</sup>-1]<br><br>[0, 255] |
| 'u' | wchar_t | Unicode | 2 | '\u0000' - '\uFFFF' |
| 'h' | signed short | int | 2 | [-2<sup>15</sup>, 2<sup>15</sup>-1]<br><br>[-32.768, 32.767] |
| 'H' | unsigned short | int | 2 | [0, 2<sup>16</sup>-1]<br><br>[0, 65.535] |
| 'i' | signed int | int | 4(2<sup>*</sup>) | [-2<sup>31</sup>, 2<sup>31</sup>-1]<br><br>[-2.147.483.648, 2.147.483.647] |
| 'I' | unsigned int | int | 4(2<sup>*</sup>) | [0, 2<sup>32</sup>-1]<br><br>[0, 4.294.967.296] |
| 'l' | signed long | int | 8(4<sup>*</sup>) | [-2<sup>63</sup>, 2<sup>63</sup>-1]<br><br>[--9.223.372.036.854.775.808,<br>9.223.372.036.854.775.807] |
| 'L' | unsigned long | int | 8(4<sup>*</sup>) | [0, 2<sup>64</sup>-1]<br><br>[0, 18.446.744.073.709.551.615] |
| 'f' | float | float | 4 | [1.2E-38, 3.4E+38] |
| 'd' | double | double | 8 | [2.3E-308, 1.7E+308] |
## Creación de Arrays
Para crear arrays debemos indicar o seu **tipo** e, **opcionalmente**, un **inicializador** ou lista de valores.

```python
# importamos a librería array
import array as arr
```

```python
# creamos un array de bytes vacío
udata = arr.array('B')
print(udata)
print("número de elementos:", len(udata))
```

```python
# creamos un array de bytes inicializado con varios elementos
udata = arr.array('B')
print(udata)
print("número de elementos:", len(udata))
```
## Métodos
A librería arrays proporcionanos unha serie de métodos para operar co seu contido. Algúns son:
- `a[i:j]`: Fragmento do array desde `i` ata (`j`-1).
- `a[i:j:k]`: Fragmento do array desde `i` ata (`j`-1) con salto `k`.
- `a[i] = x`: O ítem na posición `i` é reemplazado por _X_.
- `a[i:j] = t`: O fragmento de A desde `i` ata  `j` é reemplazado polo contido do array T.
- `a.itemsize`: Longitude en Bytes dun elemento do array A.
- `a.append(x)`: Añade un elemento X ao array A.
- `a.count(x)`: Devolve o número de ocurrencias de X no array A.
- `a.extend(i)`: Añade os elementos do iterable `i` ao final do array. Se `i` é un array, debe ser do mesmo tipo.
- `a.index(x)`: Indice dende a primeira ocurrencia de X en A.
- `a.pop()`: Elimina do array o último ítem. **Devolve** o item eliminado.
- `a.pop(i)`: Elimina do array o ítem da posición `i`. **Devolve** o ítem eliminado.
- `a.remove()`: Elimina do array a primeira ocurrencia de X.
- `a.reverse()`: Invirte o orden do array.
- `a.fromlist(s)`: Añade os ítems da lisa S.
- `a.tolist()`: Convirte o array nunha lista.
- `a.frombytes(s)`: Añade os items da secuencia de bytes S.
- `a.tobytes()`: Convirte o array nunha secuencia de bytes.
- `a.fromfile(f, n)`: Lee _n_ ítems do fichero, e añadeos ao array.
- `a.tofile(f)`: Escribe o array como secuencia de bytes no fichero f.
# Tuplas
As **tuplas** son secuencias **inmutables**, xeralmente empleadas para o almacenamento ordenado de datos **heterogéneos**. A súa diferencia fundamental coas **listas** é que, unha vez creada, non pode ser modificada.  Suelen emplearse para almacenar secuencias de valores constantes (por exemplo, as claves dun diccionario) ou retornos de funcións de varios valores.

As tuplas poden ser construidas de diferentes maneiras:
- Usando un par de **paréntesis** para denotar a **tupla vacía**: `( )`
- Usando una **coma final** para unha tupla simple: `a,` ou `(a,)`
- Separando os ítems con **comas**: `a, b, c` ou `(a, b, c)`
- Usando o contructor `tuple()` ou `tuple(iterable)`.
# Listas
Como as tuplas, as **listas** son secuencias indexadas de datos do mesmo ou diferente tipo. A principal diferencia é que as listas son **mutables**. É decir, unha vez creadas, poden ser modificadas.

Este feito aporta unha gran flexibilidade. Por outro lado, pode dar lugar a situacións indeseables. Por exemplo, unha lista pasada a unha función, podría ver modificado o seu contido no interior da mesma.

As listas poden ser construidas de diferentes maneiras:
- Usando un par de **corchetes** para denotar a **lista vacía**: `[ ]`
- Usando **corchetes**, separando os ítems con comas: `[a]` ou `[a, b, c]`
- Usando listas **por compresión**: `[x for x in iterable]`.
- Usando o constructor `list()` ou `list(iterable)`

Ademáis dos métodos e operacións das secuencias mutables, as listas dispoñen tamén do método `sort()`.