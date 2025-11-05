---
tags:
  - ia
  - machine_learning
---
# Machine Learning
O machine learning ou aprendizaxe automático basase en gran medida na **estadística** e **probabilidade**. Os métodos de machine learning apoyanse en técnicas estadísticas para analizar datos, comprendelos e configurar as súas propias reglas para emular o comportamento de un sistema. 

Cada paso nun proxecto de machine learning, desde a comprensión dos datos ata a interpretación dos resultados requere o uso de métodos estadísticos.

Un ejemplo claro do uso da estádistica no machine learning é o **Teorema de Bayes** e o **K Nearest Neighbors (KNN)**.
## Teorema de Bayes
O Teorema de Bayes é un sistema matemático que permite calcular a probabilidade de unha hipótesis (`h`) basándose en datos observados (`D`). Funciona de maneira inversa aos cálculos de probabilidad habituais. Conocendo as consecuencias, axuda a determinar a probabilidade das súas causas. 

No machine learning, o Teorema de Bayes, provee un marco probabilístico para o modelado predictivo, donde se busca maximizar a probabilidade de que un modelo se axuste a un conxunto de datos. Este concepto é coñecido como máximo a posteriori (MAP). 

Podemos representar o teorema coa seguinte formula:
$$P (h | D) = \frac {P (D | h) * P (h)}{P (D)}$$
### Algoritmos Naive Bayes
Os modelos de Naive Bayes son un tipo de algoritmos de aprendizaxe automático basados no teorema de Bayes. Seu nome "naive" (ingenuo) provén da suposición simplificada de que as variables de entrada son independentes entre sí.

As súas principais **ventaxas** son:
- É unha forma rápida e sinxela de predecir clases para problemas de clasificación binarios e multiclase.
- Cando a suposición de independencia é apropiada, o algoritmo comportase mellor que outros modelos de clasificación, incluso con menos datos de entrenamento.
- Axuda a resolver problemas de dimensionalidade ao permitir que cada distribución de características se estime de forma independiente.

Polo contrario, as súas **desventaxas** son:
- Aínda que son bos clasificadores, son coñecidos por ser estimadores deficientes, polo que as probabilidades que se obteñen non deben tomarse moi en serio.
- A suposición de independencia probablemente non reflicta a realidade de como son os datos no mundo real.
- Se o conxunto de datos de proba ten unha característica que non foi observada no conxunto de adestramento, o modelo asignaralle unha probabilidade de cero, o que fai inútiles as predicións.
### Exemplo Práctico
**Nun determinado grupo poboacional, a probabilidade de ter cáncer é do 0,02%. Doutra banda, existe unha proba para detectalo que non sempre é precisa. En caso de ter cáncer, lanza un resultado positivo o 85% das veces, e en caso de non ter cáncer, lanza un resultado negativo o 95% das veces. Calcular a probabilidade de ter cáncer se a proba da positivo.**

Para solucionar o problema empezamos definindo as probabilidades:
- $P(c)=0,0002$ : Probabilidad de que unha persoa teña cáncer.
- $P(!c)=0,9998$ : Probabilidad de que unha persoa non teña cáncer.
- $P(Pos|c)=0,85$ : Probabilidad de test positivo tendo cáncer.
- $P(Pos|!c)=0,05$ : Probabilidad de test positivo non tendo cáncer.
-  $P(N|c)=0,15$ : Probabilidad de test negativo tendo cáncer. 
- $P(N|!c)=0,95$ : Probabilidad de test negativo non tendo cáncer.

Ahora unha vez que temos calculados os resultados podemos aplicalos na seguinte formula:
$$P (c | Pos) = \frac {P (Pos| c) * P (c)}{P (Pos)} = P (c | Pos) = \frac {P (Pos| c) * P (c)}{(P(!c)*P(Pos|!c))+(P(c)*P(Pos|c))} $$

Entonces sustituimos os valores que calculamos ao principio e quedanos a formula seguinte:
$$P (c | P) = \frac {0,85 0,0002}{(0,9998*0,05)+(0,0002*0,85)} \approx 0.003389$$

> [!Note]- Tutorial de como resolver estos ejercicios.
> Para solucionar este tipo de problemas é bastante máis sencillo se realizamos un **esquema de árbol** como realiza no seguinte tutorial: [Teorema de Bayes | - YouTube](https://www.youtube.com/watch?v=Fi6G48j0IZ4) 
## K Nearest Neighbors (KNN)
O método **KNN** é un modelo de aprendizaxe automática supervisada que se distingue por ser moi sinxelo pero á vez efectivo. Utilízase comunmente en problemas de **clasificación**.


