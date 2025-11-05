---
tags:
  - python
---
# Introducción
Pandas é unha librería de Python utilizada para a manipulación e análise de datos. Ofrece estruturas de datos fáciles de usar, como DataFrames, que permiten traballar con datos tabulares de forma eficiente. Con Pandas, podes ler e escribir datos desde diversos formatos, limpar e transformar datos, realizar análises estatísticas e moito máis, facilitando así o traballo con grandes volumes de información. Para instalar pandas facemolo ao igual que outras librerías de python através de [[01 - Datos e operadores#Pip|pip]].
```bash
pip install pandas
```
# Importar pandas
Normalmente importamos pandas co alias “pd”.
```python
import pandas as pd

dataset = {
  'marcas': ["BMW", "Volvo", "Ford"],
  'ventas': [3, 7, 2]
}

coches = pd.DataFrame(dataset)

print(coches)
```
# Series e Dataframes
## Series
As series en pandas son unha columna de un dataframe. Podemos definir unha serie da seguinte maneira con un [[01 - Datos e operadores#Diccionarios|diccionario]].
```python
import pandas as pd 

calorias = { "desayuno": 400, "comida": 700, "cena": 260}

ingesta = pd.Series(calorias)

print(ingesta)
```

Podemos tamén crear una serie a partir dunha [[01 - Datos e operadores#Listas|lista]] pero de esta maneira debemos indicar o índice nos á man. Se non indicamos o índice as filas non terán nombre.
```python
import pandas as pd 

calorias =  [400, 700, 260]

ingesta = pd.Series(calorias, index = ["desayuno", "comida", "cena"])

print(ingesta)
```
## Dataframes
Un dataframe é unha estructura bidimensional de datos, como un array de dúas dimensións, ou unha tabla con columnas e filas.
```python
import pandas as pd 

datos =  {
    "calorias": [ 420, 700, 250],
    "comida": ["galletas", "kebab", "arroz e atún"]
}

df = pd.DataFrame(datos)

print(df)
```

Podemos crear os nosos índices para as columnas
```python
import pandas as pd 

datos =  {
    "calorias": [ 420, 700, 250],
    "comida": ["galletas", "kebab", "arroz e atún"]
}

df = pd.DataFrame(datos, index= ["desayuno", "comida", "cena"])

print(df)
```
