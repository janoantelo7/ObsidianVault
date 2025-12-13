---
tags:
  - machine_learning
---
# Introducción
Existen principalmente, tres tipos de aprendizaxe automático: supervisado, non supervisado e por reforzo. Estos son os tres grandes paradigmas do [[Apuntes/Intelixencia Artificial/Sistemas de Aprendizaxe Automática/00 - Introducción#Machine Learning|machine learning]]. A principal diferenza entre eles radica en que tipo de información recibe o modelo durante o entrenamento e cómo aprende.
## Aprendizaxe supervisado
Este tipo de aprendizaxe básase en entrenar un modelo utilizando **datos etiquetados**, é decir, exemplos de entrada acompañados coa resposta correcta. 
### Como aprende
O algoritmo compara as súas prediccións coas etiquetas reales e axusta os seus parámetros para minimizar o error.
### Problemas que resolve
Este tipo de aprendizaxe resolve os seguintes problemas:
- **Clasificación**: predecir unha categoría discreta.
- **Regresión**: predecir un valor numérico continuo.
#### Exemplos
- Detectar se un correo é _spam_ ou _non spam_.
- Predecir o precio dunha vivienda.
- Recoñecemento de imáxes con etiquetas (can, gato, etc.)

As ventajas que presenta son:
- Alta precisión cando hai datos de calidade.
- Resultados fáciles de evaular.

As desventajas que presenta son:
- Require grandes volúmes de datos etiquetados.
- O etiquetado pode ser costoso e lento.
## Aprendizaxe non supervisado
No aprendizaxe non supervisado o modelo traballa con **datos sen etiqueta**, buscando patrons, estructuras ou relacións ocultas.
### Como aprende
Identificando similutides, agrupacións ou distribucións estadísticas sen unha "resposta correcta" predefinida.
### Problemas que resolve
- Clustering (agrupamento).
- Reducción de dimensionalidade.
- Detección de anomalías.
#### Exemplos
- Segmentar os clientes según seu comportamento.
- Agrupar noticias por temática.
- Detectar transaccións financieiras atípicas.

As ventajas que presenta son:
- Non requiere datos etiquetados.
- Útil para a exploración e descubrimento de patróns.

As desventajas que presenta son:
- Resultados máis difíciles de interpretar.
- Non existe unha métrica clara de "resposta correcta".
## Aprendizaxe por reforzo
O aprendizaxe por reforzo basase en que un **axente** aprende a tomar decisións interactuando cun **entorno**, recibindo **recompensas** ou **castigos** según súas accións.
### Como aprende
O axente proba accións, observa as consecuencias e axusta súa estratexia para **maximizar a recompensa acumulada a largo plazo**.
#### Exemplos
- Xogos (ajedrez, go, videoxogos).
- Robots que aprenden a camiñar.
- Sistemas de recomendación adaptativos.
- Control de tráfico ou logística.

As ventajas que presenta son:
- Ideal para problemas secuenciales e dinámicos.
- Aprende estrategias complejas sen datos etiquetados.

As desventajas que presenta son:
- Entrenamento costoso en tempo e recursos.
- Pode requerir _guaranteeing_ nun entorno de simulación, é decir, que o aprendizaxe sea controlado, estable e cumpla certas reglas para que o axente poida aprender sen riscos.
# Tipos de algoritmos
## Regresión Lineal
A regresión lineal é un método estadístico que busca modelar a realación entre unha variable dependente (o que queremos predecir) e unha ou máis variables independentes (os datos que temos).

É un algoritmo de aprendizaxe supervisado, o que significa que necesitamos datos etiquetados (datos históricos coa resposta correcta) para entrenar o modelo. O obxectivo principal é encontrar unha línea recta (ou un plano, en dimensións superiores) que pase o máis cerca posible de todos os puntos dos teus datos.

Nos casos máis simples solemos representalo coa seguinte formula:
$$y = {m}\times{x} + {b}$$
Onde $x$ representa a variable independiente (os datos de entrada), mentres que $y$ representa a variable dependiente (valor de salida). 

$m$ representa a **pendiente** ou a inclinación da recta. En machine learning, esto representa o **peso** e $b$ representa o **sesgo**.
