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
### Cando usala?
- Capa de salida para a **clasificación binaria**
- Modelos onde necesitas unha probabilidade (0 a 100%).
- Redes neuronales moi pouco profundas.
