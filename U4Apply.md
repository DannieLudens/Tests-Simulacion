# Unidad 4

## 🛠 Fase: Apply

**Obra de arte generativa algorítmica interactiva en tiempo real**



Diseña e implementa una obra de arte generativa algorítmica interactiva en tiempo real en p5.js que cumpla con los siguientes requisitos:

- Selecciona uno de los conceptos con los que experimentaste en la fase de investigación y propón la obra alrededor de este.
  > Ondas Sinusoidales y Análisis de Amplitud de Audio


- Incorpora en tu obra al menos un concepto de cada una de las unidades 1, 2 y 3.
- La obra debe ser interactiva en tiempo real. Puedes usar teclado, mouse, música, el micrófono, video, sensor o cualquier otro dispositivo de entrada.

### Explicación conceptual de la obra

<img width="500" src="https://github.com/user-attachments/assets/3eec79a0-4c10-42f4-9da1-988d4a46ff8c">

El concepto central de esta obra es la **reactividad sonora mediante análisis de amplitud de ondas de audio**, donde:

- La música no solo se escucha, sino que se **visualiza** a través del comportamiento de las partículas
- Las **ondas sinusoidales** del audio se analizan en tiempo real usando FFT (Fast Fourier Transform)
- La **amplitud** de la onda controla el tamaño (radio) de las partículas estrelladas
- Se visualiza la forma de onda en un círculo que sigue al cursor

**Nota sobre el concepto original**: Inicialmente consideré usar "atracción al click del mouse" como en la experimentacion que hice de "ramitas" y repulsión de particulas a la silueta capturando el frame difference de la camara, pero el proyecto evolucionó hacia algo menos complejo e interesante: un sistema no solo para dibujar un trazo y cada trazo repeler las particulas tambien considere un "easter egg" donde el **Nyan Cat persigue al mouse** (steering behavior) mientras las partículas **huyen** tanto del gato como de su rastro arcoíris. Esto aplica fuerzas de atracción Y repulsión simultáneamente.

---

**Referentes:**

<details>
  <summary>Ver Aquí</summary>


> [SuperRadiance](https://superradiance.art/) donde las particulas interactuan con el movimiento o son generadas por el mismo movimiento

<img width="300" src="https://github.com/user-attachments/assets/bc28cc6c-2c36-4991-8f67-02aad9191c62" />

> [Pendulum Waves](https://youtu.be/GqVyz-8AGcA?si=2Vg0hBLbF9yeR8GQ) donde se genera sonido segun un comportamiento visual

<img width="300"  src="https://github.com/user-attachments/assets/61e7cc8f-f953-43ba-bf4e-1052dd43fd05" />

> [Audio Visualizer](https://www.youtube.com/watch?v=uk96O7N1Yo0&pp=ygUTcmVhY3RpdmUgc291bmQgcDVqcw%3D%3D) Como visualizar la forma de onda

<img width="300"  src="https://github.com/user-attachments/assets/daf7a7bc-b5af-46f0-8aee-d1cace46961f" />

</details>

---

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?

<details>
  <summary>Tu respuesta aquí:</summary>

> Funciones sinusoides dependiendo de la amplitud de la onda de la cancion las perticulas aumentan o disminuyen su tamaño(radio)
>
> **Análisis de amplitud de ondas sinusoidales y oscilación reactiva**.
> 
> El concepto de **onda sinusoidal** es fundamental: el audio es una onda que oscila, y esa oscilación se traduce visualmente en el crecimiento y decrecimiento de las partículas estrelladas, creando una conexión directa entre sonido y forma.
>
> Utilicé análisis de audio en tiempo real mediante `p5.sound.js`:
>
> **1. Análisis de amplitud** (`sketch.js`, líneas 86-90):
> - `amplitude.getLevel()` analiza la potencia de la onda de audio
> - Retorna un valor entre 0 y 1 que representa la intensidad del sonido
> - Lo amplifico por 2.5 para mayor efecto visual
>
> **2. Oscilación del tamaño de partículas** (`particle.js`, líneas 141-151):
> - El tamaño base se multiplica por un factor que varía de 0.8x a 6x
> - Uso `lerp()` para suavizar las transiciones y evitar saltos bruscos
> - Las partículas "pulsan" al ritmo de la música
>
> **3. Visualización de waveform** (`sketch.js`, líneas 261-289):
> - FFT descompone la onda en sus componentes de frecuencia
> - La visualizo en forma circular alrededor del cursor
> - El radio varía según la amplitud de cada punto de la onda

</details>

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?

<details>
  <summary>Tu respuesta aquí:</summary>
  
> **Steering Behaviors: Seek (perseguir) y Flee (huir)**.
> 
> Estos comportamientos crean una dinámica emergente donde las partículas "rodean" los obstáculos, creando patrones visuales complejos sin programación explícita de rutas. Es como si las partículas tuvieran "instinto de supervivencia".
>
> Implementé dos comportamientos opuestos:
>
> **1. SEEK - El Nyan Cat persigue al mouse** (`nyancat.js`, líneas 32-40):
> - Calcula el vector deseado desde su posición al objetivo (mouse)
> - Calcula la fuerza de dirección (steering): `deseado - velocidad_actual`
> - Esta fuerza hace que el gato "gire" suavemente hacia el mouse
>
> **2. FLEE - Las partículas huyen del Nyan Cat** (`particle.js`, líneas 93-138):
> - Calculan la distancia al gato y su rastro
> - Si están muy cerca, crean un vector de escape en dirección opuesta
> - La fuerza es inversamente proporcional a la distancia (más cerca = más fuerza)
> - Las partículas también huyen de los trazos pintados con el mismo principio (líneas 52-91)
>

</details>



* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?

<details>
  <summary>Tu respuesta aquí:</summary>


> **Vectores para representar física de movimiento (Motion 101)**.
>
> Utilicé vectores `p5.Vector` para modelar la física de cada partícula con tres propiedades fundamentales: posición (`pos`), velocidad (`vel`) y aceleración (`acc`). Implementé el algoritmo básico de movimiento en el método `update()` (`particle.js`, líneas 116-121):
>
> ```
> velocidad = velocidad + aceleración
> posición = posición + velocidad
> aceleración = 0
> ```
>
> Este concepto también se aplica al Nyan Cat (`nyancat.js`, líneas 5-7, 48-56), que utiliza el mismo sistema vectorial para perseguir al mouse. Los vectores permiten operar matemáticamente con el movimiento: sumar fuerzas, calcular direcciones, normalizar vectores, etc. Es la base fundamental sobre la que se construye toda la física de la obra.
>
> **Acumulación de fuerzas en la aceleración**.
> 
> Estas fuerzas se acumulan en la aceleración durante cada frame, y luego en el método `update()` la aceleración modifica la velocidad, y la velocidad modifica la posición. Al final del frame, la aceleración se resetea a cero(como hemos venido estudiandolo). Este enfoque permite combinar múltiples influencias de forma realista, simulando la Segunda Ley de Newton (F = ma).
>
> Implementé el principio de que las fuerzas NO modifican directamente la velocidad, sino que se acumulan en la **aceleración**. En el método `applyForce()` (`particle.js`, líneas 36-38), cada fuerza se suma a la aceleración con `this.acc.add(force)`.
>
> En el draw loop (`sketch.js`, líneas 95-105), aplico múltiples fuerzas a cada partícula:
> 1. **Fuerza de Perlin Noise**: Comportamiento orgánico base
> 2. **Fuerza de repulsión**: De los trazos pintados o del Nyan Cat
>
</details>



* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?

<details>
  <summary>Tu respuesta aquí:</summary>


> **Ruido Perlin para movimiento orgánico no repetitivo**.
>
> Esto crea un movimiento fluido y natural que simula fluidos o campos magnéticos, muy diferente al movimiento lineal o completamente aleatorio. Las partículas "fluyen" por el canvas de manera coherente pero impredecible, lo que da vida y naturalidad a la obra.
>
> Implementé el ruido de Perlin en el método `defaultBehavior()` de cada partícula (`particle.js`, líneas 40-48). Cada partícula tiene offsets únicos (`noiseOffsetX`, `noiseOffsetY`) que generan valores de ruido basados en su posición espacial (x, y) y temporal (frameCount). El ruido se convierte en ángulos de dirección que producen un campo de fuerzas orgánico.
>
</details>


---

### ¿Cómo resolviste la interacción?

> **Evolución del concepto original:**
> 
> Inicialmente quería fusionar visión artificial (frame difference y captura de video) con la simulación de partículas, donde la silueta del usuario repelería las partículas. Sin embargo, como no domino completamente esas técnicas y considerando el tiempo disponible, decidí trabajar desde lo que conozco bien de la materia de simulación, creando algo incluso más interesante.

<details>
  <summary>Tu respuesta aquí:</summary>
  
> **Interacción con dos modos: Pincel y Nyan Cat**.
>
> <img width="400" src="https://github.com/user-attachments/assets/6b398e26-7432-4dcd-95dc-2b5e90243d61">
>
> **Solución implementada:**
>
> **1. Modo Pincel (por defecto)**:
> - El usuario dibuja trazos con el mouse arrastrando
> - Los trazos tienen colores arcoíris que cambian progresivamente (recorren el espectro HSB)
> - Los trazos se desvanecen gradualmente con el tiempo
> - Las partículas aplican fuerzas de repulsión para evitar los trazos
> - Control de grosor con scroll del mouse
> - Indicador visual del tamaño del pincel
>
>   <img width="500" src="https://github.com/user-attachments/assets/6e8bdfa3-0dc5-434c-a1f3-61942cf72a1f">
>
> **2. Modo Nyan Cat (tecla N)**:
> - El gato aparece y persigue al mouse con steering behavior
> - Deja un rastro arcoíris automático que se desvanece progresivamente (FIFO)
> - Las partículas huyen tanto del cuerpo del gato como de su rastro
> - Control de tamaño del gato y rastro con scroll
> - Visualización de waveform circular alrededor del cursor
>
>   <img width="500" src="https://github.com/user-attachments/assets/ce8757e3-40b7-47f7-a93f-230bc43f069f">
>
> **3. Audio reactivo (ambos modos)**:
> - La amplitud de la música controla el tamaño de las 250 partículas estrelladas
> - Usuario puede cargar cualquier canción (formato MP3, WAV, etc.)
> - Canción por defecto: "L'Amour Toujours" de Gigi D'Agostino
> - Controles completos: Play/Pause, Stop, Volumen
> - Sin auto-play: el usuario decide cuándo empezar
>
>   <img width="500" src="https://github.com/user-attachments/assets/bdf15471-afab-445b-aceb-db2afdcaf095">
> 

  
</details>

---

### Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/DanieLudens/sketches/s93Z9A63L)

---

### Código de la obra 

<details>
  <summary>index.html</summary><br>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.10/lib/p5.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.10/lib/addons/p5.sound.min.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />
  </head>
  <body>
    <main>
    </main>
    <script src="stroke.js"></script>
    <script src="particle.js"></script>
    <script src="nyancat.js"></script>
    <script src="sketch.js"></script>
  </body>
</html>

```
</details>

<details>
  <summary>style.css</summary><br>

```css
html, body {
  margin: 0;
  padding: 0;
  background: #0a0a0a;
  font-family: 'Courier New', monospace;
}

canvas {
  display: block;
}

main {
  position: relative;
}

/* Estilo para los sliders */
input[type="range"] {
  -webkit-appearance: none;
  appearance: none;
  background: rgba(0, 255, 255, 0.2);
  outline: none;
  border-radius: 5px;
  height: 6px;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 16px;
  height: 16px;
  background: cyan;
  cursor: pointer;
  border-radius: 50%;
}

input[type="range"]::-moz-range-thumb {
  width: 16px;
  height: 16px;
  background: cyan;
  cursor: pointer;
  border-radius: 50%;
  border: none;
}

```
</details>



<details>
  <summary>sketch.js</summary><br>

```js
const CONFIG = {
  CANVAS_WIDTH: 800,
  CANVAS_HEIGHT: 600,
  NUM_PARTICLES: 250,
  TARGET_FPS: 60
};

let particles = [];
let strokes = []; // Array de trazos pintados
let currentStroke = null; // Trazo actual mientras se dibuja
let isDrawing = false;

// Audio
let song;
let amplitude;
let fft;
let audioLoaded = false;
let isPlaying = false;

// Controles UI
let brushSizeSlider;
let brushSizeLabel;
let volumeSlider;
let playButton;
let pauseButton;
let stopButton;
let audioInput;

let brushSize = 20;
let currentHue = 0; // Para efecto arcoíris

let nyanCat;
let nyanCatImg;

function preload() {
  nyanCatImg = loadImage('nyanCat.png');
}

function setup() {
  let canvas = createCanvas(CONFIG.CANVAS_WIDTH, CONFIG.CANVAS_HEIGHT);
  canvas.position(0, 0);
  frameRate(CONFIG.TARGET_FPS);
  
  // Crear partículas
  for (let i = 0; i < CONFIG.NUM_PARTICLES; i++) {
    particles.push(new Particle(random(width), random(height)));
  }
  
  // Crear Nyan Cat
  nyanCat = new NyanCat(width/2, height/2, nyanCatImg);
  
  // Configurar audio
  amplitude = new p5.Amplitude();
  amplitude.smooth(0.7);
  fft = new p5.FFT(0.7, 512);
  
  // Cargar canción por defecto
  loadDefaultSong();
  
  // Crear controles UI
  createUIControls();
}

function draw() {
  background(0);
  
  // 1. Obtener nivel de audio
  let audioLevel = 0;
  if (audioLoaded && isPlaying) {
    audioLevel = amplitude.getLevel() * 2.5; // Amplificación
    audioLevel = constrain(audioLevel, 0, 1);
  }
  
  // 2. Actualizar Nyan Cat
  if (nyanCat.isActive) {
    nyanCat.update(createVector(mouseX, mouseY));
  }
  
  // 3. Actualizar y dibujar trazos (solo si Nyan Cat está inactivo)
  if (!nyanCat.isActive) {
    updateAndDisplayStrokes();
  }
  
  // 4. Actualizar y dibujar partículas con blend mode ADD para efecto de brillo
  blendMode(ADD);
  for (let particle of particles) {
    // Aplicar comportamiento por defecto (Perlin Noise)
    let noiseForce = particle.defaultBehavior();
    particle.applyForce(noiseForce);
    
    // Aplicar repulsión de trazos o del Nyan Cat
    if (nyanCat.isActive) {
      let avoidNyan = particle.avoidNyanCat(nyanCat);
      particle.applyForce(avoidNyan);
    } else {
      let avoidForce = particle.avoidStrokes(strokes);
      particle.applyForce(avoidForce);
    }
    
    // Actualizar tamaño según audio
    particle.updateAudioSize(audioLevel);
    
    // Actualizar física
    particle.update();
    particle.edges();
    particle.display();
  }
  blendMode(BLEND);
  
  // 5. Dibujar Nyan Cat con su rastro
  nyanCat.display();
  
  // 6. Dibujar trazo actual mientras se pinta (modo pincel)
  if (isDrawing && currentStroke && !nyanCat.isActive) {
    currentStroke.display();
  }
  
  // 7. Dibujar interfaz de información
  drawUI();
  
  // 8. Dibujar waveform circular si hay audio (alrededor del cursor) - solo si Nyan Cat inactivo
  if (audioLoaded && isPlaying && mouseX >= 0 && mouseX <= width && mouseY >= 0 && mouseY <= height && !nyanCat.isActive) {
    drawWaveform();
  }
  
  // 9. Dibujar indicador de tamaño del pincel - solo si Nyan Cat inactivo
  if (mouseX >= 0 && mouseX <= width && mouseY >= 0 && mouseY <= height && !nyanCat.isActive) {
    drawBrushIndicator();
  }
}

// FUNCIONES DE TRAZOS
function updateAndDisplayStrokes() {
  // Actualizar y dibujar trazos, eliminar los que ya se desvanecieron
  for (let i = strokes.length - 1; i >= 0; i--) {
    strokes[i].update();
    strokes[i].display();
    
    if (!strokes[i].isAlive) {
      strokes.splice(i, 1);
    }
  }
}

function mousePressed() {
  // Solo dibujar si el mouse está dentro del canvas y Nyan Cat está inactivo
  if (mouseX >= 0 && mouseX <= width && mouseY >= 0 && mouseY <= height && !nyanCat.isActive) {
    isDrawing = true;
    currentStroke = new Stroke(brushSize);
    currentStroke.addPoint(mouseX, mouseY, currentHue);
  }
}

function mouseDragged() {
  if (isDrawing && currentStroke && !nyanCat.isActive) {
    // Avanzar el tono para efecto arcoíris ANTES de agregar el punto
    currentHue = (currentHue + 2) % 360; // Incremento de 2 para cambios más visibles
    currentStroke.addPoint(mouseX, mouseY, currentHue);
  }
}

function mouseReleased() {
  if (isDrawing && currentStroke) {
    // Guardar el trazo completo
    strokes.push(currentStroke);
    currentStroke = null;
    isDrawing = false;
  }
}

// Control de scroll del mouse (rueda)
function mouseWheel(event) {
  if (nyanCat.isActive) {
    // Cambiar tamaño del Nyan Cat y su rastro
    nyanCat.changeScale(-event.delta / 1000);
    nyanCat.changeTrailThickness(-event.delta / 100);
  } else {
    // Cambiar tamaño del pincel
    brushSize += -event.delta / 50;
    brushSize = constrain(brushSize, 5, 50);
    updateBrushSizeLabel();
    brushSizeSlider.value(brushSize);
  }
  return false; // Prevenir scroll de página
}

// Control de teclado
function keyPressed() {
  if (key === 'n' || key === 'N') {
    nyanCat.toggle();
    console.log(`Nyan Cat: ${nyanCat.isActive ? 'ACTIVADO 🐱🌈' : 'DESACTIVADO'}`);
  }
}

// FUNCIONES DE AUDIO
function loadDefaultSong() {
  song = loadSound('L AMOUR TOUJOURS - GIGI D AGOSTINO.mp3', 
    () => {
      amplitude.setInput(song);
      fft.setInput(song);
      audioLoaded = true;
      isPlaying = false;
      console.log("✓ Canción cargada correctamente");
    },
    () => {
      console.log("⚠ Error al cargar la canción por defecto");
    }
  );
}

function handleFile(file) {
  if (file.type === 'audio') {
    if (song && isPlaying) {
      song.stop();
    }
    song = loadSound(file.data, () => {
      amplitude.setInput(song);
      fft.setInput(song);
      audioLoaded = true;
      isPlaying = false;
      playButton.html('▶ Play');
      console.log("✓ Nueva canción cargada");
    });
  }
}

function togglePlay() {
  if (!audioLoaded || !song) return;
  
  if (isPlaying) {
    song.pause();
    playButton.html('▶ Play');
    isPlaying = false;
  } else {
    song.loop();
    playButton.html('⏸ Pause');
    isPlaying = true;
  }
}

function stopAudio() {
  if (song && audioLoaded) {
    song.stop();
    isPlaying = false;
    playButton.html('▶ Play');
  }
}

function updateVolume() {
  if (song && audioLoaded) {
    let vol = volumeSlider.value();
    song.setVolume(vol);
  }
}

// ========================================
// VISUALIZACIÓN DE WAVEFORM
// ========================================
function drawWaveform() {
  let waveform = fft.waveform();
  
  push();
  translate(mouseX, mouseY);
  
  // Fondo circular semi-transparente
  fill(0, 0, 0, 100);
  noStroke();
  circle(0, 0, 160);
  
  // Dibujar waveform en forma circular
  noFill();
  stroke(0, 255, 255, 200);
  strokeWeight(2);
  beginShape();
  for (let i = 0; i < waveform.length; i++) {
    let angle = map(i, 0, waveform.length, 0, TWO_PI);
    let radius = map(waveform[i], -1, 1, 50, 80);
    let x = radius * cos(angle);
    let y = radius * sin(angle);
    vertex(x, y);
  }
  endShape(CLOSE);
  
  // Círculo interior de referencia
  noFill();
  stroke(0, 255, 255, 50);
  strokeWeight(1);
  circle(0, 0, 100);
  
  pop();
}

// ========================================
// INTERFAZ DE USUARIO
// ========================================
function createUIControls() {
  let controlsY = CONFIG.CANVAS_HEIGHT + 20;
  
  // Slider de grosor del pincel
  let brushLabel = createDiv('Grosor del pincel:');
  brushLabel.position(20, controlsY);
  brushLabel.style('color', 'white');
  brushLabel.style('font-family', 'monospace');
  
  brushSizeSlider = createSlider(5, 50, 20, 1);
  brushSizeSlider.position(20, controlsY + 25);
  brushSizeSlider.style('width', '200px');
  brushSizeSlider.input(() => {
    brushSize = brushSizeSlider.value();
    updateBrushSizeLabel();
  });
  
  // Label que muestra el valor actual del grosor
  brushSizeLabel = createDiv(`Tamaño: ${brushSize}px`);
  brushSizeLabel.position(230, controlsY + 25);
  brushSizeLabel.style('color', 'cyan');
  brushSizeLabel.style('font-family', 'monospace');
  brushSizeLabel.style('font-weight', 'bold');
  
  // Selector de archivo de audio
  audioInput = createFileInput(handleFile);
  audioInput.position(20, controlsY + 60);
  audioInput.style('background-color', 'rgba(0, 0, 0, 0.7)');
  audioInput.style('color', 'white');
  audioInput.style('padding', '8px');
  audioInput.style('border', '1px solid cyan');
  audioInput.style('border-radius', '5px');
  audioInput.attribute('accept', 'audio/*');
  
  // Botones de control de audio
  playButton = createButton('▶ Play');
  playButton.position(320, controlsY + 60);
  styleButton(playButton, 'rgba(0, 255, 0, 0.7)', 'lime');
  playButton.mousePressed(togglePlay);
  
  stopButton = createButton('⬛ Stop');
  stopButton.position(420, controlsY + 60);
  styleButton(stopButton, 'rgba(255, 0, 0, 0.7)', 'red');
  stopButton.mousePressed(stopAudio);
  
  // Slider de volumen
  let volumeLabel = createDiv('Volumen:');
  volumeLabel.position(540, controlsY + 60);
  volumeLabel.style('color', 'white');
  volumeLabel.style('font-family', 'monospace');
  
  volumeSlider = createSlider(0, 1, 0.5, 0.01);
  volumeSlider.position(620, controlsY + 65);
  volumeSlider.style('width', '150px');
  volumeSlider.input(updateVolume);
}

function styleButton(button, bgColor, borderColor) {
  button.style('background-color', bgColor);
  button.style('color', 'white');
  button.style('padding', '8px 16px');
  button.style('border', `1px solid ${borderColor}`);
  button.style('border-radius', '5px');
  button.style('cursor', 'pointer');
  button.style('font-family', 'monospace');
}

function drawUI() {
  // Información en pantalla
  fill(255);
  textSize(14);
  textAlign(LEFT);
  text(`FPS: ${floor(frameRate())}`, 10, 20);
  text(`Partículas: ${particles.length}`, 10, 40);
  text(`Trazos activos: ${strokes.length}`, 10, 60);
  
  if (isPlaying) {
    fill(0, 255, 0);
    text('🎵 Reproduciendo', 10, 80);
  } else {
    fill(255, 100, 100);
    text('⏸ Audio pausado', 10, 80);
  }
  
  // Estado del Nyan Cat
  if (nyanCat.isActive) {
    fill(255, 150, 255);
    text('🐱 Nyan Cat ACTIVO - Scroll: Tamaño', 10, 100);
    text(`Rastro: ${nyanCat.trail.length} puntos`, 10, 120);
  } else {
    fill(150, 150, 150);
    text('Presiona [N] easter egg Nyan Cat', 10, 100);
  }
  
  // Instrucciones
  textAlign(CENTER);
  fill(100, 200, 255);
  textSize(16);
  if (nyanCat.isActive) {
    text('Nyan Cat persigue el mouse y deja rastro arcoíris 🌈', width / 2, height - 10);
  } else {
    text('Dibuja con el mouse para crear trazos que repelen las partículas', width / 2, height - 10);
  }
}

// Actualizar el label del tamaño del pincel
function updateBrushSizeLabel() {
  brushSizeLabel.html(`Tamaño: ${brushSize}px`);
}

// Dibujar indicador visual del tamaño del pincel
function drawBrushIndicator() {
  push();
  noFill();
  stroke(255, 255, 255, 150);
  strokeWeight(2);
  circle(mouseX, mouseY, brushSize);
  
  // Punto central
  fill(255, 255, 255, 100);
  noStroke();
  circle(mouseX, mouseY, 3);
  pop();
}
```
</details>

<details>
  <summary>stroke.js</summary><br>

```js
class Stroke {
  constructor(thickness) {
    this.points = []; // Ahora cada punto guardará {x, y, hue}
    this.thickness = thickness;
    this.alpha = 255; // Opacidad inicial
    this.fadeSpeed = 0.5; // Velocidad de desvanecimiento
    this.isAlive = true;
  }
  
  // Agregar un punto al trazo con su color
  addPoint(x, y, hue) {
    this.points.push({ x: x, y: y, hue: hue });
  }
  
  // Actualizar el trazo (desvanecimiento)
  update() {
    this.alpha -= this.fadeSpeed;
    if (this.alpha <= 0) {
      this.alpha = 0;
      this.isAlive = false;
    }
  }
  
  // Dibujar el trazo con colores arcoíris 
  display() {
    if (this.points.length < 2) return;
    
    push(); // Guardar estado
    colorMode(HSB, 360, 100, 100, 255);
    strokeWeight(this.thickness);
    noFill();
    
    // Dibujar línea entre cada par de puntos con su color
    for (let i = 0; i < this.points.length - 1; i++) {
      let p1 = this.points[i];
      let p2 = this.points[i + 1];
      
      // Usar el color del primer punto del segmento
      stroke(p1.hue, 80, 100, this.alpha);
      line(p1.x, p1.y, p2.x, p2.y);
    }
    
    pop(); // Restaurar estado
  }
}

```
</details>

<details>
  <summary>particle.js</summary><br>

```js
class Particle {
  constructor(x, y) {
    // Vectores de física (motion 101)
    this.pos = createVector(x, y);
    this.vel = createVector(random(-1, 1), random(-1, 1));
    this.acc = createVector(0, 0);
    
    // Propiedades de movimiento (Unidad 2 y 3)
    this.maxSpeed = 3;
    this.maxForce = 0.5;
    
    // Propiedades visuales y audio reactivo
    this.baseSize = random(3, 6);
    this.size = this.baseSize;
    this.targetSize = this.baseSize;
    
    // Color espacial (cyan y violeta) - Guardamos valores HSB
    const isCyan = random() < 0.5;
    this.hue = isCyan ? random(180, 200) : random(260, 300);
    this.saturation = random(70, 100);
    this.brightness = 100;
    this.alpha = random(60, 90);
    
    // Offset para ruido Perlin único por partícula
    this.noiseOffsetX = random(1000);
    this.noiseOffsetY = random(1000);
    
    // Propiedades de la forma estrellada
    this.numPoints = 8; // 8 puntas de estrella
    this.rotation = random(TWO_PI); // Rotación inicial aleatoria
    this.rotationSpeed = random(-0.02, 0.02); // Velocidad de rotación
  }
  
  // Aplicar fuerza
  applyForce(force) {
    this.acc.add(force);
  }
  
  // Comportamiento Perlin Noise
  defaultBehavior() {
    let angle = noise(
      this.pos.x * 0.01 + this.noiseOffsetX, 
      this.pos.y * 0.01 + this.noiseOffsetY, 
      frameCount * 0.005
    ) * TWO_PI * 2;
    
    let force = p5.Vector.fromAngle(angle);
    force.setMag(0.1);
    return force;
  }
  
  // Repulsión de trazos pintados
  avoidStrokes(strokes) {
    if (strokes.length === 0) return createVector(0, 0);
    
    let avoidForce = createVector(0, 0);
    let count = 0;
    
    // Revisar cada trazo activo
    for (let stroke of strokes) {
      for (let point of stroke.points) {
        // Calcular distancia a cada punto del trazo
        let d = dist(this.pos.x, this.pos.y, point.x, point.y);
        let avoidRadius = stroke.thickness + 20; // Radio de repulsión
        
        if (d < avoidRadius && d > 0.1) { // Evitar división por cero
          // Crear fuerza de repulsión (convertir point a vector)
          let pointVec = createVector(point.x, point.y);
          let diff = p5.Vector.sub(this.pos, pointVec);
          
          // Verificar que diff tenga magnitud antes de normalizar
          if (diff.mag() > 0) {
            diff.normalize();
            // Fuerza inversamente proporcional a la distancia
            let strength = map(d, 0, avoidRadius, 2, 0);
            diff.mult(strength);
            avoidForce.add(diff);
            count++;
          }
        }
      }
    }
    
    if (count > 0) {
      avoidForce.div(count);
      // Solo aplicar steering si hay fuerza
      if (avoidForce.mag() > 0) {
        avoidForce.setMag(this.maxSpeed);
        avoidForce.sub(this.vel);
        avoidForce.limit(this.maxForce * 1.5); // Fuerza más fuerte para repulsión
      }
    }
    
    return avoidForce;
  }
  
  // Repulsión del Nyan Cat
  avoidNyanCat(nyanCat) {
    if (!nyanCat.isActive) return createVector(0, 0);
    
    let avoidForce = createVector(0, 0);
    
    // Repeler del cuerpo del gato
    let catBounds = nyanCat.getBounds();
    let catCenter = createVector(nyanCat.pos.x, nyanCat.pos.y);
    let d = dist(this.pos.x, this.pos.y, catCenter.x, catCenter.y);
    let avoidRadius = max(catBounds.width, catBounds.height) / 2 + 30;
    
    if (d < avoidRadius && d > 0.1) {
      let diff = p5.Vector.sub(this.pos, catCenter);
      if (diff.mag() > 0) {
        diff.normalize();
        let strength = map(d, 0, avoidRadius, 3, 0);
        diff.mult(strength);
        avoidForce.add(diff);
      }
    }
    
    // Repeler del rastro arcoíris
    for (let point of nyanCat.trail) {
      let d = dist(this.pos.x, this.pos.y, point.x, point.y);
      let trailRadius = nyanCat.trailThickness + 20;
      
      if (d < trailRadius && d > 0.1) {
        let pointVec = createVector(point.x, point.y);
        let diff = p5.Vector.sub(this.pos, pointVec);
        
        if (diff.mag() > 0) {
          diff.normalize();
          let strength = map(d, 0, trailRadius, 2, 0);
          diff.mult(strength);
          avoidForce.add(diff);
        }
      }
    }
    
    // Aplicar steering si hay fuerza
    if (avoidForce.mag() > 0) {
      avoidForce.setMag(this.maxSpeed);
      avoidForce.sub(this.vel);
      avoidForce.limit(this.maxForce * 2); // Fuerza fuerte para el gato
    }
    
    return avoidForce;
  }
  
  // Actualizar tamaño según audio 
  updateAudioSize(audioLevel) {
    if (audioLevel > 0) {
      // Mapear nivel de audio a multiplicador de tamaño
      this.targetSize = this.baseSize * map(audioLevel, 0, 1, 0.8, 6);
      // Suavizado con lerp para transiciones fluidas
      this.size = lerp(this.size, this.targetSize, 0.3);
    } else {
      // Sin audio, volver al tamaño base
      this.size = lerp(this.size, this.baseSize, 0.1);
    }
  }
  
  // Actualizar física (motion101)
  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0); // Resetear aceleración
  }
  
  // Wrapping en los bordes del canvas
  edges() {
    if (this.pos.x > width) this.pos.x = 0;
    else if (this.pos.x < 0) this.pos.x = width;
    
    if (this.pos.y > height) this.pos.y = 0;
    else if (this.pos.y < 0) this.pos.y = height;
  }
  
  // Dibujar la partícula como estrella pulsante
  display() {
    push(); // Guardar estado
    
    // Actualizar rotación
    this.rotation += this.rotationSpeed;
    
    translate(this.pos.x, this.pos.y);
    rotate(this.rotation);
    
    colorMode(HSB, 360, 100, 100, 100);
    fill(this.hue, this.saturation, this.brightness, this.alpha);
    noStroke();
    
    // Dibujar estrella con puntas que pulsan
    beginShape();
    for (let i = 0; i < this.numPoints * 2; i++) {
      let angle = map(i, 0, this.numPoints * 2, 0, TWO_PI);
      let radius;
      
      if (i % 2 === 0) {
        // Puntas externas (pulsan con el audio)
        radius = this.size;
      } else {
        // Puntas internas (más pequeñas)
        radius = this.size * 0.4;
      }
      
      let x = radius * cos(angle);
      let y = radius * sin(angle);
      vertex(x, y);
    }
    endShape(CLOSE);
    
    pop(); // Restaurar estado
  }
}

```
</details>

<details>
  <summary>nyancat.js</summary><br>

```js
class NyanCat {
  constructor(x, y, img) {
    // Vectores de física (motion 101)
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    
    // Propiedades de movimiento
    this.maxSpeed = 5;
    this.maxForce = 0.3;
    
    // Imagen del gato
    this.img = img;
    this.scale = 0.2; // Escala inicial (20% del tamaño original)
    this.minScale = 0.1;
    this.maxScale = 0.5;
    
    // Rotación
    this.angle = 0;
    
    // Rastro arcoíris (puntos con colores)
    this.trail = [];
    this.maxTrailLength = 150; // Longitud máxima del rastro
    this.currentHue = 0; // Color actual del rastro
    this.trailThickness = 15; // Grosor del rastro
    
    // Estado
    this.isActive = false;
  }
  
  // Perseguir el mouse (steering behavior)
  seek(target) {
    let desired = p5.Vector.sub(target, this.pos);
    desired.setMag(this.maxSpeed);
    
    let steer = p5.Vector.sub(desired, this.vel);
    steer.limit(this.maxForce);
    
    return steer;
  }
  
  // Actualizar física y rastro
  update(mousePos) {
    if (!this.isActive) return;
    
    // Aplicar fuerza hacia el mouse
    let seekForce = this.seek(mousePos);
    this.acc.add(seekForce);
    
    // Actualizar velocidad y posición
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);
    
    // Calcular ángulo de rotación según la velocidad
    if (this.vel.mag() > 0.1) {
      this.angle = this.vel.heading();
    }
    
    // Agregar punto al rastro si el gato se está moviendo
    if (this.vel.mag() > 0.5) {
      this.trail.push({
        x: this.pos.x,
        y: this.pos.y,
        hue: this.currentHue,
        alpha: 255
      });
      
      // Avanzar color arcoíris
      this.currentHue = (this.currentHue + 3) % 360;
      
      // Limitar longitud del rastro (FIFO)
      if (this.trail.length > this.maxTrailLength) {
        this.trail.shift(); // Eliminar el punto más viejo
      }
    }
    
    // Desvanecer rastro progresivamente
    this.updateTrail();
  }
  
  // Actualizar desvanecimiento del rastro (de atrás hacia adelante)
  updateTrail() {
    for (let i = 0; i < this.trail.length; i++) {
      // Los puntos más viejos (al inicio) se desvanecen más rápido
      let fadeAmount = map(i, 0, this.trail.length, 3, 0.5);
      this.trail[i].alpha -= fadeAmount;
    }
    
    // Eliminar puntos completamente transparentes
    this.trail = this.trail.filter(p => p.alpha > 0);
  }
  
  // Cambiar escala con scroll
  changeScale(delta) {
    this.scale += delta * 0.02;
    this.scale = constrain(this.scale, this.minScale, this.maxScale);
  }
  
  // Cambiar grosor del rastro
  changeTrailThickness(delta) {
    this.trailThickness += delta * 2;
    this.trailThickness = constrain(this.trailThickness, 5, 50);
  }
  
  // Dibujar rastro arcoíris
  drawTrail() {
    if (this.trail.length < 2) return;
    
    push();
    colorMode(HSB, 360, 100, 100, 255);
    noFill();
    
    // Dibujar línea entre cada par de puntos
    for (let i = 0; i < this.trail.length - 1; i++) {
      let p1 = this.trail[i];
      let p2 = this.trail[i + 1];
      
      // Grosor que disminuye hacia atrás
      let thickness = map(i, 0, this.trail.length, this.trailThickness * 0.5, this.trailThickness);
      strokeWeight(thickness);
      
      // Color con alpha variable
      stroke(p1.hue, 80, 100, p1.alpha);
      line(p1.x, p1.y, p2.x, p2.y);
    }
    
    pop();
  }
  
  // Dibujar el gato
  display() {
    if (!this.isActive) return;
    
    // Primero dibujar el rastro (detrás del gato)
    this.drawTrail();
    
    // Luego dibujar el gato
    push();
    translate(this.pos.x, this.pos.y);
    rotate(this.angle);
    
    // Calcular dimensiones escaladas
    let w = this.img.width * this.scale;
    let h = this.img.height * this.scale;
    
    // Dibujar imagen centrada
    imageMode(CENTER);
    image(this.img, 0, 0, w, h);
    
    pop();
  }
  
  // Obtener rectángulo de colisión para repulsión
  getBounds() {
    let w = this.img.width * this.scale;
    let h = this.img.height * this.scale;
    
    return {
      x: this.pos.x - w/2,
      y: this.pos.y - h/2,
      width: w,
      height: h
    };
  }
  
  // Activar/desactivar
  toggle() {
    this.isActive = !this.isActive;
    if (this.isActive) {
      // Al activar, posicionar cerca del mouse
      this.pos.set(mouseX, mouseY);
      this.vel.set(0, 0);
      this.trail = []; // Limpiar rastro anterior
    }
  }
  
  // Resetear posición
  reset() {
    this.pos.set(width/2, height/2);
    this.vel.set(0, 0);
    this.acc.set(0, 0);
    this.trail = [];
  }
}

```
</details>


---




### Captura de pantalla representativa



<img width="500" src="https://github.com/user-attachments/assets/0856a2a7-a8ce-46c2-b0d9-0736a39c290e">

<img width="500" src="https://github.com/user-attachments/assets/15879f0c-4e81-4005-abf2-642b548db19c">

<img width="500" src="https://github.com/user-attachments/assets/b11d60da-c93a-4ce3-b29c-d1d1b63cc3ff">

<img width="500" src="https://github.com/user-attachments/assets/22dc4921-e859-4441-b332-56cf3b7e82aa">




