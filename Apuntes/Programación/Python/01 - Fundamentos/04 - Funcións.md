---
tags:
  - python/fundamentos
---
# Funcións
Python permitenos crear as nosas propias funcións que se declaran coa cláusula `def` e todas terán:
- un **nombre**.
- **parámetros**: (dende 0 a N), van encerrados entre paréntesis.
- un **docstring**: esto é opcional, en el incluese unha descripción da función, os seus parámetros e o seu retorno.
- un **corpo**: as accións da función.
- cláusula `return`: (0 ou máis) para devolver un valor, se non existe a función devolve o valor `None`.

Estas estructuras son a base da **programación modular**, que se cimenta sobre dous conceptos clave: **abstracción** e **descomposición**.

- **Abstracción**: as funcións actúan como caixas negras ás que lle proporcionamos uns datos de entrada (os argumentos). Todos os detalles da súa implementación, e funcionamento interno, queda oculto.
- **Descomposición**: o empleo de funcións permitenos a división de problemas complexos en tarefas máis simples e abordables computacionalmente.

Polo xeral, estas funcionalidades:
- Son **autocontenidas**, é decir, representan tarefas ben definidas que a función pode resolver (se dispón dos datos necesarios).
- Permiten a **división** do código, facilitando a súa **organización** e **mantenimiento**.
- Son **reutilizables**, incluso 
- Facilitan o **traballo en equipo** xa que permiten repartir mellor a carga de traballo entre diferentes programadores.

```python
def es_par(i):
    """Comproba se un número é par.
    Args:
        i (int): número entero.
    Returns:
        (bool): True se é par.
    """
    if i%2 == 0:
        par = True
    else:
        par = False

    return par
```
## Invocación
O código dunha función, é decir, o corpo, só se ejecutará cando chamemos á función dende algún punto do programa. A función ten que ser definida antes de ser invocada.

```python
# Inicio do programa
x = int(input('Número? '))

# invocación da función es_par() previamente definida
par = es_par(x)

if par:
    print('Par')
else:
    print('Impar')
```
## Retorno
A cláusula `return` utilizase para devolver o control do programa ao punto dende o que se chamou á función, e devolver un **valor de retorno** que poderá ser utilizado.

Ainda que unha función poida ter varias cláusulas de `return`, só se ejecutará unha e o valor devolto pode ser o resultado de calquer expresión, incluido chamadas a outras funcións.

Unha das características de Python é que as funcións poden **devolver máis de un valor**.

```python
def min_max(vals):
    """Devolve o máximo e o mínimo dunha lista de valores.
    Args:
        vals (List): lista de valores.
    Returns:
        (float, float): Mínimo e máximo.
    """

    vals.sort()

    # devuelve varios valores separados por comas (tupla)
    return vals[0], vals[-1]
```
# Ámbitos das variables
É importante comprender que as variables que utilizamos como argumento na definición da función (**formal parameters**), e que **sólo** son visibles no corpo da mesma, son **independientes** das variables empleadas como argumento na invocación (**actual parameters**).

```python
def f( x ):
    """
    Args:
        x: formal parameter
    """
    x = x + 1
    print("en f(x): x =", x)
    return x

x = 3
z = f(x) # x é un <<actual parameter>>

print("x =",x,"; z =",z)
```

Unha característica de Python é que, dentro da función, podese acceder ás variables definidas fora, pois son consideradas **globales**, pero, en principio non se poden modificar. Se necesitamos modificar unha variable externa de **ámbito global** desde unha función, debemos declararla dentro da función mediante a cláusula `global`.

```python
def f():
    # declaramos a variable x como global
    global x
    x = x + 1

x = 5
f()
print(x)
```

Ainda que o lenguaje nos permite, non deberíamos facer uso de esta facilidade polo general xa que de esta forma estamos limitando a independencia da función (autocontención).
# Argumentos
As funcións poden ter o número de parámetros formales que necesitemos. Na invocación da función debemos proporcionar os suficientes valores para todos eles.

```python
# Especificación dunha función
def autor(nom, apel, f_nac):
    pass

# Ejemplo de chamada
autor("Pancho", "Perro", "06/11/1999")
```

Podemos alterar o orden dos argumentos na invocación da función, se empleamos parexas `clave=valor` (para todos os parámetros).

```python
def autor(nom, apel, f_nac):
    pass

# Ejemplo de chamada
autor(f_nac="06/11/1999", apel="Perro", nom="Pancho")
```

Tamén podemos establecer **valores por defecto** para os parámetros da función. Para eso, asignaselles un valor na definición e podrán ser omitidos na invocación. Se hai parámetros obligatorios e opcionales, estos últimos deben ir ao final.

```python
def autor(nom, apel, f_nac, activo="s", mascota=None):
    pass

autor("Pancho", "Perro", "06/11/1999")  # usarase o valor "s" para activo (por defecto)
autor("Jano", "Antelo", "06/11/1999", activo="n") # usarase o valor "n" para activo
```
## Número variable de argumentos
Python tamén nos permite definir funcións que acepten un **número variable** de argumentos. Para eso, usaremos os parámetros especiales `*args` e `**kwargs` (estos son nomes arbitrarios ainda que se soen usar estos por convención).
### `args`
Crearase unha función dunha **tupla** do nombre `args` (ou o nombre que se escollese) e a lonxitude variable que recollerá os parámetros pasados. Os argumentos pasados na chamada poden ser de diferente tipo.

```python
def sumatorio(*nums):
    print("sumar:",nums,type(nums))

    suma = 0
    for n in nums:
        suma += n
    return suma

print("a suma é", sumatorio(1, 2, 3))
print("a suma é", sumatorio(15, 10, -10, 5))
```
### `kwargs` (key-word arguments)
Neste caso, crearase un diccionario do nome `kwargs` e de lonxitude variable que recollerá os parámetros pasados como parexas `nome=valor` (diccionario). Os argumentos pasados na chamada poden ser de calquer tipo.

```python

```
