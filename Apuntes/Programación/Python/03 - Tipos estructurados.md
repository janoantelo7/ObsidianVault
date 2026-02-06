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

```python
# crear unha lista vacía
lista = []
lista
```

```python
# crear a lista cun inicializador
lista = [1, 2, 3 ,4]
```
## Indexado
Como o resto de secuencias ordenadas, podemos acceder aos elementos da lista mediante un índice ou extraer fragmentos da lista, que á súa vez será outra lista.

```python
# acceder a un elemento usando o índice (0 para o primeiro)
lista[3]
```

```python
# extraer un fragmento da lista
lista[2:4]
```

```python
# un índice fora do rango generará un erro
lista[5]
```
## Modificación da lista
### Añadir e modificar elementos

```python
# crear unha lista por concatenación con outra
lista_1 = [1, 2]
lista_2 = lista_1 + [2, 'a', 4]
```

```python
# añadir unha lista dentro de unha lista
lista_2 = []
lista_2.append(lista_1)
# añadir elementos sueltos á lista
lista_2.append("hola")
lista_2.append(3)
```

Podemos modificar os elementos:

```python
lista_2[2] = 999
lista_2[0][1] = 666
```

Nunha lista con elementos de diferentes tipos non se poden ordenar co método sort()

```python
lista = ["a", "ab", "A", "AB", "Z", "Ñ", "1"]
lista.sort()
```

É importante recalcar o seguinte, ainda que os métodos `append` e `extend` nos permiten añadir elementos a unha lista fano de diferente maneira:
- `append`: Añade o elemento suministrado mantendo o seu tipo, ao final da lista.
- `extend`: Añade de forma **individual** cada un dos elementos do _iterable_ suministrado como argumento.

```python
lista = [1, 2]

num = 5
tupla = (3, 4)
cadena = "hola"

lista.append(num)
lista.append(tupla)
lista.append(cadena)
```

A tupla que engadimos en esta lista conta como un único elemento da mesma:

```python
len(lista)
```

Añadir elementos con extend:

```python
lista = [1, 2]

lista.extend(tupla)
lista.extend(cadena)
```

Extend solo funciona con iterables, se intentamos o seguinte vai dar un error:

```python
lista.extend(num)
```
### Eliminar elementos

`del` permite eliminar un elemento polo seu índice:

```python
del lista[2]
```

Tamén nos permite eliminar un fragmento completo:

```python
del lista[6:]
```

`pop` elimina o último elemento (ou o elemento do índice suministrado) e devolveo:

```python
elemento_borrado = lista.pop()
print(lista)
print(f"elemento borrado: {elemento_borrado}")
```

Tamén podemos utilizar `remove` que elimina a primeira ocurrencia do valor indicado. Genera un error se no encontra.

```python
lista = [1, 2, 3, [1, 5]]
lista[-1].remove(5)
lista
```
## Creación de listas por compresión
A compresión de listas proporcionanos unha sintaxis reducida de cando queremos crear unha nova lista a partir dos valores de unha colección existente. Por exemplo, supoñamos que dada unha lista de nombres queremos extraer os que empecen pola letra 'A'.

Podríamolo facer cun bucle `for`:

```python
# Lista de nombres
nombres = ["Alejandro", "Pancho", "Jano", "Luis", "Cristiano", "Antonio"]

# Extracción de nombres que empezan por A (for)
nombres_A = []
for nom in nombres:
    if nom[0] == 'A':
        nombres_A.append(nom)
```

A compresión de listas permitenos facelo nunha única sentencia:

```python
nombres = ["Alejandro", "Pancho", "Jano", "Luis", "Cristiano", "Antonio"]

nombres_A = [nom for nom in nombres if nom[0] == "A"]
```
#### Sintaxis
A sintaxis máis simple dunha lista de compresión é a seguinte:

```python
nova_lista = [expresion for item in iterable]
```

- `item`: É cada un dos elementos do itreable que obtemos en cada iteracción
- `expresion`: Representa o valor final añadido á lista. Normalmente, será o ítem actual obtido na iteracción ou algunha manipulación sobre o mismo.
- `iterable`: É calquer obxecto composto por elementos que poidamos recorrer, como unha lista, unha tupla, un conxunto,...

Podemos **filtrar** os elementos que añadimos á lista usando a siguiente sintaxis:

```python
nova_lista = [expresion for item in iterable if condición(item) == True]
```

```python
# Crea unha lista cos números pares entre 0 e 9
lista = [n for n in range(10) if n%2 == 0]
```

Tamén se pode, unha vez extraído o elemento da colección desde a que creamos a lista (con ou sin condicional) aplicar unha condición `if-else` sobre o valor antes de engadilo á lista final. A súa sintaxis é a seguinte:

```python
nova_lista = [expresión_True if condicion_1 else expresión_False for item in iterable]
```

```python
nova_lista = [expresión_True if condición_1 else expresión_False for item in iterable if condición_2(item) == True ]
```

```python
# Sustituye os números negativos da lista por 0
nums = [5, -2, 10, 17, -13, 16, 4, -2]
lista = [n if n>0 else 0 for n in nums]
```

```python
# Extrae da lista números no rango [-10,10]. Sustituye os números negativos da lista por 0
nums = [5, -2, 10, 17, -13, 16, 4, -2]
lista = [n if n>0 else 0 for n in nums if abs(n)<=10]
```
## Converión entre listas e strings
Podemos facer conversións fácilmente entre listas e cadeas de caracteres mediante a función `list()` e os métodos `split()` e `join()` de strings.
- `list(s)`:  Crea unha lista a partir dos caracteres individuais do string `s`.
- `s.split(sep)`: Trocea a cadena `s` en subcadenas utilizando `sep` como separador (espacio se non se indica) e genera unha lista.
- `s.join(lista)`: Xenera unha cadea de caracteres concatenando os elementos (tipo `str`) de `lista` coa cadea `s`.

```python
s = "ola,     qué\ttal?"
list(s)
```

```python
# por defecto, usa calquer espacio en blanco como separador
"ola,     qué\ntal?".split('tal')
```

```python
print('\t'.join(["15", "02", "2022"]))
'\n'.join(["15", "02", "2022"])
```
## Ordenación
Para ordenar unha lista, todos os seus elementos teñen que ser do mesmo tipo e así poder comparalos. Dispoñemos da función `sorted()` e os métodos `sort()` e `reverse()` de `list`:
- `lista.sort()`: Ordena a `lista` (modificación sobre a lista original)
- `lista.reverse()`: Invirte o orden da `lista` (modifica sobre a lista original)
- `sorted(lista)`: Devolve unha nova lista ordenada a partir de `lista` (non modifica a lista original)

```python
lista = [3, 2, 1, 8, 2]
print("lista original:", lista)
print("lista ordenada:", sorted(lista))
print("lista original:", lista)
```

```python
lista = [3, 2, 1, 8, 2]
print("lista original:", lista)
lista.sort()
print("lista original:", lista)
```

```python
lista = [3, 2, 1, 8, 2]
print("lista original:", lista)
lista.reverse()
print("lista original:", lista)
```
## Mutabilidad e clonado
As listas son **objetos mutables** e esto pode ter efectos colaterales non deseados cando as utilizamos. As listas implementanse como **objetos en memoria** e as variables de tipo lista conteñen **referencias** que apuntan a ditos objetos.

Cando asignamos unha variable de tipo lista a outra variable, non se realiza unha copia da lista, senon que ambas conteñen a mesma referencia ao mesmo objeto en memoria (son **alias** da mesma lista).

Do anterior se desprende que, se **modificamos** unha das listas anteriores, a outra tamén se verá modificada. En realidade, hai unha única lista á que apuntan ambas variables.

Esto mismo ocurre cando pasamos unha lista como argumento a unha función. Non se pasa unha copia da lista, senon que se pasa unha referencai a mesma.

```python
x = [1, 2, 1]
y = x
x[2] = 3

print("x: ", x)
print("y: ", y)
print("id(x): ", id(x))
print("id(y): ", id(y))
```

Cando o que queremos é obter unha **copia** dunha lista, podemos facelo de diversas maneiras.
- mediante un bucle, agregando os elementos a unha nova lista:
```python
lista = [1, 2, 3]

copia = []
for n in lista:
    copia.append(n)

print("lista:", lista)
print("copia:", copia)
print(f"lista id: {id(lista)}; copia id: {id(copia)}")
```

- Utilizando o método `copy()`:

```python
lista = [1, 2, 3]

copia = lista.copy()

print("lista:", lista)
print("copia:", copia)
print(f"lista id: {id(lista)}; copia id: {id(copia)}")
```

- Empleando o **operador de indexado**:

```python
lista = [1, 2, 3]

copia = lista[:]

print("lista:", lista)
print("copia:", copia)
print(f"lista id: {id(lista)}; copia id: {id(copia)}")
```
### Shallow vs Deep copy
Os exemplos de copia de listas vistos son exemplos dos que se denomina **shallow copy** ou **copia superficial**. 

Esto quere decir, que cando creamos unha copia dunha lista estamos creando unha copia superficial do obxecto que é independente do orixinal. Os **obxectos contidos** (os elementos da lista) **non se copian**, senón que o novo obxecto refírese ás **mesmas referencias de memoria** que o orixinal.

A consecuencia de esto é que os cambios feitos nos obxectos mutables internos afectarán tanto ao obxecto orixinal como á copia.

```python
# creamos unha copia dunha lista
colores = [['azul', 'verde'], ['rojo', 'naranja']]
colores_copia = colores[:]
```

Eliminamos un elemento da lista orixinal:

```python
del colores[0]
print(colores)
print(colores_copia)
```

En este exemplo a lista copia non se ve modificada. Sen embargo, se eliminamos un elemento da lista copia, tamén se modifica a lista orixinal:

```python
del colores_copia[1][0]
print(colores)
print(colores_copia)
```

De maneira resumida, se modificamos o nivel superior só afecta á lista que modificamos, se modificamos os obxectos mutables anidados (cambiando un elemento dentro dunha sublista) afectamos a ambas listas porque comparten o mesmo obxecto interno.

Para evitar este comportamento podemos utilizar **Deep Copy**. Este é unha función quen os proporciona Python dentro do módulo `copy`.

```python
import copy

# creamos unha copia dunha lista
colores = [['azul', 'verde'], ['rojo', 'naranja']]
colores_copia = copy.deepcopy(colores)
colores_copia
```

Eliminamos un elemento da lista original

```python
del colores[0]
print(colores)
print(colores_copia)
```

Se eliminamos un elemento da lista contenida na copia nono se modifica la lista original

```python
del colores_copia[1][0]
print(colores)
print(colores_copia)
```
# Sets
Os **sets** ou **conxuntos** son secuencias de elementos que cumplen co seguinte:
- **Non están ordenados**, é decir, non soportan indexado.
- Cada elemento é único. **Non se permiten duplicados**.
- É **mutable**, pero os seus elementos teñen que ser de tipos **inmutables**.

Os seus usos habituales son:
- Claves de diccionarios
- Eliminacións de duplicados en coleccións
- Realización de opreacións de álgebra de conxuntos (unión, intersección, diferencia, complemento,...).

Ao ifual que o resto de coleccións, soporta o operador de pretenencia `in`, a función `len()` e o seu recorrido mediante bucles [[02 - Estructuras de control#Bucle `for-in`|for]].

Os sets podense construir das seguintes maneiras:
- Utilizando chaves `{}`, separando os elementos con comas: `{1, 2, 3}`
- Usando o constructor `set()` ou `set(iterable)`
- Por **compresión**: `{x for x in iterable}`

```python
var = set([1,2,34])
```

Máis creación de sets

```python
set_1 = {1}
set_2 = {2, 'a', (1, 4), True}
set_3 = set('ola')
set_4 = {x**2 for x in [1,2,1,2,1,1,2]}

print("set_1", set_1)
print("set_2", set_2)
print("set_3", set_3)
print("set_4", set_4)
```

Obter o número de elementos

```python
len(set_2)
```

Añadir elementos

```python
set_1.add(3)
set_1.add('ola')
set_1.add(3) # se é repetido (non o añade)
```

- `pop()` elimina un  elemento arbitrario e devolveo.

```python
s = {1, 2, 3}
item = s.pop()
print(item, s)
```

- `remove(x)` elimina o elemento _x_ e da error se non o encontra

```python
s = {1, 2, 3}
s.remove(2)
s
```

- `discard(x)` Elimina o elemento x. Non da error se non o encontra

```python
s = {1, 2, 3}
s.discard(5)
s
```
## Álgebra de conxuntos
| Operación                        | Resultado                                                       |
| -------------------------------- | --------------------------------------------------------------- |
| `x1.union(x2,...)`               | Unión dos sets (todos os elementos)                             |
| `x1.intersection(x2,..)`         | Intersección entre os sets (elementos en común)                 |
| `x1.difference(x2,...)`          | Elementos de x1 menos os de x2                                  |
| `x1.symmetric_difference(x2,..)` | Unión dos conxuntos menos a intersección (elementos non comúns) |
```python
x1 = {1, 2, 3}
x2 = {3, 6}

# union de 2 sets, as dúas formas producen a mesma salida
print(x1 | x2)
print(x1.union(x2))

# intersección entre os 2 sets, as dúas formas producen a mesma salida
print(x1 & x2)
print(x1.intersection(x2))

# diferencia entre 2 sets, as dúas formas producen a mesma salida
print(x1 - x2)
print(x1.difference(x2))

# diferencia simetrica entre 2 sets, as dúas formas producen a misma salida
print(x1 ^ x2)
print(x1.symmetric_difference(x2))
```
# Diccionarios
Os **diccionarios** son estructuras de datos do tipo **array asociativos**. Consisten en coleccións **non ordenadas** e **mutables** de **pares _clave:valor_**, onde cada clave referencia (indexa) un valor concreto.

O acceso aos diferentes valores almacenados no diccionario realizase a través da clave correspondente. As claves son **únicas** (non pode haber claves duplicadas) e deben ser dun tipo **inmutable** (tipos primitivos, strings, e tuplas, se non conteñen tipos mutables).

Sin embargo, non hai restriccións en canto ao tipo de datos dos valores. Ademáis, distintas claves poden ter valores de diferentes tipos. De igual modo, distintas claves poden ter o mesmo valor asociado.

Podemos construir diccionarios de diferente formas:
- Usando chaves para denotar un diccionario vacío: `{}`.
- Usando chaves, separando as parexas _clave:valor_ mediante comas: `{1: 'un', 2: 'dous'}`.
- Usando o constructor `dict()` ou `dict(iterable de pares)`.
- Usando **compresión**: `{k:v for k,v in iterable de pares}`.

```python
d1 = {}
d2 = {1:'un', 2:'dous', 'a':(1, 2, 3)}
d3 = dict([('un', 'one'), ('dous', 'two'), ('tres', 'three')])
d4 = {k:v for k,v in enumerate('ola')}

print(d1, "num elementos:", len(d1))
print(d2, "num elementos:", len(d2))
print(d3, "num elementos:", len(d3))
print(d4, "num elementos:", len(d4))
```

Se queremos engadir novas parexas _clave:valor_ ao diccionario usamos a sintaxis: `diccionario[clave] = valor`. No caso de que a clave xa exista, modificase o seu valor.

```python
d = {1: "jano", 2: "pancho"}

d[3] = "ola python"
```

Para acceder a un elemento utilizamos a seguinte sintaxis:

```python
print(d[1])
print(d.get(1))
```

Para **borrar** unha entrada do diccionario podemos utilizar a función `del d[x]` ou o método `pop(x)`,  donde `x` é unha **clave** do diccionario `d`. Se a clave non existe, producirase unha excepción `KeyError`.

```python
d = {n:n**2 for n in range(10)}
print(d)

del d[3]

d.pop(5)
```
## Unión de diccionarios
O método `update()` permite fusionar os contidos de dos diccionarios. Por exemplo, se o diccionario `d1` invoca o método `update()`: `d1.update(d2)` incorporará todas as entradas do diccionario `d2`. Se algunha das claves de `d2` xa se encontra en `d1`, esta vaise actualizar co valor de `d2`.

```python
d1 = {1:'un', 2:'dous', 3:'tresss'}
d2 = {4:'catro', 3:'tres'}
d1.update(d2)
d1
```
## Vistas
Os métodos `items()`, `keys()` e `values()` proporcionanos obxectos tipo vista moi útiles á hora de recorrer e acceder aos valores dos diccionarios.

- `items()` devolve as parexas _clave:valor_ contidas no diccionario.

```python
d = {1:'un', 2:'dous', 3:'tres'}
d.items()
```

- `keys()` devolve as **claves** contidas no diccionario.

```python
d = {1:'un', 2:'dous', 3:'tres'}
d.keys()
```

- `values()` devolve os **valores** contidos no diccionario.

```python
d = {1:'un', 2:'dous', 3:'tres'}
d.values()
```

