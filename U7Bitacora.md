# Unidad 7


## Introducción 📜

> [!NOTE]
> Dando vida física a las palabras
> En esta unidad, nos enfrentamos a un reto de diseño que combina la expresividad conceptual con la simulación física. Exploraremos la idea de la tipografía semántica, donde la forma visual de una palabra refuerza o juega con su significado, pero le daremos un giro dinámico.
>
> Inspirados por el concepto “Word as Image”, utilizaremos la biblioteca de física 2D Matter.js junto con p5.js para no solo representar el significado de una palabra, sino para darle vida animada a través de la simulación física. ¿Cómo pueden las propiedades físicas (gravedad, colisiones, restricciones) animar una palabra para expresar su esencia?

---

## Set: ¿Qué aprenderás en esta unidad? 💡

> [!TIP]
> Objetivos de aprendizaje
>
> Al finalizar esta unidad, serás capaz de:
>
> - Comprender y aplicar creativamente el concepto de “Word as Image” (tipografía semántica).
> - Investigar e identificar las funcionalidades básicas de la biblioteca Matter.js (motor, mundo, cuerpos, restricciones).
> - Integrar Matter.js con p5.js para crear simulaciones físicas 2D.
> - Utilizar cuerpos y restricciones de Matter.js para construir formas complejas (como letras).
> - Aplicar principios de física simulada para animar una palabra de forma que refleje su significado.
> - Resolver problemas técnicos relacionados con la integración de p5.js y Matter.js.

### Actividad 01

> [!NOTE]
> 🎯 Enunciado
>
> Vamos a explorar cómo la forma visual de las letras y palabras puede comunicar su significado intrínseco, inspirándonos en el trabajo del diseñador Ji Lee.

> [!TIP]
> Recursos
>
> Concepto “Word as Image” de Ji Lee: observa el trabajo de Ji Lee [“Word as Image”](https://pleaseenjoy.com/#/word-as-image/). Analiza cómo manipula la tipografía para ilustrar el significado de la palabra.


#### Pasos:

1. **Explora los ejemplos:** dedica tiempo a observar varios ejemplos del proyecto “Word as Image” de Ji Lee.

2. **Analiza la técnica:** para 3-4 ejemplos que te llamen la atención, describe brevemente cómo la manipulación visual de la palabra refuerza o representa su significado. ¿Qué elementos gráficos o tipográficos utiliza?

3. **Genera tus propias ideas (estáticas):** elige 2-3 palabras diferentes. Para cada una, piensa y describe (o haz un boceto muy simple) cómo podrías representarla visualmente siguiendo el concepto “Word as Image”, sin pensar aún en animación o física. ¿Cómo alterarías las letras o la composición para evocar el significado?

> [!NOTE]
> 🧐🧪✍️ Reporta en tu bitácora
>
> 1. Tu análisis de 3-4 ejemplos de Ji Lee, explicando cómo logran la conexión palabra-imagen.
> 2. Tus propias ideas (descripción o boceto simple) para representar visualmente 2-3 palabras distintas de forma estática.

## Seek: Investigación 🔎

> [!NOTE]
> Explorando Matter.js
>
> Para dar vida física a nuestras palabras, necesitamos dominar una nueva herramienta: Matter.js. Investigaremos sus conceptos fundamentales y funcionalidades básicas para poder aplicarla en nuestro reto.

### Actividad 02

> [!NOTE]
> 🎯 Enunciado
>
> Para animar nuestras palabras con física, necesitamos entender Matter.js. Investigaremos sus conceptos clave y realizaremos experimentos básicos para familiarizarnos con su uso junto a p5.js.

> [!TIP]
> Recursos
>
> **Obligatorios:**
>
> - Sitio web oficial de Matter.js: https://brm.io/matter-js/ (explora los demos).
> - Video Tutorial de Patt Vira: p5.js Coding Tutorial | Introduction to matter.js
>
> **Opcionales:**
>
> Documentación de la API de Matter.js (para profundizar).
Otros tutoriales o ejemplos que encuentres.
Pasos:

Visualiza y lee: mira el video de Patt Vira completo. Explora los ejemplos básicos en el sitio web de Matter.js.
Identifica conceptos clave: mientras exploras, presta atención a estos conceptos fundamentales: Engine, World, Bodies (y sus tipos: rectángulos, círculos, polígonos), Constraint, MouseConstraint, Runner/Events.
Experimenta con código:
Intenta replicar en p5.js al menos dos experimentos básicos mostrados en el video de Patt Vira o en los ejemplos del sitio web. Por ejemplo:
Crear un mundo con gravedad y añadir algunos cuerpos simples (círculos, cajas) que caigan y colisionen.
Crear cuerpos estáticos (como el suelo).
Implementar MouseConstraint para poder interactuar con los cuerpos usando el mouse.
(Opcional avanzado) Crear una restricción simple (Constraint) entre dos cuerpos.
Explica los conceptos: basándote en tu experimentación y lectura, explica con tus propias palabras qué es y para qué sirve cada uno de los conceptos clave listados en el paso 2 (Engine, World, Bodies, Constraint, MouseConstraint).
🧐🧪✍️ Reporta en tu bitácora

Muestra el código de los dos (o más) experimentos básicos que replicaste integrando Matter.js y p5.js.
Incluye una **captura de pantalla o ENLACE a un GIF (no olvides, enlace) de cada experimento funcionando.
Proporciona tu explicación clara y concisa de los conceptos clave (Engine, World, Bodies, Constraint, MouseConstraint).
Menciona brevemente cualquier dificultad encontrada al configurar o usar Matter.js inicialmente.
Apply: Aplicación 🛠
¡A Animar palabras!

Es el momento de combinar inspiración, física y código. Aplicarás el concepto de “Word as Image” y tus nuevos conocimientos de Matter.js para crear una animación generativa donde una palabra cobra vida según su significado.

Actividad 03
Animando la tipografía semántica
🎯 Enunciado

¡Es hora de aplicar todo! Elige una palabra y, usando p5.js y Matter.js, crea una animación donde la palabra “actúe” o se comporte físicamente de una manera que refleje su significado, inspirándote en el concepto “Word as Image”.

Recursos

Tus ideas estáticas de la Actividad 01.
Tu conocimiento y código de experimentación de Matter.js (Actividad 02).
Documentación de Matter.js.
Tu creatividad y habilidades de p5.js.
Pasos:

Elige tu palabra: selecciona una palabra cuyo significado te inspire una idea de animación física (ej: “caer”, “flotar”, “romper”, “elástico”, “rígido”, “conectar”, “repeler”).
Diseña la animación física:
¿Cómo representarás la palabra? ¿Usarás cuerpos de Matter.js para formar las letras?
¿Qué comportamiento físico (caída, flotación, colisión, elasticidad, ruptura, conexión) representará el significado?
¿Cómo configurarás el mundo de Matter.js (gravedad, límites) y las propiedades de los cuerpos (masa, fricción, restitución/elasticidad) para lograr ese comportamiento?
¿Habrá alguna interacción del usuario (ej: click para iniciar la acción, mouse para perturbar)?
Implementa en p5.js + Matter.js: escribe el código.
Configura el motor y mundo de Matter.js.
Crea los cuerpos (Bodies) que forman tu palabra. Esto puede requerir paciencia y experimentación para obtener las formas deseadas. Usa Constraint si necesitas unir partes.
Define las propiedades físicas y las condiciones iniciales.
Implementa la interacción si la diseñaste.
Dibuja los cuerpos de Matter.js en el canvas de p5.js en cada frame.
Prueba y Refina: ejecuta tu sketch repetidamente. Ajusta la gravedad, las propiedades de los cuerpos, las restricciones y cualquier otro parámetro hasta que la animación física comunique efectivamente el significado de la palabra de una manera interesante.
🧐🧪✍️ Reporta en tu bitácora

Indica claramente la palabra elegida.
Explica tu idea conceptual: ¿Cómo la animación física representa el significado de la palabra?
Describe brevemente los aspectos técnicos clave de tu implementación: ¿Cómo formaste las letras con Matter.js? ¿Qué propiedades físicas fueron importantes? ¿Usaste restricciones?
Incluye el código completo de tu sketch final.
Inserta una captura de pantalla estática Y un enlace a un GIF animado (¡Esencial!) que muestre tu tipografía semántica animada en acción.
Evidencias 🗂️
RUBRICA!

Recuerda que la bitácora se cierra 10 minutos antes de iniciar la sesión de evaluación de la unidad (segunda sesión de la segunda semana). plasma en la bitácora. La bitácora no es un resultado que se llena a última hora.
Si no realizas la autoevaluación tu nota será 0.
Si una actividad no está COMPLETA debes multiplicar la nota de esa actividad por el porcentaje de avance que tengas.
Puedes usar IA generativa para generar código, pero NO para DISEÑAR.
Rúbrica de evaluación del proceso

5: realicé las 3 actividades completas y la autoevaluación.
4: realicé 2 actividades completas y la autoevaluación.
2: realicé 1 actividad completa y la autoevaluación.
0: no realicé ninguna actividad o no realicé la autoevaluación.

EVIDENCIAS EN BITÁCORA

Realiza las actividades propuestas en esta unidad y documenta todo el proceso en tu bitácora.
Realiza la autoevaluación indicando:
Tu nota propuesta.
La defensa de esa nota para cada actividad.
Reflect: Consolidación y metacognición 🤔
En esta unidad te mostré que los conceptos del curso pueden llevarse al mundo del diseño gráfico y la tipografía. Quiero invitarte a pensar en cómo podrías aplicar estos conceptos en tu propio interés o énfasis profesional. Y qué tal si lo que aprendiste en esta unidad intentas aplicarlo en tu portafolio profesional? Tal vez en la página web de tu portafolio? Y si no tienes una página web para tu portafolio qué tal si te animas a hacer una?
