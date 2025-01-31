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
