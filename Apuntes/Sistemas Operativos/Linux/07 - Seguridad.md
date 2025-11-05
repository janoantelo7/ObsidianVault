---
tags:
  - linux
---
Á hora de administrar servidores en Linux temos diversas ferramentas para poder securizar os nosos servidores.
# Firewalld
**Firewalld** é unha ferramenta de gestión de cortafuegos dinámica. Súa función principal é controlar o tráfico da rede permitindo ou bloqueando conexións en funcións de reglas. A diferencia de outros cortafuegos, Firewalld utiliza "zonas" para controlar o tráfico.
## Zonas
Unha zona de rede define o nivel de confianza da conexión de rede. Eso é unha relación de un a moitos, que significa que a conexión pode ser parte de unha zona, pero unha zona pode ser utilizada por moitas conexións.
### Crear zonas
Podemos definir as nosas zonas personalizadas co seguinte comando. É importante saber que para que a zona se aplique debemos facer ese cambio permanente.
```bash
firewall-cmd --permanent --new-zone=nombre-de-zona
```

Unha vez creada a zona personalizada podemos filtrar o tráfico de distintas maneiras.
- Engadir a interfaz á zona: Cando queremos que todo o tráfico que entre por esa interfaz se lle apliquen as reglas da zona.
- Engadir a IP específica: Esto sirvenos para permitir que unha IP concreta teña acceso aos servicios de unha zona.

ver: https://firewalld.org/documentation/man-pages/firewall-cmd.html 
