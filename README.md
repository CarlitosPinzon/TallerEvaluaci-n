# Parallel Matrix Multiplication Benchmark

## Descripción

Este proyecto evalúa el rendimiento de diferentes implementaciones de multiplicación de matrices cuadradas utilizando distintos modelos de paralelismo en sistemas tipo Unix.

Se comparan las siguientes estrategias:

- Implementación clásica utilizando procesos con `fork`
- Implementación paralela utilizando `OpenMP`
- Implementación paralela utilizando `POSIX Threads`
- (Base implícita) enfoque secuencial tradicional

El objetivo es analizar el comportamiento en tiempo de ejecución y observar las diferencias en desempeño según el modelo de concurrencia utilizado.

---

## Objetivo

Evaluar el impacto del paralelismo en la multiplicación de matrices de gran tamaño, midiendo tiempos de ejecución y comparando eficiencia entre:

- Paralelismo basado en procesos (`fork`)
- Paralelismo basado en hilos (`POSIX Threads`)
- Paralelismo mediante directivas de compilador (`OpenMP`)

Se busca analizar:

- Overhead de creación de procesos vs hilos
- Escalabilidad
- Aprovechamiento de múltiples núcleos
- Costos de sincronización

---

## Estructura del Proyecto


### Archivos principales

- `mmClasicaFork.c`  
  Implementación de multiplicación de matrices utilizando procesos hijos creados con `fork`.

- `mmClasicaOpenMP.c`  
  Implementación paralela utilizando directivas `OpenMP`.

- `mmClasicaPosix.c`  
  Implementación paralela utilizando `POSIX Threads`.

- `Funciones.c / Funciones.h`  
  Funciones auxiliares compartidas por las distintas implementaciones.

- `Makefile`  
  Automatiza la compilación de las distintas versiones.

- `lanza.pl`  
  Script para automatizar ejecuciones y recolección de resultados.

- Archivos `.jpg` y `.xlsx`  
  Contienen visualizaciones y tablas de los resultados obtenidos para distintos tamaños de matrices.

---

## Metodología Experimental

Se realizaron pruebas con matrices cuadradas de distintos tamaños:

- 500x500
- 1000x1000
- 2000x2000

Para cada implementación se midió el tiempo de ejecución y se registraron los resultados en tablas y gráficos comparativos.

Las métricas observadas incluyen:

- Tiempo total de ejecución
- Comparación relativa entre métodos
- Diferencias de rendimiento según tamaño del problema

---

## Compilación

Utilizar el `Makefile` incluido: make


Dependiendo del archivo específico, puede requerirse:

- Compilador compatible con OpenMP (por ejemplo `gcc` con flag `-fopenmp`)
- Soporte para `pthread` (`-lpthread`)

Ejemplo manual de compilación:
gcc mmClasicaOpenMP.c Funciones.c -fopenmp -o openmp
gcc mmClasicaPosix.c Funciones.c -lpthread -o posix
gcc mmClasicaFork.c Funciones.c -o fork


---

## Resultados

Los resultados muestran diferencias significativas en rendimiento dependiendo del modelo de paralelismo utilizado.

Observaciones generales:

- `OpenMP` tiende a ofrecer una implementación más sencilla y eficiente en términos de desarrollo.
- `POSIX Threads` proporciona mayor control sobre la gestión de hilos.
- `fork` introduce mayor overhead debido a la creación de procesos independientes.
- A medida que aumenta el tamaño de la matriz, el paralelismo muestra ventajas más evidentes frente al enfoque secuencial.

Los gráficos incluidos permiten visualizar comparaciones directas entre métodos para distintos tamaños de entrada.

---

## Consideraciones Técnicas

- El rendimiento depende del número de núcleos disponibles en la máquina.
- El uso de procesos (`fork`) implica mayor consumo de memoria comparado con hilos.
- El paralelismo no siempre garantiza mejora si el overhead supera el beneficio computacional.
- La escalabilidad depende de la correcta división del trabajo y sincronización.

---
 
## Conclusión

Este proyecto permite comparar distintos modelos de paralelismo en C aplicados a un problema clásico de alto costo computacional.

Más allá del ejercicio académico, el análisis evidencia cómo la elección del modelo de concurrencia impacta directamente en rendimiento, escalabilidad y complejidad de implementación.
