#### Control de movimiento con micro:bit  
#### Código p5.js
````
let port;
let connectBtn;
let circleX;

function setup() {
    createCanvas(400, 400);
    background(220);
    
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    circleX = width / 2; // Posición inicial del círculo
}

function draw() {
    background(220);
    fill('blue');
    ellipse(circleX, height / 2, 50, 50); // Dibujar el círculo

    if (port.availableBytes() > 0) {
        let dataRx = port.read(1); // Leer un solo byte de datos

        if (dataRx == 'A') {
            circleX -= 10; // Mover a la izquierda
        } 
        else if (dataRx == 'B') {
            circleX += 10; // Mover a la derecha
        }

        // Limitar la posición para que el círculo no salga del canvas
        circleX = constrain(circleX, 0, width);
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

#### Código micro:bit  
````
from microbit import *
import utime

uart.init(baudrate=115200)  # Configurar la comunicación serial

while True:
    if button_a.is_pressed():
        uart.write('A')  # Enviar 'A' si se presiona el botón A
        utime.sleep(0.2)  # Pequeño retraso para evitar envíos continuos

    if button_b.is_pressed():
        uart.write('B')  # Enviar 'B' si se presiona el botón B
        utime.sleep(0.2)
````

#### Explicación de mapeo  
- Si presiona botón A, envía la letra "A" por la conexión serial
- Si presiona botón B, envía la letra "B" por la conexión serial
- Si presiona el botón A, mueve el circulo hacia la izquierda  (circleX -= 10)
- Si presiona el botón B, mueve el circulo hacia la derecha (circleX += 10)
- Se usa constrain(circleX, 0, width) para evitar que el circulo salga del área visible 
