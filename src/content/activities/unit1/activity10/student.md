#### Interacción básica con micro:bit  

#### Codigo en p5.js  
````
let port;
let connectBtn;
let squareColor;

function setup() {
    createCanvas(400, 400);
    background(220);

    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    squareColor = color(0, 0, 255); // Color inicial (azul)
}

function draw() {
    background(220);

    fill(squareColor);
    rect(150, 150, 100, 100); // Dibujar el cuadrado en el centro

    if (port.availableBytes() > 0) {
        let dataRx = port.read(1); // Leer un solo byte

        if (dataRx == 'A') {
            // Cambiar el color aleatoriamente
            squareColor = color(random(255), random(255), random(255));
        }
    }

    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}
````

#### Conexión y comunicación  

- Se conecta el micro:bit a través de la librería permitiendo la comunicación entre ambos
- Al presionar el botón A, el micro:bit envía la letra "A" por la conexión serial
- Cuando p5.js recibe "A", genera un color aleatorio y lo aplica al cuadrado 
