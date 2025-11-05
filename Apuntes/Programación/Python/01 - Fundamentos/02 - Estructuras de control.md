---
tags:
  - python/fundamentos
---
 As **sentencias de control do flujo de execución** dos nosos programas permiten, baixo determinadas **condicións**, **alterar a execución secuencial** das **instrucións** dos nosos programas.

Python proporciona diversas instruccións para controlar flujo de ejecución:
- Sentencias condicionales (`if`): Permiten tomar decisións en base aos datos ou resultados de operacións, e en función de estos, executar certas sentencias ou non.
- Sentencias iterativas (`for`, `while`): Permiten repetir a execución dunha serie de instruccións mentres se cumplan determinadas condicións. Esta estructura de control conocese como **bucle**.
# Estructuras concicionales
## Estructura `if`
Podemos empregar a instrucción `if` para evaluar unha condición, e en caso de que sexa certa executar as sentencias. O seu formato é:

```python
if condicion:
	sentencia1
	sentencia2
```

Para a construcción da condición podemos empregar os [[01 - Datos e operadores#Valores lóxicos|valores lóxicos]]. Se o resultado de evaluar a expresión construida é **True**, executaranse as sentencias dentro do bloque de instruccións. 
## Estructura `if-else`
En situacións nas que desexamos realizar determinadas accións en caso de que se verifique unha condición, e outras accións diferentes, en caso contrario. Para estas situacións en Python utilizamos a estructura `if-else`. O seu formato é o seguinte:

```python
if condición:
	código_se_condición_True
else:
	código_se_condición_False
```
## Condicionales anidados
Poden darse casos no que necesitemos condicionales dentro de outros, esto chamanse condicionales anidados. Teñen a seguinte estructura, por exemplo:

```python
if condición_1 :
   # Executase sea condición_1 é True
   bloque_1
else :
   # Executase se condición_1 é False
   if condición_2 :
       # Executase se condición_2 é True
       bloque_2
   else :
       # Executase se ambas condiciones son False
       bloque_3
```

En Python podemos utilizar outra construcción máis elegante de facer algo similar que sería coa sentencia `elif`:

```python
   if condición_1 :
        # Executase si condición_1 é True
        bloque 1
    elif condición_2 :
        # Executase si as condiciones anteriores son False e condición_2 é True
        bloque 2
    elif condición_3 :
        # Executase si as condiciones anteriores son False e condición_3 é True
        bloque 3
    else :
        # Executase si todas as condiciones anteriores son False
        bloque 4
```
## Construcción `if-else` en línea (operador ternario)
A diferencia de outros linguaxes como C++ e Java, Python non ten un operador condicional ternario (`?:`). Sen embargo, podemos crear unha estructura de decisión `if-else` nunha única línea dandonos un resultado similar. A súa sintaxis é a seguinte:

```python
valor_True if condición else valor_False
```

Se a condición se cumple a expresión devolverá o valor de `valor_True`, en caso, devolverá `valor_False`. Vese máis claro en este exemplo:

```python
edad = 10
"""
if edad >= 18:
    mayor_de_edad = 'Sí'
else:
    mayor_de_edad = 'No'
"""

mayor_de_edad = 'Sí' if edad >= 18 else 'No'

print(mayor_de_edad)
```
# Estructuras iterativas
Este tipo de estructuras permiten repetir a execución dunha serie de instruccións mentras se cumpla unha determinada condición. Esta estructura conocese tamén como **bucle**.
## Bucle `while`
Os bucles `while` son os tipos máis simples destas estructuras. En eles podese establecer unha condición e, mentres esa condición se cumpla o bloque de instruccións dentro do bucle `while` continuará ejecutándose. O seu formato é o seguinte:

```python
while condición:
	accion1
	accion2
```

- `condición`: Será calquer expresión evaluable que devolva un valor booleano (`True` ou `False`).
## Bucle `for-in`
Python dispón de outro tipo de bucle, o bucle `for-in`. Este tipo de bucle suele emplearse cando conocemos de anteman o número exacto de iteraccións que queremos realizar ou ben, cando queremos recorrer secuencialmente unha serie de elementos ou valores. O seu formato é o seguinte:

```python
 for variable in serie_de_valores:
      acción_1
      acción_2
```

- En cada **interacción** do bucle, a `variable` irá tomando un dos valores da `serie_de_valores`. Habrá que tantas interaccións como valores na serie.
- Polo xeral, a sentencia `for` vainos permitir recorrer calquer tipo de obxeto secuenciable, é decir, obxetos que nos permiten acceder de forma secuencial a cada un dos seus elementos. obxetos de este tipo son as cadenas de carácteres, as listas, as tuplas...
### Función `range`
A función `range` é un tipo de secuencia inmutable que nos permite generar unha secuencia de valores entre uns límites. Ten o seguinte formato: 

```python
range([inicio],final, [paso])
```

- `inicio`: (por defecto utiliza, 0) é o valor inicial do generador. Este parámetro é opcional.
- `final`: é o valor final (**non incluido**) do generador.
- `paso`: (por defecto, 1) pasa o salto entre os valores generados. Este parámetro é opcional.
### Función `enumerate`
A función `enumerate` devolve un iterador tal que cada chamada ao seu método `__next__()` retorna unha tupla coa posición (índice) e o valor do seguinte elemento iterable. O seu formato é o seguinte:

```python
enumerate(iterable, start=0)
```

- `iterable`: será unha secuencia ou obxeto que soporte a iteracción.
- `start`: parámetro opcional para indicar o valor do índice para o primeiro elemento da secuencia (por defecto, 0).

```python
estaciones = ['Primavera', 'Verano', 'Otoño', 'Invierno']
enum = enumerate(estaciones)

enum.__next__()
# devolve: (0, 'Primavera')

enum.__next__()
# devolve: (1, 'Verano')
```

Soe utilizarse en conxunto coa función `for` en casos onde ao mesmo tempo que recorremos os elementos de un obxeto iterable, necesitamos a posición:

```python
# Extrae o valor e posición do número máis grande da lista
lista_num = [5, -2, 10, 11, 18, -2, 21, 4, 12]
max_pos = 0
max_num = lista_num[0]

for i, num in enumerate(lista_num):
    if max_num < num:
        max_num = num
        max_pos = i

print(f'O máximo é {max_num} e está en la posición {max_pos}')
```
## `break`, `continue` e `pass`
En algúnha ocasión pode que necesitemos alterar a execución normal dentro do bucle ou abandonalo. Para eso contamos coas sentencias `break` e `continue`. 
### `break`
A sentencia `break` forza a salida do bucle no que nos encontramos:

```python
while True:
  val = input("Pulsa [X] para terminar:").upper()
  if val == 'X':
    break
```

En caso de anidamento, `break` forzará só a salida do bucle no que se encontre.

```python
print('Os números primos entre 100 e 200 son:')

for numero in range(100, 201):
    primo = True
    for divisor in range(2, numero):
        if numero % divisor == 0:
            # no é primo -> saltar ao siguiente
            primo = False
            break # salimos do bucle interno

    # si o número actual é primo, imprimimolo
    if primo:
        print(numero, end=' ')
```
### `continue`
A sentencia `continue`, provoca que se salte ao inicio da siguiente interacción do bucle sin executar o resto de instruccións. É decir, non salimos do bucle como con [[#`break`|break]], senon que saltamos ao inicio do mesmo bucle (e se se cumple a condición executase a siguiente interacción).

```python
# Imprime os números impares entre 1 e 10
print('Números impares menores que 10: ', end='')
for num in range(1, 11):
    if num % 2 == 0:
        continue
    print(num, end=' ')
```
### `pass`
A sentencia `pass` representa unha opreación nula, é decir, non executa nada. Se ben pode parecer absurda a súa existencia é común vela en fases iniciais dun desarrollo no que temos a estructura do código pero ainda non temos implementada determinada funcionalidade.

```python
def fun(val):
    pass

# recorro o bucle
lista_num = [5, -2, 10, 11, 18, -2, 21, 4, 12]

for valor in lista_num:
    # a función fun de momento no fai nada
    fun(valor)
```
