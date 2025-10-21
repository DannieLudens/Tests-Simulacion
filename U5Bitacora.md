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

**Revisa y repasa algunos conceptos**

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

#### Ejemplo 4.2 - Array de Partículas (an Array of Particles)

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

**Ruido Perlin para movimiento orgánico**

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

📸 **Resultados visuales**

**visuales:**
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
  <summary>Ejemplo 4.4 - Sistema de Sistemas (a System of Systems)</summary>

#### Ejemplo 4.4 - Sistema de Sistemas (a System of Systems)

---

<details>
  <summary>🔍 Gestión de memoria</summary>

Este ejemplo introduce un concepto más complejo: **un sistema de sistemas**, o un array de emisores donde cada emisor tiene su propio array de partículas.

**1. Creación de emisores:**
```javascript
function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}
```
- Cada clic del mouse crea un **nuevo emisor** en esa posición
- Los emisores se agregan al array `emitters[]`
- Cada emisor es independiente y tiene su propia posición de origen

**2. Creación de partículas dentro de cada emisor:**
```javascript
emitter.addParticle();  // Llamado para cada emisor en draw()
```
- Cada emisor agrega partículas a su **propio** array interno `this.particles[]`
- Las partículas nacen en la posición `origin` del emisor

**3. Desaparición de partículas:**
```javascript
for (let i = this.particles.length - 1; i >= 0; i--) {
  let p = this.particles[i];
  p.run();
  if (p.isDead()) {
    this.particles.splice(i, 1);  // Elimina partícula individual
  }
}
```
- Cada emisor gestiona la eliminación de **sus propias partículas muertas**
- Se usa `splice()` al recorrer el array hacia atrás

**4. Observación:**
- **Los emisores NUNCA se eliminan**: El array `emitters[]` crece indefinidamente  
- Si haces 100 clics, tendrás 100 emisores activos
- Aunque sus partículas mueran, el emisor sigue existiendo
- Solución ideal: eliminar emisores cuando ya no tengan partículas vivas

**Diagrama de estructura:**
```
emitters[] (Array de Emisores)
   ↓
   ├─ Emitter 1
   │    └─ particles[] → [Particle, Particle, Particle...]
   │
   ├─ Emitter 2
   │    └─ particles[] → [Particle, Particle...]
   │
   └─ Emitter 3
        └─ particles[] → [Particle, Particle, Particle, Particle...]
```

**Gestión de memoria en dos niveles:**
1. **Nivel superior**: Emisores en el array global `emitters[]`
2. **Nivel inferior**: Partículas en el array interno de cada emisor `this.particles[]`

</details>

---

<details>
  <summary>🧪 Concepto aplicado: Normalización de Vectores (Unidad 2)</summary>

#### Experimento: Control de dirección con vectores normalizados

**¿Por qué elegí este concepto?**

En el ejemplo original, las partículas tienen velocidades aleatorias sin control direccional:
```javascript
this.velocity = createVector(random(-2, 2), random(-3, 0));
```

Quería que las partículas explotaran en **todas las direcciones radialmente** desde el emisor, como erupcion de volcanes reales, manteniendo velocidades consistentes.

**¿Cómo lo implementé?**

**Paso 1: Generar un vector desde un ángulo aleatorio**
```javascript
let angle = random(TWO_PI);  // Ángulo aleatorio de 0 a 360°
this.velocity = p5.Vector.fromAngle(angle);
```
- `fromAngle()` crea un vector unitario (magnitud = 1) apuntando en el ángulo especificado
- Esto garantiza que todas las partículas apunten en direcciones diferentes

**Paso 2: Normalizar para garantizar magnitud = 1**
```javascript
this.velocity.normalize();  // Asegura magnitud exactamente 1
```
- Aunque `fromAngle()` ya crea vectores normalizados, esta línea es una buena práctica
- La normalización convierte cualquier vector a magnitud 1 manteniendo su dirección

**Paso 3: Escalar a la velocidad deseada**
```javascript
this.velocity.mult(random(1, 4));  // Velocidad entre 1 y 4
```
- Multiplica el vector normalizado por un escalar
- Esto mantiene la dirección pero ajusta la rapidez

**Concepto matemático:**

Un vector normalizado tiene **magnitud = 1**:
```
v = (x, y)
magnitud = √(x² + y²) = 1

Normalización: v̂ = v / |v|
```

Esto es útil porque:
- ✅ Separa **dirección** (el vector normalizado) de **velocidad** (el escalar)
- ✅ Permite control independiente de ambos aspectos
- ✅ Evita velocidades inconsistentes por valores aleatorios extremos

**Comparación visual:**

| Sin normalización | Con normalización |
|-------------------|-------------------|
| Velocidades aleatorias en X e Y | Explosión radial uniforme |
| Algunas partículas más rápidas | Control preciso de velocidad |
| Dirección sesgada | Distribución equitativa en 360° |

**Comparación con random():**
- `random()`: Crea vectores con componentes X e Y independientes, sin control de dirección
- `fromAngle() + normalize()`: Control total sobre dirección y velocidad por separado

</details>

---

<details>
  <summary>💻 Código fuente completo</summary>

```javascript
let emitters = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  
  // Recorrer todos los emisores
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
  
  // Mostrar info
  fill(0);
  noStroke();
  text(`Emisores: ${emitters.length}`, 10, 20);
  text(`Click para crear emisor`, 10, 40);
}

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}

// ========================================
// CLASE EMITTER
// ========================================
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }
  
  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }
  
  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// ========================================
// CLASE PARTICLE CON VECTORES NORMALIZADOS
// ========================================
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    
    // 🆕 NOVEDAD: Usar normalización para control direccional
    let angle = random(TWO_PI);  // Ángulo aleatorio en 360°
    this.velocity = p5.Vector.fromAngle(angle);  // Vector unitario
    this.velocity.normalize();  // Asegurar magnitud = 1
    this.velocity.mult(random(1, 4));  // Escalar a velocidad deseada
    
    this.acceleration = createVector(0, 0.05);  // Gravedad
    this.lifespan = 255;
  }
  
  run() {
    this.update();
    this.show();
  }
  
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
  }
  
  show() {
    stroke(255, 100, 150, this.lifespan);
    strokeWeight(2);
    fill(255, 150, 200, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }
  
  isDead() {
    return this.lifespan < 0;
  }
}
```

**🔗 Enlace p5.js:** [Ver código en vivo](https://editor.p5js.org/DanieLudens/sketches/iKfXE60bT) 

</details>

---

📸 **Resultados visuales**

**visuales:**
- ✅ **Simetría radial**: Las partículas se distribuyen uniformemente en todas las direcciones
- ✅ **Control de velocidad**: Todas las partículas tienen velocidades dentro del rango especificado (1-4)
- ✅ **Efecto de fuegos artificiales**: Cada clic crea una "explosión" visualmente satisfactoria
- ✅ **Colores rosados**: Paleta diferente para distinguir este ejemplo del anterior

**Diferencias clave:**
- **Sin normalización:** Las velocidades aleatorias pueden crear sesgos direccionales
- **Con normalización:** Explosión perfectamente simétrica desde el punto de origen

</details>

|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/21a05e24-64f3-4809-81ec-ee9b94782b50">|<img width="400" src="https://github.com/user-attachments/assets/3e6148c1-0ae3-41c1-ab2f-4c9097134a4b">|





<details>
  <summary>Ejemplo 4.5 - Herencia y Polimorfismo (a Particle System with Inheritance and Polymorphism)</summary>

#### Ejemplo 4.5 - Herencia y Polimorfismo (a Particle System with Inheritance and Polymorphism)

---

<details>
  <summary>🔍 Gestión de memoria</summary>

Este ejemplo mantiene la misma gestión de memoria que ejemplos anteriores, pero introduce una diferencia importante: **un solo array contiene DOS tipos diferentes de objetos**.

**1. Creación de partículas de diferentes tipos:**
```javascript
addParticle() {
  let r = random(1);
  if (r < 0.5) {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  } else {
    this.particles.push(new Confetti(this.origin.x, this.origin.y));
  }
}
```
- 50% de probabilidad de crear una `Particle` (círculo)
- 50% de probabilidad de crear un `Confetti` (cuadrado rotado)
- Ambos tipos se agregan al **mismo array** `particles[]`

**2. Polimorfismo en el array:**
```javascript
this.particles = [Particle, Confetti, Particle, Confetti, Particle, ...];
```
- JavaScript permite mezclar tipos de objetos en un array
- Gracias a la herencia, ambos son tratados como tipo `Particle`
- Cada objeto mantiene su comportamiento único (círculos vs cuadrados)

**3. Desaparición - Sin cambios:**
```javascript
if (particle.isDead()) {
  this.particles.splice(i, 1);
}
```
- El método `isDead()` es **heredado** de la clase `Particle`
- Funciona igual para `Particle` y `Confetti`
- No importa el tipo, todos se eliminan de la misma manera

**4. Observación sobre herencia:**
La clase `Confetti` NO necesita su propio `isDead()` ni `update()`:
- ✅ **Hereda** `isDead()` de `Particle`
- ✅ **Hereda** `update()` de `Particle`
- ✅ Solo **sobrescribe** `show()` para cambiar la apariencia

**Diagrama de herencia:**
```
Particle (Clase Padre)
   ├─ position, velocity, acceleration, lifespan
   ├─ update()
   ├─ isDead()
   └─ show() → dibuja círculo
        ↓
   Confetti (Clase Hija) extends Particle
   ├─ HEREDA: position, velocity, acceleration, lifespan
   ├─ HEREDA: update(), isDead()
   └─ SOBRESCRIBE: show() → dibuja cuadrado rotado
```

</details>

---

<details>
  <summary>🧪 Concepto aplicado: Fricción/Resistencia del Aire (Unidad 3)</summary>

**Experimento: Fricción para desacelerar partículas**

**¿Por qué elegí este concepto?**

En el ejemplo original, las partículas mantienen su velocidad constante (solo afectadas por gravedad). Quería agregar **resistencia del aire** para que las partículas se desaceleren gradualmente, simulando un comportamiento más realista.

**¿Cómo lo implementé?**

La fricción es una fuerza que se opone al movimiento. Su magnitud es proporcional a la velocidad del objeto:

**Fórmula de fricción:**
```
fricción = -μ × velocidad × |velocidad|
```
Donde:
- `μ` (mu) = coeficiente de fricción
- La fricción apunta en dirección **opuesta** a la velocidad
- Es proporcional al **cuadrado** de la velocidad

**Implementación en código:**

**Paso 1: Crear el método applyFriction() en Particle**
```javascript
applyFriction() {
  let friction = this.velocity.copy();  // Copiar vector velocidad
  friction.normalize();                  // Obtener dirección (magnitud = 1)
  friction.mult(-1);                     // Invertir (opuesta al movimiento)
  
  let c = 0.01;  // Coeficiente de fricción
  let speed = this.velocity.mag();       // Obtener velocidad actual
  friction.mult(c * speed);              // Fricción proporcional a velocidad
  
  this.acceleration.add(friction);       // Aplicar como fuerza
}
```

**Explicación detallada del código:**
1. `velocity.copy()` - Copia el vector para no modificar el original
2. `normalize()` - Convierte a vector unitario (magnitud = 1) para obtener solo la dirección
3. `mult(-1)` - Invierte la dirección (fricción opuesta al movimiento)
4. `velocity.mag()` - Obtiene la magnitud/velocidad actual
5. `mult(c * speed)` - Escala la fricción proporcionalmente a la velocidad
6. `acceleration.add()` - Suma la fricción a la aceleración total

**Paso 2: Llamar applyFriction() en update()**
```javascript
update() {
  this.applyFriction();  // 1. Aplicar fricción primero
  this.velocity.add(this.acceleration);  // 2. Actualizar velocidad
  this.position.add(this.velocity);      // 3. Actualizar posición
  this.acceleration.mult(0);              // 4. Resetear aceleración
  this.lifespan -= 2;                     // 5. Reducir tiempo de vida
}
```

**Comparación visual:**

| Sin fricción | Con fricción (c = 0.01) |
|--------------|-------------------------|
| Partículas mantienen velocidad | Partículas se desaceleran gradualmente |
| Trayectorias largas y rectas | Trayectorias que se "frenan" |
| Movimiento constante | Movimiento más natural y realista |

**Nota técnica:**

La implementación actual usa fricción proporcional a la velocidad (`F = c × v`). En física real, la resistencia del aire es proporcional a `v²`. Aquí está la comparación:

```javascript
// Implementación actual (más simple)
friction.mult(c * speed);  // F ∝ v

// Implementación más realista (opcional)
friction.mult(c * speed * speed);  // F ∝ v²
```

La versión con `v²` produce una desaceleración más dramática a altas velocidades, pero puede ser visualmente menos sutil.

</details>

---

<details>
  <summary>💻 Código fuente completo</summary>

```javascript
let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 50);
}

function draw() {
  background(255);
  emitter.addParticle();
  emitter.run();
  
  // Info
  fill(0);
  noStroke();
  text(`Partículas: ${emitter.particles.length}`, 10, 20);
}

// ========================================
// CLASE EMITTER
// ========================================
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }
  
  addParticle() {
    let r = random(1);
    if (r < 0.5) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    } else {
      this.particles.push(new Confetti(this.origin.x, this.origin.y));
    }
  }
  
  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let particle = this.particles[i];
      particle.run();
      
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// ========================================
// CLASE PARTICLE CON FRICCIÓN
// ========================================
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(4, 0));  // 🆕 Velocidad inicial alta para ver fricción
    this.acceleration = createVector(0, 0.05);
    this.lifespan = 255;
  }
  
  run() {
    this.update();
    this.show();
  }
  
  // 🆕 MÉTODO DE FRICCIÓN
  applyFriction() {
    let friction = this.velocity.copy();  // Copiar el vector velocidad
    friction.normalize();                  // Convertir a vector unitario
    friction.mult(-1);                     // Invertir dirección (opuesta al movimiento)
    
    let c = 0.01;  // Coeficiente de fricción
    let speed = this.velocity.mag();       // Obtener magnitud de velocidad
    friction.mult(c * speed);              // Fricción proporcional a velocidad
    
    this.acceleration.add(friction);       // Aplicar fricción como fuerza
  }
  
  update() {
    this.applyFriction();  // 🆕 Aplicar fricción primero
    this.velocity.add(this.acceleration);  // Actualizar velocidad con aceleración
    this.position.add(this.velocity);      // Actualizar posición con velocidad
    this.acceleration.mult(0);              // Resetear aceleración para el próximo frame
    this.lifespan -= 2;                     // Reducir tiempo de vida
  }
  
  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 12);
  }
  
  isDead() {
    return this.lifespan < 0;
  }
}

// ========================================
// CLASE CONFETTI (HEREDA FRICCIÓN)
// ========================================
class Confetti extends Particle {
  constructor(x, y) {
    super(x, y);
    // Confetti automáticamente hereda applyFriction()
  }
  
  // Sobrescribe solo show() para cambiar apariencia
  show() {
    let angle = map(this.position.x, 0, width, 0, TWO_PI * 2);
    
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(175, 0, 175, this.lifespan);  // Color morado para distinguir
    
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    rectMode(CENTER);
    square(0, 0, 12);
    pop();
  }
}
```

**🔗 Enlace p5.js:** [Ver en vivo](https://editor.p5js.org/DanieLudens/sketches/Mvsl_dgqN)

</details>

---

📸 **Resultados visuales**

**visuales:**
- ✅ **Dos tipos de partículas**: Círculos grises y cuadrados morados rotados
- ✅ **Desaceleración muy visible**: Las partículas empiezan cayendo rápido y se frenan notoriamente
- ✅ **Efecto realista**: Simula resistencia del aire de manera convincente
- ✅ **Velocidad inicial alta**: Con `random(4, 0)` el efecto de fricción es dramático

**Diferencias clave:**
- **Sin fricción:** Partículas mantienen velocidad constante, caen en líneas casi rectas
- **Con fricción + velocidad alta:** Partículas se desaceleran progresivamente, creando trayectorias parabólicas naturales

</details>


|Original|Modificado|
|-----|-----|
|<img width="400" src="https://github.com/user-attachments/assets/89bd2838-e372-46b7-961d-88fe33b9aaac">|<img width="400" src="https://github.com/user-attachments/assets/0b959b23-1765-4153-a4db-4e91b777f0ac">|






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
