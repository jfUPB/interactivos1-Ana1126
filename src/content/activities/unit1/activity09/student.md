#### Generando patrones visuales   
#### Código 

````
let numCircles;
let maxSize;
let waveAmplitude;
let colorShift;

function setup() {
  createCanvas(600, 600);
  noLoop();  // Dibuja solo una vez
  generatePattern();  // Genera el primer patrón
}

function draw() {
  background(20);
  translate(width / 2, height / 2);  // Centramos el patrón
  noFill();
  
  for (let i = 0; i < numCircles; i++) {
    let radius = map(i, 0, numCircles, 50, maxSize);
    let colorValue = (i * colorShift) % 255;

    stroke(colorValue, 100, 255);
    strokeWeight(1.5);

    beginShape();
    for (let angle = 0; angle < TWO_PI; angle += PI / 36) {
      let offset = sin(angle * 3) * waveAmplitude;
      let x = (radius + offset) * cos(angle);
      let y = (radius + offset) * sin(angle);
      vertex(x, y);
    }
    endShape(CLOSE);
  }
}

// Genera nuevos valores aleatorios para modificar el patrón
function generatePattern() {
  numCircles = int(random(5, 20));  // Número de círculos concéntricos
  maxSize = random(150, 300);  // Tamaño máximo de los círculos
  waveAmplitude = random(5, 30);  // Amplitud de las ondulaciones
  colorShift = random(50, 150);  // Cambio de color entre círculos
}

// Evento de clic para regenerar el patrón
function mousePressed() {
  generatePattern();
  redraw();  // Redibuja con nuevos valores
}

````
#### Explicación de las funciones utilizadas  
- random(min, max) se utiliza para generar valores aleatorios en el número de circulos, su tamaño y los colores
- sin(angle * 3) crea ondulaciones en los circulos generando un efecto de vibración visual
- cos(angle) y sin(angle) se usan para calcular las coordenadas en el circulo, posicionando los vértices

#### Parámetros modificables 
- numCircles: determina la cantidad de circulos concéntricos
- maxSize: Define el radio máximo de los circulos
- waveAmplitude: controla la intensidad de la distorción del patrón
- colorShift: ajusta los colores de los anillos

#### Interacción  
Cada vez que se hace click en la pantalla, se genera un nuevo patrón con diferentes variaciones visuales. 

#### Imágenes  
![image](https://github.com/user-attachments/assets/2d5d3d60-1d2a-4ece-8c34-255ea5c0a459)
![image](https://github.com/user-attachments/assets/27cbce3f-b62a-4b81-9789-1fe62298a495)
![image](https://github.com/user-attachments/assets/5e1f0e39-f4a0-45c5-a8fd-f40f09c581a7)

