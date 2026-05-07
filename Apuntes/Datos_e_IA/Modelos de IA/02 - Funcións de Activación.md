---
tags:
  - ia
  - machine_learning
  - deep_learning
---
As **funcións de activación** son compoñentes críticos nas redes neuronales. A súa función principal é introducir **non-linealidade** no modelo, permitindo que a rede aprenda e realice tareas compexas que van máis alá dunha simple [[01 - Tipos de algoritmos no aprendizaxe automático#Regresión Lineal]].

# Tipos de funcións de activación
## Sigmoide (Lógistica)
É a función clásica que imita o disparo dunha neurona biológica. Comprime calquer valor ao intervalo **(0, 1)**. Históricamente foi moi popular, pero ten un defecto: cando os valores son moi altos ou baixos a curva volvese plana e a rede deixa de aprender (problema do gradiente desvaneciente)
### Casos de uso:
- Capa de salida para a **clasificación binaria**.
- Modelos onde necesitas unha probabilidade (0 a 100%).
- Redes neuronales moi pouco profundas.
## Tanh
É unha versión mellorada da Sigmoide. Ao estar centrada en cero (rango de -1 a 1), axuda a que os datos de cada capa teñan unha media cercana a cero, o que facilita e acelera enormemente o entrenamento. Sen embargo, sigue sufrindo do mesmo problema de saturación en valores extremos.
### Casos de uso:
- Capas ocultas en redes de tamaño medio.
- Moi común en Redes Neuronales Recurrentes (RNN).
- Cando os datos de entrada teñen valores negativos importantes.
## ReLu
É o estándar da industria hoxe en día. Súa lóxica é simple: "se é negativo, apagao (0); se é positivo, deixao pasar". Esta simplicidade matemática fai que as redes profundas se entrenen moito máis rápido. Crea unha rede "dispersa", onde non todas as neuronas traballan á vez.
### Casos de uso:
- Case sempre en capas ocultas.
- Visión artificial e procesamento de lenguaje (Transformers).
- Cando buscas eficiencia e velocidade de cómputo.
## Leaky ReLu
Soluciona o problema das "neuronas mortas" en ReLu permitindo unha pendente moi pequena para os valores negativos. Esto asegura que todas as neuronas manteñan unha pequena posibilidade de seguir aprendendo incluso se súa entrada é negativa.
### Casos de uso:
- Se túa rede sufre do problema de neuronas que deixan de activarse.
- Arquitecturas complexas como as GANs.
- Para exprimir o máximo rendemento no entrenamento.
## Softmax
Toma as puntuacións finales da rede e normalizaas para que parezcan probabilidades que suman exactamente 1.0 (100%). É indispensable para problemas onde o sistema debe elegir unha sola opción entre varias posibles.
### Casos de uso:
- Capa final de clasificación múltiple.
- Casos onde as categorías sean excluintes.
- Motores de recomendación.