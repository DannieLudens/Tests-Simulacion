# Unidad 5

## Introducción 📜

En esta unidad voy a explorar los sistemas de partículas. Los sistemas de partículas son conjuntos de partículas que interactúan entre sí y con su entorno. Estos sistemas son fundamentales en el mundo del arte y diseño generativo, ya que permiten crear composiciones complejas y dinámicas a partir de reglas simples.

> [!WARNING]
> Evidencias en bitácora
>
> - En la bitácora debes incluir las siguientes evidencias:
>
> - Las solicitudes de la actividad 2 (Investigación).
> - Las solicitudes de la actividad 3 (Aplicación).
> - Tu mismo vas a propoer una nota basada en la rúbrica y justificarás cada criterio de la rúbrica indicando qué evidencias presentes en la bitácora justifican la nota que propones.
> - Si tu bitácora no incluye la nota propuesta y la justificación tendrás una nota de 0.

## Set: ¿Qué aprenderás en esta unidad? 💡

En esta unidad vas a experimentar con aplicaciones interactivas que tendrán las siguientes características:

- Emitirán partículas que se moverán en el espacio.
- Las partículas estarán sujetas a fuerzas que las harán cambiar de dirección y velocidad.


Ten presente que estos sistemas se ejecutarán en tiempo real usando la CPU. Por lo tanto, deberás tener en cuenta las limitaciones de rendimiento y optimización al diseñar tus sistemas de partículas. Mejor dicho, no podrás tener miles de partículas en pantalla sin que el rendimiento se vea afectado. Para lograr esto necesitarás recurrir a la programación de la GPU usando shaders. Pero esto lo harás en la siguiente temporada.

### Actividad 01

Solo para antojarte un poco, te pediré que mires el trabajo de uno de los artistas generativos más reconocidos actualmente. Se trata de [Refik Anadol](https://refikanadol.com/)

## Seek: Investigación 🔎

En esta fase, repasarás los conceptos de herencia y polimorfismo que aplicarás para crear sistemas de partículas que se comporten y se vean de manera diferente. Adicionalmente, aplicarás fuerzas a las partículas para que se muevan e interactúan con el entorno.

### Actividad 02

#### Revisa y repasa algunos conceptos

Dale una mirada al [capítulo sobre sistemas de partículas](https://natureofcode.com/particles/) del texto guía del curso. Explora libremente, pero te pediré que revises especialmente los siguientes conceptos:

1. Revisa detalladamente el ejemplo 4.2: [an Array of Particles.](https://natureofcode.com/particles/#example-42-an-array-of-particles)
2. Analiza el ejemplo 4.4: a [System of Systems.](https://natureofcode.com/particles/#example-44-a-system-of-systems)
3. Analiza el ejemplo 4.5: [a Particle System with Inheritance and Polymorphism.](https://natureofcode.com/particles/#example-45-a-particle-system-with-inheritance-and-polymorphism)
4. Analiza el ejemplo 4.6: [a Particle System with Forces.](https://natureofcode.com/particles/#example-46-a-particle-system-with-forces)
5. Analiza el ejemplo 4.7:[ a Particle System with a Repeller.](https://natureofcode.com/particles/#example-47-a-particle-system-with-a-repeller)

🧐🧪✍️ En tu bitácora responde a esta pregunta para cada una de las simulaciones: ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

Además te pediré que hagas los siguientes experimentos y los reportes en tu bitácora:

1. Vas a modificar cada una de las simulaciones anteriores incluyen en cada una, al menos un concepto de las unidades anteriores, pero no repitas concepto, la idea es que repases al menos uno de cada unidad.
2. Vas a gestionar la creación y la desaparición de las partículas y la memoria.
3. Explica cómo lo hiciste (aunque es posible que la simulación ya lo haga, trata de identificarlo de nuevo y explicarlo con tus palabras). Explica qué concepto aplicaste, cómo lo aplicaste y por qué.
4. Incluye un enlace a tu código en el editor de p5.js.
5. Incluye el código fuente de cada una de las simulaciones.
6. Captura de pantallas de cada una de las simulaciones con las imágenes que más te gusten como resultado de la ejecución de cada una de las simulaciones.

---

<details>
  <summary>Ejemplo 4.2 - Array de Partículas (an Array of Particles)</summary>

### Ejemplo 4.2 - Array de Partículas (an Array of Particles)

---

<details>
  <summary>🔍 Gestión de memoria</summary>

En este ejemplo observamos que:

**1. Creación de partículas:**
- Se usa `particles.push(new Particle(width/2, 20))` en cada frame
- Esto hace que el array crezca constantemente
- Cada partícula se crea en el centro superior del canvas

**2. Desaparición de partículas:**
- El método `splice(i, 1)` elimina partículas cuando `isDead()` retorna `true`
- Se recorre el array AL REVÉS (`i--`) para evitar saltos de índice
- Esto es crucial: si eliminas elementos mientras avanzas, algunos elementos se "saltan"

**3. Observción:**
- Sin el `splice()`, el array crecería infinitamente (60 partículas/segundo a 60 FPS = 3,600 partículas por minuto)
- Esto consumiría RAM progresivamente y bajaría los FPS drásticamente
- Es como una "limpieza automática" de memoria - solo mantiene partículas vivas

**Diagrama del ciclo de vida de una particula:**
```
[CREAR] → [ACTUALIZAR] → [¿Muerta?] → [ELIMINAR]
   ↑              ↓           ↓
   |          [Viva]     [splice()]
   └──────────────┘
```

**Código clave:**
```javascript
// Recorrer AL REVÉS es fundamental
for (let i = particles.length - 1; i >= 0; i--) {
  let p = particles[i];
  p.update();
  p.show();
  
  // Limpieza de memoria
  if (p.isDead()) {
    particles.splice(i, 1);  // Elimina del array
  }
}
```

**Observación importante:**
El `lifespan` disminuye 2 unidades por frame (`lifespan -= 2`), lo que significa que cada partícula vive aproximadamente 127 frames (255/2 ≈ 2.1 segundos a 60 FPS).

</details>

---

<details>
  <summary>🧪 Concepto aplicado: Ruido Perlin (Unidad 1)</summary>

#### Experimento: Ruido Perlin para movimiento orgánico

**¿Por qué elegí este concepto?**

Quería que las partículas tuvieran un movimiento más natural y fluido, similar a humo o vapor flotando en el aire, en lugar de simplemente caer por gravedad de forma predecible.

**¿Cómo lo implementé?**

1. **Variables únicas por partícula:**
```javascript
this.xoff = random(1000);  // Offset único en eje X
this.yoff = random(1000);  // Offset único en eje Y
```
Cada partícula comienza en una posición aleatoria del "espacio de ruido Perlin"

2. **Generación de fuerzas orgánicas:**
```javascript
let noiseX = map(noise(this.xoff), 0, 1, -0.1, 0.1);
let noiseY = map(noise(this.yoff), 0, 1, -0.05, 0.05);
let noiseForce = createVector(noiseX, noiseY);
this.acceleration.add(noiseForce);
```

3. **"Caminar" por el espacio de ruido:**
```javascript
this.xoff += 0.01;  // Avance suave en X
this.yoff += 0.01;  // Avance suave en Y
```

**¿Por qué diferentes rangos en X e Y?**
- Más movimiento horizontal (`-0.1 a 0.1`) crea dispersión lateral
- Menos movimiento vertical (`-0.05 a 0.05`) mantiene las partículas flotando sin subir demasiado

**Comparación con random():**
- `random()`: Saltos bruscos, movimiento errático y artificial
- `noise()`: Cambios suaves, movimiento fluido y natural

</details>

---

<details>
  <summary>💻 Código fuente completo</summary>

```javascript
let particles = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255, 25); // Transparencia para efecto de rastro
  
  particles.push(new Particle(width / 2, 20));
  
  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    p.update();
    p.show();
    
    if (p.isDead()) {
      particles.splice(i, 1);
    }
  }
  
  fill(0);
  noStroke();
  text(`Partículas: ${particles.length}`, 10, 20);
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0.5);
    this.acceleration = createVector(0, 0);
    this.lifespan = 255;
    
    // Ruido Perlin
    this.xoff = random(1000);
    this.yoff = random(1000);
  }
  
  update() {
    // Generar fuerzas desde ruido Perlin
    let noiseX = map(noise(this.xoff), 0, 1, -0.1, 0.1);
    let noiseY = map(noise(this.yoff), 0, 1, -0.05, 0.05);
    let noiseForce = createVector(noiseX, noiseY);
    
    this.acceleration.add(noiseForce);
    this.velocity.add(this.acceleration);
    this.velocity.limit(3);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    
    // Avanzar en el espacio de ruido
    this.xoff += 0.01;
    this.yoff += 0.01;
    
    this.lifespan -= 2;
  }
  
  show() {
    stroke(100, 150, 255, this.lifespan);
    strokeWeight(2);
    fill(150, 200, 255, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }
  
  isDead() {
    return this.lifespan < 0;
  }
}
```

**🔗 Enlace p5.js:** [Ver código en vivo](https://editor.p5js.org/DanieLudens/sketches/603sVXTDi)

</details>

---

#### 📸 Resultados visuales

**Observaciones visuales:**
- ✅ El efecto de rastro (`background(255, 25)`) crea líneas suaves que revelan las trayectorias
- ✅ Los colores azules (#96C8FF aproximadamente) sugieren agua o aire
- ✅ El movimiento es hipnótico y natural, no mecánico
- ✅ Las partículas se dispersan lateralmente mientras flotan, creando un patrón de "humo ascendente"

**Diferencias clave:**
- **Sin Perlin:** Las partículas caen en líneas casi rectas con pequeñas variaciones
- **Con Perlin:** Las partículas trazan curvas suaves, como si flotaran en corrientes de aire

</details>

</details>

|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/e868d5d8-5495-4295-91e9-561cf48002d6">|<img width="400" src="https://github.com/user-attachments/assets/0d5a3814-883d-4f54-a78d-1945d691ccea">|

<details>
  <summary> a System of Systems Modificado</summary>

#### 2.  a System of Systems Modificado

</details>

|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/e868d5d8-5495-4295-91e9-561cf48002d6">|<img width="400" src="https://github.com/user-attachments/assets/0d5a3814-883d-4f54-a78d-1945d691ccea">|

<details>
  <summary>a Particle System with Inheritance and Polymorphism Modificado</summary>

#### 3. a Particle System with Inheritance and Polymorphism Modificado

</details>

|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/e868d5d8-5495-4295-91e9-561cf48002d6">|<img width="400" src="https://github.com/user-attachments/assets/0d5a3814-883d-4f54-a78d-1945d691ccea">|

<details>
  <summary> a Particle System with Forces Modificado</summary>

#### 4.  a Particle System with Forces Modificado

</details>

|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/e868d5d8-5495-4295-91e9-561cf48002d6">|<img width="400" src="https://github.com/user-attachments/assets/0d5a3814-883d-4f54-a78d-1945d691ccea">|

<details>
  <summary> a Particle System with a Repeller Modificado</summary>

#### 5.  a Particle System with a Repeller Modificado

</details>

|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/e868d5d8-5495-4295-91e9-561cf48002d6">|<img width="400" src="https://github.com/user-attachments/assets/0d5a3814-883d-4f54-a78d-1945d691ccea">|

--- 

## Apply: Aplicación 🛠

### Actividad 03

Es hora de una nueva creación. Diseña e implementa una obra de arte generativa algorítmica interactiva en tiempo real en p5.js que cumpla con los siguientes requisitos:

Documenta el proceso de creación, incluyendo la idea inicial, bocetos, experimentación con el código y el resultado final.

1. Es unidad incluye una novedad: DISEÑO. Debes intencionar tu obra. Esta vez te pediré que DISEÑES antes de generar código. Define un concepto, haz bocetos, define la interacción, etc. ¿Cuál es el concepto de tu obra? ¿Qué quieres comunicar con ella?



2. Debes utilizar los conceptos de herencia y polimorfismo que revisaste en la fase de investigación.



3. Debes utilizar al menos un concepto de cada una de las unidades anteriores: 4 conceptos.



4. Debes definir cómo vas a gestionar el tiempo de vida de las partículas y la memoria.



5. La obra debe ser interactiva en tiempo real. Puedes usar teclado, mouse, música, el micrófono, video, sensor o cualquier otro dispositivo de entrada.



6. Incluye un enlace a tu código en el editor de p5.js.



7. Incluye el código fuente.



8. Captura de pantallas de tu obra con las imágenes que más te gusten


## Reflect: Consolidación y metacognición 🤔

Una vez termines esta unidad invierte en ti unos minutos para reflexionar sobre tu proceso de aprendizaje.

1. Realiza un diagrama conceptual donde incluyas todos los conceptos que has aprendido en las unidades 1 a 5.



2. ¿Qué has venido haciendo bien en tu proceso durante el curso que debas mantener en la próxima unidad?



3. ¿Qué has venido haciendo mal en tu proceso durante el curso que debas cambiar en la próxima unidad?
