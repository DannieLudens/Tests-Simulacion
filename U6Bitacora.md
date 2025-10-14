# Unidad 6

## Introducción 📜

> [!NOTE]
> **Agentes autónomos y comportamiento emergente**
>
> Continuando nuestro viaje por “The Nature of Code”, nos adentramos en el fascinante mundo de los **agentes autónomos**. Estos son entidades que operan independientemente en un entorno, tomando decisiones basadas en un conjunto de reglas y en la percepción de su entorno (incluyendo otros agentes).
>
> En esta unidad, exploraremos cómo algunas reglas simples a nivel individual pueden dar lugar a comportamientos colectivos complejos y a menudo inesperados, un fenómeno conocido como emergencia. Nos centraremos en dos algoritmos clave presentados en “The Nature of Code”: los **campos de flujo (flow fields)** y el **comportamiento de enjambre (flocking).**

## Set: ¿Qué aprenderás en esta unidad? 💡

> [!NOTE]
> **Objetivos de aprendizaje**
>
> Al finalizar esta unidad, serás capaz de:
>
> - Describir el concepto de agente autónomo y comportamiento emergente en el contexto del arte generativo.
> - Analizar y explicar el funcionamiento de los algoritmos de campos de flujo (flow fields) y comportamiento de enjambre (flocking) presentados en “The Nature of Code”.
> - Identificar los parámetros clave que controlan el comportamiento de los agentes en ambos algoritmos.
> - Implementar un sketch interactivo en p5.js que utilice flow fields o flocking.
> - Aplicar creativamente uno de estos algoritmos.


### Actividad 01

En esta actividad propondré que te encuentres de nuevo el trabajo de [Tyler Hobbs](https://youtu.be/8tTGJvijoDw?si=7KWuEhMTIjH41JOj) y específicamente que mires [su artículo sobre campos de flujo.](https://www.tylerxhobbs.com/words/flow-fields)

> [!NOTE]
> 🧐🧪✍️ Reporta en tu bitácora
>
> - Captura en tu bitácora dos imágenes de Tyler Hobbs que te llamen la atención y explica por qué.
> - ¿Qué te inspira de su trabajo?


## Seek: Investigación 🔎

> [!NOTE]
> Analizando los algoritmos
> 
> Vamos a sumergirnos en el código y la lógica detrás de los campos de flujo y el comportamiento de enjambre, utilizando los ejemplos de “The Nature of Code” como punto de partida. El objetivo es entender cómo funcionan internamente.

### Actividad 02

En esta actividad quiero que investigues alrededor de estas dos preguntas:

1. ¿Qué es una fuerza de dirección (steering force)?
2. ¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?
3. ¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?


> [!NOTE]
> 🧐🧪✍️ Reporta en tu bitácora
>
> Documenta tus hallazgos en tu bitácora.

### Actividad 03

> [!NOTE]
> 🎯 Enunciado
>
> Vamos a analizar el primer algoritmo clave: los campos de flujo (Flow Fields), basándonos en el ejemplo del libro “The Nature of Code”. Entenderemos cómo una cuadrícula de vectores dirige el movimiento de los agentes.

> [!TIP]
> Recursos
>
> - Libro “The Nature of Code” (TNoC) de Daniel Shiffman: [Capítulo 5, sección “Flow Fields”](https://natureofcode.com/autonomous-agents/#flow-fields) (y ejemplos de código asociados).
> - El código fuente del ejemplo de Flow Fields de TNoC.


#### Pasos:

1. **Ejecuta el ejemplo:** ejecuta el código del ejemplo principal de Flow Fields de TNoC en p5.js. Observa el comportamiento de los vehículos/agentes.

2. **Identifica la estructura del campo:** en el código (usualmente en una clase `FlowField`), localiza cómo se almacena el campo de flujo. ¿Qué estructura de datos se usa (ej: un array 2D)? ¿Qué representa cada elemento de esa estructura? ¿Cómo se calcula inicialmente el vector en cada punto?

3. **Analiza el comportamiento del agente:** en el código de la clase del vehículo/agente (`Vehicle`), encuentra la función `follow()`. Explica con tus palabras:
  - ¿Cómo determina el agente qué vector del campo de flujo debe seguir basándose en su posición actual? (pista: implica mapear la posición a índices de la cuadrícula).
  - Una vez que tiene el vector deseado del campo, ¿Cómo lo utiliza para calcular la fuerza de dirección (`steering force`)? (pista: implica calcular la diferencia con la velocidad actual y limitar la fuerza).

4. Identifica parámetros clave: localiza en el código las variables que controlan aspectos importantes como:

   - La resolución del campo de flujo (el tamaño de las celdas de la cuadrícula).
   - La velocidad máxima (`maxspeed`) y la fuerza máxima (`maxforce`) de los agentes.
  
5. Experimenta con modificaciones: realiza al menos una de las siguientes modificaciones en el código, ejecuta y describe el efecto observado en el comportamiento de los agentes:
   - Cambia significativamente la forma en que se generan los vectores del campo (ej: usa una fórmula matemática diferente en lugar de noise(), o cambia drásticamente los parámetros de noise()).
   - Modifica sustancialmente la resolución del campo de flujo (hazla mucho más fina o mucho más gruesa).
   - Altera considerablemente maxspeed o maxforce de los agentes.
  

> [!NOTE]
> 🧐🧪✍️ Reporta en tu bitácora
>
> 1. Explica brevemente la estructura de datos usada para el campo de flujo y cómo se generan sus vectores.
> 2. Describe con tus palabras cómo un agente utiliza el campo para calcular su fuerza de dirección.
> 3. Lista los parámetros clave identificados (resolución, maxspeed, maxforce).
> 4. Describe la modificación que realizaste al código y **explica detalladamente el efecto** que tuvo en el movimiento y comportamiento colectivo de los agentes. Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.


### Actividad 04

> [!NOTE]
> 🎯 Enunciado
> Ahora analizaremos el segundo algoritmo: el comportamiento de enjambre (Flocking), famoso por simular el movimiento coordinado de pájaros o peces. Nos basaremos nuevamente en “The Nature of Code” para entender las tres reglas básicas que lo gobiernan.

> [!TIP]
> Recursos
>
> Libro “The Nature of Code” (TNoC) de Daniel Shiffman: [capítulo 5, sección “Flocking”](https://natureofcode.com/autonomous-agents/#flocking) (y ejemplos de código asociados).
> El código fuente del ejemplo de Flocking de TNoC.

#### Pasos:

1. **Ejecuta el ejemplo: **ejecuta el código del ejemplo principal de Flocking de TNoC en p5.js. Observa el movimiento colectivo de los “boids” (agentes).

2. Identifica las tres reglas: en el código de la clase del agente (ej: Boid), localiza las funciones que implementan las tres reglas fundamentales del Flocking:

   - **Separación (Separation):** evitar el hacinamiento con vecinos cercanos.
   - **Alineación (Alignment):** dirigirse en la misma dirección promedio que los vecinos cercanos.
   - **Cohesión (Cohesion):** moverse hacia la posición promedio de los vecinos cercanos.
  
3. **Explica las reglas:** para cada una de las tres reglas, explica con tus propias palabras:

   - ¿Cuál es el objetivo de la regla?
   -  ¿Cómo calcula el agente la fuerza de dirección correspondiente? (describe la lógica general, ej: “Calcula un vector apuntando lejos de los vecinos demasiado cercanos”).
  
4. **Identifica parámetros clave:** localiza en el código las variables que controlan:
   - El radio (o distancia) de percepción (`perceptionRadius` o similar) que define quiénes son los “vecinos”. A veces también hay un ángulo de percepción.
   - Los pesos o multiplicadores que determinan la influencia relativa de cada una de las tres reglas al combinarlas.
   - La velocidad máxima (`maxspeed`) y la fuerza máxima (`maxforce`) de los agentes (similar a Flow Fields).

5. **Experimenta con modificaciones:** realiza al menos **una** de las siguientes modificaciones en el código, ejecuta y describe el efecto observado en el comportamiento colectivo del enjambre:

   - Cambia drásticamente el peso de una de las reglas (ej: pon la cohesión a cero, o la separación muy alta).
   - Modifica significativamente el radio de percepción (hazlo muy pequeño o muy grande).
   - Introduce un objetivo (`target`) que todos los boids intenten seguir (usando una fuerza de `seek`) además de las reglas de flocking, y ajusta su influencia.
  
> [!NOTE]
> 🧐🧪✍️ Reporta en tu bitácora
>
> 1. Explica con tus palabras el objetivo y la lógica general de cálculo de cada una de las tres reglas de Flocking (Separación, Alineación, Cohesión).
> 2. Lista los parámetros clave identificados (radio de percepción, pesos de las reglas, maxspeed, maxforce).
> 3. Describe la modificación que realizaste al código y **explica detalladamente el efecto** que tuvo en el comportamiento colectivo del enjambre (¿Se dispersan? ¿Forman grupos compactos? ¿se mueven caóticamente?). Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.

## Apply: Aplicación 🛠

> [!NOTE]
> Creación generativa con un giro inesperado
>
> Ahora que entiendes los algoritmos, es tu turno de crear. Aplicarás uno de ellos (flow fields o flocking) para generar una pieza de arte interactivo que permita visualizar un tema musical de tu elección. La interacción del usuario debe influir en el comportamiento de los agentes.

### Actividad 05

1. Elige un tema musical que te inspire.
2. Diseña una pieza de arte generativo que utilice el algoritmo de flow fields y/o flocking.
3. Vas a visualizar el tema musical y además vas a “tocar” las visuales, es decir, tu pieza de arte debe ser interactiva y debe permitir la interpretación en tiempo real de las visuales como si fuera un instrumento más que acompaña de manera coherente el tema musical.

> [!NOTE]
> 🧐🧪✍️ Reporta en tu bitácora
>
> 1. Documenta todo el proceso de diseño y creación en tu bitácora, incluyendo bocetos y decisiones de diseño.
> 2. El código fuente completo de tu sketch en p5.js.
> 3. Un enlace a tu sketch en el editor de p5.js.
> 4. Capturas de pantalla mostrando tu pieza en acción.


## Evidencias 🗂️

> [!NOTE]
> RUBRICA!
>
> - Recuerda que la bitácora se cierra 10 minutos antes de iniciar la sesión de evaluación de la unidad (segunda sesión de la segunda semana). plasma en la bitácora. La bitácora no es un resultado que se llena a última hora.
> - Si no realizas la autoevaluación tu nota será 0.
> - Si una actividad no está COMPLETA debes multiplicar la nota de esa actividad por el porcentaje de avance que tengas.
> - Puedes usar IA generativa para generar código, pero NO para DISEÑAR.
> 
> Rúbrica de evaluación del proceso
>
> 5: realicé las 5 actividades completas y la autoevaluación.
> 4: realicé 4 actividades completas y la autoevaluación.
> 3: realicé 3 actividades completas y la autoevaluación.
> 2: realicé 2 actividades completas y la autoevaluación.
> 1: realicé 1 actividad completa y la autoevaluación.
> 0: no realicé ninguna actividad o no realicé la autoevaluación.

> [!WARNING]
> **EVIDENCIAS EN BITÁCORA**
> 1. Realiza las actividades propuestas en esta unidad y documenta todo el proceso en tu bitácora.
> 2. Realiza la autoevaluación indicando:
>    - Tu nota propuesta.
>    - La defensa de esa nota para cada actividad.


## Reflect: Consolidación y metacognición 🤔

1. Explica en tus propias propias palabras qué es un agente autónomo y cómo puede contribuir al arte generativo.


2. ¿Qué es el comportamiento emergente y cómo se manifiesta en los algoritmos de flow fields y flocking?

3. Para los más curisos. ¿Puedo aplicar lo que aprendí en esta unidad en Blender? Te dejo un [video](https://youtu.be/eqLA7oJkLyM?si=s97HHI8vErOxSDO5) para que te antojes y si creas algo en Blender ¿Me muestras?
