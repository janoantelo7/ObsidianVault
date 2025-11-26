---
tags:
  - python/data_science
  - ia
---
NumPy é unha librería de código libre que proporciona soporte para a creación de **vectores** e **matrices** multidimensionales de gran tamaño, xunto coa gran colección de funcións matemáticas de alto nivel para operar con estas estructuras. 

NumPy é o estándar actual para o traballo con datos numéricos en Python. Súa API usase de forma masiva en outras librerías como Pandas, SciPy, Matplotlib, scikit-learn, scikit-image e a mayoría do resto de paquetes científicos de Python.
# Instalación de NumPy
Podemos instalar NumPy desde o repositorio oficial de Python.

```shell
pip install numpy
```
# Importar NumPy
Unha vez instalado, deberemos importar NumPy para acceder as súas funcións dese noso código Python. É unha convención ampliamente adoptada emplear o alias **np** para facer o código máis lexible para calquera que traballe con el.

```python
import numpy as np
# podemos comprobar a versión de numpy con
np.__version__
```
# Arrays de NumPy
O array é a estructura de datos central da librería NumPy. Básicamente é un vector multidimensional que contén información acerca dos valores, cómo localizar un elemento e cómo interpretalo. Todos os elementos do array son do **mesmo tipo**, que podemos obter mediante súa propiedade `dtype`.

Existen diferentes formas de **indexar** os elementos do array: por enteiros, por unha tupla de enteiros non negativos, por outro array ou por booleanos. O **rango** do array é seu número de dimensións ou **ejes**. A propiedade `shape` é unha tupla de enteiros cos tamaños de cada unha das súas dimensións.

Podemos **inicializar** estos arrays a partir de [[03 - Tipos estructurados#Listas|listas]]  de Python, usando listas anidadas de 2 ou máis dimensións. Como veremos, dispoñemos tamén de toda unha serie de funcións que nos permiten cargar arrays inicializados a cero, uno, valores aleatorios ou rangos de valores.

```python
# inicializando un array a partir de unha lista
a = np.array([1, 2, 3, 4, 5, 6])
```

```python
# dimensions
a.shape
```

```python
# tipo de datos
print(a.dtype)
```

```python
# array de dúas dimensions (matriz)
a = np.array([[1, 2, 3, 4], [5, 6, 7 , 8], [9, 10, 11, 12]])

# dimensions
print(f'Dimensions (F,C): {a.shape}')

# valores
print(f'Valores: \n{a}')
```
## Indexado de elementos
Para acceder a algún dos elementos do array, usaremos corchetes `[]`. O primeiro elemento ten índice `0`.

```python
# array dunha dimensión
a = np.array([1, 2, 3, 4, 5, 6])

# cada elemento é un valor númerico
a[2]
```

```python
# array de 2 dimensións
a = np.array([[1, 2, 3, 4], [5, 6, 7 , 8], [9, 10, 11, 12]])

# cada elemento será un array de unha dimensión
print(f'Matriz:\n{a}')
print(f'Última fila: {a[2]}')
print(f'Dimensions da última fila: {a[2].shape}')

# indexado dun elemento da fila
print("O elemento da última fila e primera columna é: a[2][0] = ", a[2][0])
print("Tamén o podemos indexar así: a[2,0] = ", a[2,0])
```
## Por qué arrays de NumPy en lugar de listas de Python?
Os arrays de NumPy proporcionanos mecanismos **máis rápidos e eficientes** para a creación e manipulación de conxuntos de datos numéricos. Mentras que as listas de Python poden conter diferentes tipos de datos na mesma lista, todos os elementos dun array de NumPy deben ser do mesmo tipo, o que fai que as operacións matemáticas sobre eles sexan máis eficientes.

Por outro lado, as estructuras internas do almacenamento que dan soporte aos arrays de NumPy consumen moita menos memoria.
## Terminología
En numerosas ocasións encontraremonos na literatura términos como vector, matriz, tensor... Para referirse a estas estructuras de datos.

Suelese emplear o término **vector** para arrays 1-D ou dunha dimensión (non hai diferencia entre fila ou columna). Unha **matriz** é un array 2-D ou de dúas dimensións.

En programación e _machine learning_, usase o término **tensor** para representar estructuras de datos n-dimensionales, optimizadas para cálculos matemáticos intensivos. Podemos facer as seguintes equivalencias según a dimensionalidade:

- Un **escalar** é un tensor de **orden 0**
- Un **vector** é un tensor de **orden 1**
- Unha **matriz** é un tensor de **orden 2**

En calquer caso, en NumPy utilizase internamente a clase `ndarray` para representar calquer array multidimensional, homoxeneo e dun número fijo de elementos. Estos arrays creanse usando funcións como `array`, `zeros`, `empty`.

```python
# vector inicializado con valores
v = np.array([1,2,3,4])
print(f'v shape = {v.shape}')
print(v)

# matriz 3x4 inicializada a ceros
m = np.zeros([3, 4])
print(f'\nm shape = {m.shape}')
print(m)

# tensor 4x2x3 con valores indeterminados
t = np.empty([4, 2, 3])
print(f'\nt shape = {t.shape}')
print(t)
```


