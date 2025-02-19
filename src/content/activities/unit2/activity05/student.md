#### Leyendo datos seriales 
#### Código en P5.js  
Este código: 
- "Connect to micro:bit": conecta o desconecta el puerto serial.
- "h": envía el carácter h al micro:bit

#### Expliocación linea por linea 
````
let port;         // Variable para manejar la conexión serial
let connectBtn;   // Botón para conectar el micro:bit

function setup() {
    createCanvas(400, 400);   // Crea un lienzo de 400x400 píxeles
    background(220);          // Fondo gris claro

    port = createSerial();    // Inicializa la comunicación serial

    connectBtn = createButton('Connect to micro:bit'); // Botón de conexión
    connectBtn.position(80, 300);                      // Posición en pantalla
    connectBtn.mousePressed(connectBtnClick);         // Llama a la función al hacer clic

    let sendBtn = createButton('h');   // Botón para enviar 'h'
    sendBtn.position(220, 300);        // Posición en pantalla
    sendBtn.mousePressed(sendBtnClick); // Llama a la función al hacer clic
````
Función para conectar o desconectar: 
````
function connectBtnClick() {
    if (!port.opened()) {                     // Si el puerto NO está abierto
        port.open('MicroPython', 115200);     // Ábrelo con baudrate de 115200
    } else {
        port.close();                         // Si ya estaba abierto, ciérralo
    }
}
````

Función para enviar datos:  
````
function sendBtnClick() {
    port.write('h');  // Envía la letra 'h' al micro:bit
}
````

#### Código en micro:bit  
Este código: 
- Inicializa la comunicación UART (serial) a 115200 baudios.
-  Muestra un fantasma cuando está listo.
-  Si recibe 'h', muestra fantasma por 0.5 segundos y luego carita feliz.

#### Expicación linea por linea 

````
from microbit import *  # Importa todas las funciones de micro:bit
````

Iniciación de la comunicación serial: 

````
uart.init(baudrate=115200)  # Configura la UART con la misma velocidad que p5.js
display.show(Image.GHOST)   # Muestra un fantasma indicando que está listo
````

Bucle principal: 

````
while True:                           # Bucle infinito
    data = uart.read(1)               # Lee 1 byte desde el puerto serial
    if data:                          # Si recibió algo
        if data[0] == ord('h'):       # Si el byte recibido es la letra 'h'
            display.show(Image.GHOST) # Muestra fantasma 
            sleep(500)                # Espera 500 ms
            display.show(Image.HAPPY) # Luego muestra carita feliz
````


