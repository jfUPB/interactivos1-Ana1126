#### Generando salidas visuales  
#### Código en p5.js 
````
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);

    port = createSerial(); // Inicializa la conexión serial

    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    // Botones para enviar caracteres específicos
    createButton('Show Ghost').position(80, 340).mousePressed(() => port.write('g'));
    createButton('Show Happy').position(200, 340).mousePressed(() => port.write('h'));
    createButton('Show Heart').position(320, 340).mousePressed(() => port.write('c'));

    createButton('Show Text A').position(80, 380).mousePressed(() => port.write('a'));
    createButton('Show Text B').position(200, 380).mousePressed(() => port.write('b'));
    createButton('Show Text C').position(320, 380).mousePressed(() => port.write('d'));
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200); // Conecta con el micro:bit a la velocidad correcta
    } else {
        port.close(); // Cierra el puerto si ya estaba abierto
    }
}
````

#### Código en micro:bit:  
````
from microbit import *

uart.init(baudrate=115200)  # Inicializa la UART con la misma velocidad que p5.js
display.show(Image.HAPPY)   # Imagen inicial al encender

while True:
    data = uart.read(1)  # Lee un carácter del puerto serial
    if data:
        if data[0] == ord('g'):  # Muestra un fantasma
            display.show(Image.GHOST)
            sleep(500)
        elif data[0] == ord('h'):  # Muestra una carita feliz
            display.show(Image.HAPPY)
            sleep(500)
        elif data[0] == ord('c'):  # Muestra un corazón
            display.show(Image.HEART)
            sleep(500)
        elif data[0] == ord('a'):  # Muestra el texto 'A'
            display.scroll('A')
        elif data[0] == ord('b'):  # Muestra el texto 'B'
            display.scroll('B')
        elif data[0] == ord('d'):  # Muestra el texto 'C'
            display.scroll('C')
````

#### Explicación del funcionamiento:  
- El código de p5.js envía un carácter por el puerto serial cuando presionas un botón.
- El micro:bit recibe ese carácter y muestra la imagen o el texto correspondiente.
