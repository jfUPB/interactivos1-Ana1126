## El momento de aplicar lo aprendido  

### Enlace a la aplicación original sin modificar, pero recreada en el editor de p5.js.  
https://editor.p5js.org/hannah26/sketches/Y0RN6SL7q  

### Muestra el código de p5.js para la versión modificada.  
````javascript
class E1 {
  constructor (x, y, r, dir = null) {
    this.pos = createVector(x,y);
    this.dir = dir;
    if (!dir) {
      this.dir = createVector(speed,0);
      this.dir.rotate(random(TWO_PI))
    }
    this.r = r
  } 
  move () {
    this.pos.add(this.dir); 
    this.dir.rotate(random(...directionJitter))
  }
  constrain () {
    let r = this.r;
    let x = constrain(this.pos.x, r, width-r)
    let y = constrain(this.pos.y, r, height-r)
    if (x != this.pos.x || y != this.pos.y) {
      this.pos.x = x;
      this.pos.y = y;
      this.dir.rotate(random(TWO_PI))
    }
  }
  inCircle (cx, cy, r) {
    return dist(cx,cy,this.pos.x,this.pos.y) <= r+this.r 
  }
  penetration (other) {
    let d = this.pos.dist(other.pos);
    let td = this.r + other.r; 
    return td - d;
  }
  interact (other) {
    let pen = this.penetration(other);
    if (abs(pen) < minR*touchRatio) {
      this.dir.rotate(radians(0.1))
    } else if (pen > 0) {
      let v = this.pos.copy().sub(other.pos).setMag(speed);
      this.dir = v;
    }
  }  
  draw () {
    circle(this.pos.x, this.pos.y, this.r*2)
    let p = this.pos.copy()
    let q = p.copy().add(this.dir.copy().setMag(this.r));
    line(p.x, p.y, q.x, q.y)
  }
}

let n = 300;
let speed = 0.5;
let touchRatio = 0.1;
let drawRatio = 3;
let creationSpread = 0.8;
let colorRatioPwr = 0.5;
let directionJitter = [0, 0.05];
let mode = "picture";
let circleAreaRatio = 20;
let centerX, centerY, R; 
let elements = [];
let minR, maxR;

let serial;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  setupSerial();
  generate();
}

function setupSerial() {
  serial = new p5.SerialPort();
  serial.on("data", serialEvent);
  serial.openPrompt();
}

function serialEvent() {
  let data = serial.readLine().trim();
  if (!data) return;
  let values = data.split(",");
  if (values.length === 4) {
    microBitX = int(values[0]) + windowWidth / 2;
    microBitY = int(values[1]) + windowHeight / 2;
    microBitAState = values[2] === "True";
    microBitBState = values[3] === "True";
  }
}

function generate() {
  R = min(width,height) / 2;
  let area = PI * R**2;
  n = floor(random(100,400));
  circleAreaRatio = random(2,30);
  let avgCircleArea = area / n;
  let minCircleArea = 2 * avgCircleArea / (circleAreaRatio+1);
  minR = sqrt(minCircleArea)/PI;
  maxR = sqrt(minCircleArea*circleAreaRatio)/PI; 
  centerX = width/2;
  centerY = height/2;
  elements = [];
  for (let i = 0; i < n; i++) {
    elements.push(randomElement());
  }
  background(0)
}

function randomElement () {
  let dir = createVector(1, 0);
  dir.rotate(random(TWO_PI));
  let v = dir.copy().mult(random(R*creationSpread))
  v.add(createVector(centerX, centerY));
  return new E1(v.x, v.y, random(minR,maxR), dir.mult(speed));
}

function mouseClicked() {
  generate();
}

function keyPressed() {
  if (mode == "elements") {
    mode = "picture"
  }
  else {
    mode = "elements"
  }
  background(0)
}

function draw() {
  simulate();
  if (mode == "elements") renderElements()
  else renderPicture()

  if (microBitAState) {
    fill(255, 0, 0);
    noStroke();
    circle(microBitX, microBitY, 10);
  }

  if (microBitBState) {
    fill(0, 0, 255);
    noStroke();
    rect(microBitX - 10, microBitY - 10, 20, 20);
  }
}

function renderElements() { 
  background(0)
  stroke(0)
  for (let e of elements) e.draw()
}
 
function renderPicture () {
  for (let i = 0; i < n; i++) {
    let a = elements[i];
    for (let j = i+1; j < n; j++) {
      let b = elements[j];
      if (abs(a.penetration(b)) < minR * drawRatio) {
        stroke(map((a.r+b.r)**colorRatioPwr, 
                    (2*minR)**colorRatioPwr, 
                    (2*maxR)**colorRatioPwr, 0, 255),20)
        line(a.pos.x, a.pos.y, b.pos.x, b.pos.y)
      }
    }
  }  
}

function simulate() {
  let newElements = [];
  for (let e of elements) {
    e.move();
    if (e.inCircle(centerX, centerY, R)) 
      newElements.push(e)
    else
      newElements.push(randomElement())
  }
  elements = newElements;
  n = elements.length;
  for (let i = 0; i < n; i++) {
    let a = elements[i];
    for (let j = i+1; j < n; j++) {
      let b = elements[j];
      a.interact(b);
      b.interact(a);
    }
  }  
}
````

### Enlace a la aplicación modificada en el editor de p5.js.  
https://editor.p5js.org/hannah26/sketches/A_i8a31-L
