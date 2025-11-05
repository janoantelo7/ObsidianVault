---
tags:
  - python/fundamentos
---
# Listas
As **listas** son tipo de dato que nos permiten crear coleccións de datos. As súas principales características son: 
- **Mutabilidade:** as listas son mutables, o que significa que podes agregar, eliminar ou modificar elementos despois de creala.
- **Sintaxis:** as listas definense mediante corchetes “[]”.
- Son máis lentas que as tuplas para coleccions de grandes datos.
## Crear unha lista
Definición de unha lista
```python
lista = [1,2,3]

print(lista)
```
## Añadir elementos á lista
Añadir elementos na lista
```python
lista = [1,2,3]
lista.append(4)

print(lista)
```
## Modificar a lista
Modificar elementos na lista
```python
lista = [1,2,3]
lista[0] = 10

print(lista)
```
## Eliminar elementos da lista
Para eliminar un elemento da lista podemos facelo de dúas maneiras
```python
### método 1 ###
lista = [1,2,3]
lista.remove(3) #esto elimina a primeira aparición de ese elemento

print(lista)

### método 2 ###
lista = [1,2,3]
lista.pop(2) #esto elimina o elemento na posición indicada

print(lista)
```

# Tuplas
as **tuplas** son outro tipo de dato que nos permiten crear coleccións de datos. As súas principales características son:
- **Inmutabilidade:** as tuplas son inmutables, esto quere decir que unha vez creas unha tupla non podes modificar o seu contido.
- **Sintaxis:** as tuplas definense mediante paréntesis “()”.
- Gracias a ser inmutables, as tuplas son máis rápidas e ocupan menos memoria que as listas.
## Creación de unha tupla
 No siguiente ejemplo vemos como se definie unha tupla
 ```python
tupla = (1,2,3)

print(tupla) 
```

# Sets
Os **sets** son unha colección de elementos únicos e desordenados. As súas principales características son:
- **Elementos únicos**: Os sets non permiten elementos duplicados.
- **Desordenados**: Os sets non teñen un orden definido, o que significa que non podes acceder aos elementos por índice como nunha lista.
- **Mutable**: Os sets son mutables, o que significa que podes agregar ou eliminar elementos de eles.
## Creación de un set
Creación de un set. Á hora de crear un set podemos utilizar a función `set()` se queremos definir un set vacío ou utilizar chaves `{}` para crear un set con valores.
```python
# creación de un set vacío
meu_set = set()

# creación de set con valores
set_valores = {1,2,3,4,4} 
print(set_valores) # Output: {1, 2, 3, 4}
```
## Agregar elementos
Para añadir elementos en un set utilizamos o método `add()`:
```python
meu_set = {1,2,3,4,4} 
meu_set.add(5)

print(meu_set) # Output: {1, 2, 3, 4, 5}
```
## Eliminar elementos
Hai varias formas de eliminar elementos nun set:
- `remove()`: Elimina un elemento específico. Se o elemento non existe, lanza un error.
- `discard()`: Elimina un elemento específico. Non lanza error se un elemento non existe.
- `pop()`: Elimina e devolve un elemento arbitrario do set (xa que os sets ao ser desordenados non sabes cal vai eliminar).
- `clear()`: Elimina todos os elementos do set.
```python
meu_set = {1,2,3,4,5} 
meu_set.remove(1)
meu_set.discard(4)
print(meu_set) # Output: {2, 3, 5}

meu_set.pop()
print(meu_set) # Output: {3, 5}

meu_set.clear()
print(meu_set) # Output: set()
```
## Comprobar existencia
Podemos verificar se un elemento está dentro do set, utilizando a palabra clave `in`. Devolve `True` se o elemento está no set e `False` se non está no set.
```python
meu_set = {1,2,3,4,5} 
print(3 in meu_set) # Output: True
print(10 in meu_set) # Output: False
```
# Diccionarios
Un **diccionario** é un conxunto de valores emparexados. Un diccionario é parecido a unha lista, pero os índices non teñen porque ser númericos. O diccionario definese utilizando chaves (`{}`). No seguinte exemplo podemos ver como se define un diccionario. As claves de un diccionario non poden repetirse, no caso de repetirse a última sobreescribirá á primeira.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

print(diccionario)
```
## Acceder aos elementos
Podemos acceder ao valor de cada elemento do diccionario seleccionando a clave da seguinte maneira:
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

print(diccionario["animal"]) # Mostrará "gato"
```
## Actualizar os elementos
Para actualizar os elementos de un diccionario podemos facelo da seguinte maneira que é seleccionando o elemento e asignandolle o novo valor. Esta maneira é útil cando se quere actualizar un só valor do diccionario.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

print(diccionario) # Imprime o diccionario antes de modificalo: {'animal': 'gato', 'cousa': 'pedra', 3: 'número'}

diccionario["animal"] = "can"

print(diccionario) # Imprime o diccionario modificado: {'animal': 'can', 'cousa': 'pedra', 3: 'número'}
```

Se queremos actualizar varios valores de un diccionario podemos utilizar o método `update()`. A este método debemos pasarlle un argumento en formato diccionario. Se non existe a clave que queremos modificar no diccionario añadirá esa clave co valor pasado no diccionario.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

print(diccionario) # Imprime o diccionario antes de modificalo: {'animal': 'gato', 'cousa': 'pedra', 3: 'número'}

diccionario.update({"animal": "can", "cousa": "mando"})

print(diccionario) # Imprime o diccionario modificado: {'animal': 'can', 'cousa': 'mando', 3: 'número'}
```
## Añadir elementos
Se queremos añadir elementos a un diccionario é tan sencillo como chamar ao diccionario con unha nova clave e asignandolle un novo valor. Tamén o podemos facer co método anteriormente mencionado `update()`.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

diccionario["color"] = "verde"

print(diccionario) # Imprime o diccionario co novo valor: {'animal': 'gato', 'cousa': 'pedra', 3: 'número', 'color': 'verde'}
```

Se queremos facelo co método `update()` faríase da seguinte maneria mandandolle a clave e o valor como argumento:
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

diccionario.update({"color":"rojo"})

print(diccionario) # Imprime o diccionario co novo valor: {'animal': 'gato', 'cousa': 'pedra', 3: 'número', 'color': 'rojo'}
```
## Eliminar elementos
Podemos eliminar os elementos de varias maneiras de un diccionario depenendo do que queiramos eliminar.  Se queremos eliminar un só elemento de un diccionario podemos facelo co método `pop()`.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

diccionario.pop("animal")

print(diccionario) # Imprime o diccionario sin o elemento "aniaml": {'cousa': 'pedra', 3: 'número'}
```

Outra maneira de eliminar un elemento de un diccionario é coa palabra clave `del`. Se utilizamos `del` sin indicar a clave que queremos eliminar o que fará será eliminar o diccionario.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

del diccionario["animal"]

print(diccionario) # Imprime o diccionairo sin o elemento "animal": {'cousa': 'pedra', 3: 'número'}
```

```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

del diccionario

print(diccionario) # Esto da o seguinte error: "NameError: name 'diccionario' is not defined"
```

Podemos eliminar o último elemento de un diccionario co método `popitem()`.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

diccionario.popitem()

print(diccionario) # Imprime o diccionario sin o último elemento: {'animal': 'gato', 'cousa': 'pedra'}
```

Por último, podemos utilizar o método `clear()` para vaciar o diccionario e crear un diccionario vacío.
```python
diccionario = {
    "animal": "gato",
    "cousa": "pedra",
    3: "número"
}

diccionario.clear()

print(diccionario) # Imprime o diccionario vacío: {}
```
