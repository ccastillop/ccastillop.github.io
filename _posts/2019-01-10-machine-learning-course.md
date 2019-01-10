---
layout: post
title:  "Curso Machine Learning"
date:   2019-01-10 14:54:00 -0500
categories: machine-learning
---

En Diciembre de 2018, [INICTEL-UNI][INICTEL] y la [PCM][PCM] organizaron un curso introductorio de 21 horas para los trabajadores de la Secretaría de Gobierno Digital (SGD) de la PCM. El curso buscaba adquirir los fundamentos teóricos y prácticos para el desarrollo de modelos de _Machine Learning_. 

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

### Taller de Ejemplo
Predecir el costo de una carretera nueva en base a los datos de carreteras ya construidas. Las variables son 

- X1: Altura en mts.
- X2: Longitud en km.
- X3: Carriles
- X4: Número de curvas pronunciadas

La solución desarrollada en Matlab, junto con la data de entrenamiento, pueden verse en mi [Github][clase_04]

Clasificación usando Regresión Logística
____

La Regresión logística es útil para problemas donde la estimación es una clasificación. Por ejemplo, dado ciertas condiciones saber si una persona está sana o afectada. La función logística es ideal para clasificación:

$$ h_{\theta}(x) = \frac{1}{ 1 + e^{-\theta^{t}x } } $$

$$ 0 \leq h_{\theta}(x) \leq 1 $$ 

Mientras, la función de costo utiliza el logaritmo para determinar el error. La suma de estos errores debe ser entonces minimizada.

$$ Error = \left\{\begin{matrix}
 -log(h_{\theta}(x)) & , y = 1 \\ 
 -log(1 - h_{\theta}(x)) & , y = 0  
\end{matrix}\right. $$

El algoritmo para minimizar la función de costo es igualmente el algoritmo de gradiente descendiente. Un ejemplo extendido de este procedimiento es la clasificación multiclase. En sí es aplicar el algoritmo OVR (One vs Rest) para ir construyendo múltiples clasificaciones binarias. 

### Taller para detectar números en imágenes

La solución desarrollada en Matlab, junto con la data de entrenamiento, pueden verse en mi [Github][clase_05]

Redes Neuronales
-----

Inspirado en la biología, las redes neuronales buscan replicar el funcionamiento de las neuronas encontradas en los seres vivios. El primer modelo matemático de la neurona se llama [Perceptrón][perceptron], que busca obtener una salida binara a partir de varias entradas binárias y una funcion de transferencia lineal, con parámetros o pesos constantes. 

El Perceptrón resultó ser una buena primera aproximación, pero recibió muchas críticas por sus limitaciones. Un segundo modelo fue el perceptrón multicapa, que en sí permite combinaciones de pesos y potencias mucho más complejo. 

El gran problema de estos modelos es cómo entrenamos la red para que prediga un resultado valioso. Se desarrollaron algoritmos tales como el _back propagation_ que, utilizando redes de realimentación, permite que la red aprenda. Estos algoritmos están implementados en _Matlab_ por lo que es relativamente sencillo constuirlos y entrenarlos. 

Sin embargo, un esquema más eficiente de red neuronal es especializar grupos de redes para que aprendan ciertos aspectos o conceptos del problema. Por ejemplo, para detectar si una imagen es un auto o un camión o una bicicleta, una red se especializa en las formas, otra en los contornos, otra en la conexión entre formas o puntos de contacto, entre otros conceptos. La última red combina estos conceptos para obtener resultados mucho más exactos con menos neuronas.
Esta forma de diseñar redes se denomina [Deep Learning][deep_learning] o Aprendizaje Profundo.

### Taller de redes neuronales

La solución desarrollada en Matlab de una red neuronal para detectar y seleccionar números, junto con la data de entrenamiento, pueden verse en mi [Github][clase_06]

_Chat bot_
-----

La última clase fue un taller práctico de cómo crear un _chat bot_ para que responda a preguntas en español sobre información de expedientes. Se utilizó el servicio gratuito de Microsoft llamado [LUIS][luis]

En sí los pasos para crear un _chat bot_ utlilizando los servicios de Microsoft son:

- Crearse una cuenta en Outlook.es y utilizarla para registrarse en [LUIS][luis]
- Crear los _Intents_, que son las intenciones. Ejemplo: ListarExpedientes
- Crear _Entidades_ que son las palabras clave relevantes para identificar la itención del usuario. Ejemplo: ciudad, número
- Cada _Entidad_ puede describirse con una lista de frases que la identifica.
- Las _Utterances_ son las oraciones que al final identifican una sola intención. Ejemplo: quiero obtener los expedientes...

Con estos datos se crea el _chat bot_ y se entrena en la misma aplicación [LUIS][luis]. Finalmente, se puede consumir el servicio mediante una sencilla [API REst][api_rest] que lo consuma. 

La solución desarrollada en Matlab que consume esta API RESt pueden verse en mi [Github][clase_07]

Conclusiones
-----

Este curso toca apenas la superficie del mundo del _Machine Learning_. El profesor Eduardo Serrano Campos nos abrió la mente ante la fuerte tendencia actual del _Data Science_ y cómo el mundo cada vez depende más de científicos que puedan procesar e interpretar estos datos, con el fin de obtener información y predicciones valiosas. 


{% include_relative shared/mathjax.html %}
{% include_relative shared/footer_machine_learning.md %}
