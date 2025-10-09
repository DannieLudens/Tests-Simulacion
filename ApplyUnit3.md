# Unidad 3


## 🛠 Fase: Apply

En esta fase, aplicaré los conceptos aprendidos creando una obra generativa interactiva en tiempo real que involucren diferentes tipos de fuerzas. Inspirada en el problema de los n-cuerpos crearé algo diferente basado en ese concepto y en las esculturas cinéticas de Alexander Calder.

Basada en la exploración que hice en la [Unidad 4 Actividad 7: repaso de conceptos de unidades anteriores: Ramitas](https://github.com/jfUPB/simulacion-2025-20-DannieLudens/blob/unidad4/reflect/unidad-4/set-seek.md)

  <img width="400" src="https://github.com/user-attachments/assets/624cfd85-98c0-4b34-a68f-ea529ecc5a20">

### Actividad 10: Problema de los N-Cuerpos y Moviles de Calder

<img width="400" src="https://github.com/user-attachments/assets/b5151d31-45d3-4bc4-91d9-771af1fa8c79"> Viento moderado y baja gravedad


<details>
  <summary>Más Muestras (Click Aquí)</summary>

<img width="400" src="https://github.com/user-attachments/assets/2bf59e8a-f824-4f36-a2a4-da36300b3360"> 2 minutos + interactividad con nodos

<img width="400" src="https://github.com/user-attachments/assets/38f8457f-55cf-4e13-9742-f87e33dd5b43"> Aumento de viento al máximo

<img width="400" src="https://github.com/user-attachments/assets/3ad7a3bb-4275-4623-b3a4-8c6495ed15b3"> Aumento de gravedad extrema

<img width="400" src="https://github.com/user-attachments/assets/0c48821c-c3cb-4db0-a881-dd7ade441781"> Limpieza de canvas para ver los trazos

</details>

<img width="600" src="https://github.com/user-attachments/assets/f9951881-a582-4271-9ed7-0b73df2e46a2"> Viento bajo y gravedad extrema

### **Descripción de la Obra**

#### **Concepto**
Esta obra combina la estética base del equilibrio de los móviles de Alexander Calder con la complejidad física del problema de n-cuerpos. El resultado es un sistema donde 5 masas colgantes interactúan gravitacionalmente entre sí, creando patrones de movimiento únicos e impredecibles.

### **Interactividad**

#### **Controles del Usuario:**
- **Drag & Drop**: Arrastra cualquier figura o balancín para moverlo
- **Flechas ↑↓**: Ajustar intensidad del viento (0.0 - 5.0)
- **G**: Activar/Desactivar fuerzas gravitacionales
- **+ / -**: Aumentar/Disminuir constante gravitacional (saltos de 5.0)
- **ESPACIO**: Limpiar todos los trails del canvas

#### **Feedback Visual:**
- **Trails permanentes**: Cada masa deja un rastro de su trayectoria en tonos claros
- **Indicador de viento**: Barra visual que muestra la intensidad actual
- **Información en tiempo real**: Estado de todos los parámetros físicos
- **Color de arrastre**: Las figuras se vuelven amarillas al ser arrastradas

---

### **Randomness Utilizados**

#### **Perlin Noise (`noise()`)**
```javascript
// Aplicación: Viento orgánico y natural
let windX = map(noise(this.noiseOffsetX), 0, 1, -windStrength, windStrength);
let windY = map(noise(this.noiseOffsetY), 0, 1, -windStrength * 0.3, windStrength * 0.3);
```
- **Propósito**: Genera viento que nunca se repite, creando movimiento fluido y orgánico
- **Características**: Cada masa tiene offsets únicos para variedad individual

#### **Random (`random()`)**
```javascript
// Aplicaciones múltiples:
this.angle = random(-PI/6, PI/6);           // Ángulos iniciales variados
this.noiseOffsetX = random(2000, 3000);     // Offsets únicos en Perlin space
let colorIndex = floor(random(calderColors.length)); // Selección de colores
```
- **Propósito**: Diversidad en condiciones iniciales y comportamientos únicos

#### **Shuffle (`shuffle()`)**
```javascript
// Garantizar diversidad cromática:
colorAssignments = shuffle(colorAssignments);
```
- **Propósito**: Mezcla la asignación de colores garantizando que siempre aparezcan los 3 colores primarios de Calder en posiciones variables

---

### **Modelado del Problema de N-Cuerpos**

#### **Ley de Gravitación Universal**
Cada masa calcula la fuerza gravitacional hacia todas las demás masas usando:

```javascript
// F = G * m1 * m2 / r²
let strength = (gravitationalConstant * this.mass * otherMass.mass) / (distance * distance);
```

#### **Sistema de Interacciones**
- **5 masas** interactúan simultáneamente
- **20 fuerzas gravitacionales** calculadas en cada frame (cada masa hacia las otras 4)
- **Suma vectorial** de todas las fuerzas sobre cada masa

#### **Proceso por Frame**
1. **Para cada masa**: Calcula fuerza hacia todas las demás masas individualmente
2. **Suma fuerzas**: Cada masa experimenta la suma vectorial de 4 fuerzas gravitacionales
3. **Conversión angular**: Las fuerzas cartesianas se convierten en influencias sobre la velocidad angular del péndulo
4. **Aplicación**: `angularInfluence = gravitationalForce.x * 0.001`

#### **Características del N-Cuerpos**
- **No linealidad**: Pequeños cambios en posición generan grandes diferencias en comportamiento
- **Impredecibilidad**: Los patrones nunca se repiten exactamente debido a la sensibilidad a condiciones iniciales
- **Comportamiento emergente**: El movimiento de cada masa afecta a todas las demás simultáneamente
- **Escalabilidad**: La constante gravitacional es ajustable permitiendo desde movimientos sutiles hasta caos gravitacional


### **Características del codigoo**

#### **Arquitectura del Sistema**
- **Clase BalanceArm**: Representa balancines con brazos horizontales
- **Clase Mass**: Representa las figuras finales (círculos, cuadrados, triángulos)
- **Sistema jerárquico**: Cada balancín puede contener otros balancines o masas
- **Física híbrida**: Combina péndulos simples con fuerzas gravitacionales

#### **Renderizado Avanzado**
- **Doble capa**: Canvas principal + capa separada para trails permanentes (trazos de dibujos)
- **Trazos de contraste**: Tonos más claros que no compiten visualmente con las figuras
- **Colores garantizados**: Sistema que asegura la presencia de los 3 colores primarios de Calder

#### **Optimización de Performance**
- **Constraints de distancia**: Evita cálculos extremos y divisiones por cero
- **Límites de fuerza**: Previene comportamientos inestables
- **Renderizado eficiente**: Los trails se dibujan una sola vez y persisten

#### **De las unidades anteriores de "The Nature of Code"**
- **Unidad 0 (Randomness)**: Perlin noise, random, shuffle
- **Unidad 2 (Forces)**: Gravitación, viento, fricción
- **Unidad 3 (Oscillation)**: Péndulos, movimiento angular
