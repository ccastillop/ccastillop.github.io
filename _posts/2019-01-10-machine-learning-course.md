---
layout: post
title:  "Curso Machine Learning"
date:   2019-01-10 14:54:00 -0500
categories: machine-learning
---

En Diciembre de 2018, [INICTEL-UNI][INICTEL] y la [PCM][PCM] organizaron un curso introductorio de 21 horas para los trabajadores de la PCM. El curso buscaba adquirir los fundamentos teóricos y prácticos para el desarrollo de modelos de _Machine Learning_. 

A continuación trabajo un informe a modo de resumen del curso.


Condiciones previas
----------

Los participantes debieron llegar con los siguientes conocimientos

- Conocimientos básicos de programación
- Conocimientos básicos de álgebra lineal de pregrado (matrices, vectores, entre otros)
- Conceptos básicos de cálculo (derivadas) para entender los algoritmos

Introducción a _Machine Learning_
------------

La Inteligencia Artificial es un campo de estudio que busca que las computadoras haga tareas para las cuales el humano requiere inteligencia, tales como sistemas expertos, procesamiento de imágenes, árboles y algoritmos heurísticos.

_Machine Learning_ es un sub campo de la Inteligencia Articial que se enfoca en utilizar métodos estadísticos para que la computadora aprenda en función de los datos históricos que se le entrega para entrenarse. Las herramientas y modelos utilizados son sobre todo del campo de la estadística, tales como modelo de regresión lineal, regresión lógica, entre otras.

Regresión lineal con una variable
-------
El modelo de regresión lineal busca, a partir de datos históricos, obtener la ecuación de una recta que permita estimar o predecir los valores futuros. Por ejemplo, predecir la nota que tendrá un alumno dado su porcentaje de asistencia al curso.

La siguiente ecuación permite obtener la nota $h$ a partir de $x$

$$h(x) = \theta_0 + \theta_1 x $$

El reto consiste en obtener los valores de $\theta_0$ y $\theta_1$ que estimen de la mejor manera el valor de $h$. Para obtenerlos, utilizamos datos históricos de entrenamiento, $m$ pares $[x, h]$. El error mínimo de la estimación la da la _función de costo_ siguiente:

$$ J(\theta) = \frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x_i) - y_i)^{2} $$

El objetivo es $ \frac{Min J(\theta)}{\theta} $, es decir, minimizar el valor de $ J(\theta) $ y así obtener las mejores estimaciones bajo el modelo de regresión lineal. 

Pero ¿Cómo lograr, utilizando programación, el menor valor?. Se utiliza el _Algoritmo de Gradiente Descendente_. El reto está implementar este algoritmo en programación. Esto requiere una revisión de lo que es álgebra lineal, vectorización y optimización para programación.

Revisión de Álgebra Lineal y Vectorización
-------
En la siguiente clase se revisan estos conceptos: matrices, vectores tanto de columna como de fila y la nomemclatura de los elementos de la j-ésima columna $A_{:,j}$, o de la j-ésima fila $A_{j,:}$. También se revisó las operaciones con matrices: suma, multiplicación, producto interno, producto externo, multiplicación escalar. 


Procesadores y operaciones vectoriales. Uso de Matlab
-----
Nótese que los algoritmos pueden ser expresados como combinaciones de operaciones vectoriales. Y las instrucciones [SIMD][SIMD] de los microprocesadores están optimizados para estas operaciones. Es más, combinando las operaciones SIMD con la arquitectura multi-nucleo es posible velocidades de procesamiento considerablemente rápidas. 

Este tipo de procesadores suelen encontrarse en los [GPU][GPU], es decir, en los procesadores usados en las tarjetas de video. Por ello, son usadas itensivamente en el procesamiento de _machine_learning_. Finalmente, este tipo de procesadores pueden ser alquilados en la nube. 

Resulta valioso ejercitar álgebra lineal utilizando _Matlab_, el software _de facto_ para trabajos científicios. 

Finalmente, los ejercicios utilizando Matlab pueden verse en mi [Github][clase_03]

Regresión lineal con múltiples variables
-----
Llega el momento de aplicar el algoritmo para hacer regresión lineal de múltiples variables: $$h(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2+ ... + \theta_n x_n$$. Entonces, aplicando la función de costo antes señalada, y acondicionando la ecuación a $$h(x) = \theta_0 x_0 + \theta_1 x_1 + \theta_2 x_2+ ... + \theta_n x_n$$ con $x_0 = 1$ se puede usar cálculo vectorial optimizado para programación. 

Un paso adicional antes de pasar a la programación es el Escalamiento o Estandarización de Variables, que busca optimizar el algoritmo de gradiente descendente para buscar el valor óptimo sin que sufra. El escalamiento se realiza calculando el valor promedio $\mu$ y la desviación estándar $\sigma$ de los datos:

$$VariableEscalada = \frac{VariableOrigianl - \mu}{\sigma} $$




{% include_relative shared/mathjax.html %}
{% include_relative shared/footer_machine_learning.md %}
