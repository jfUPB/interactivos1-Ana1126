#### Generando imágenes en micro:bit  
#### Código p5.js  
````
let port;
let connectBtn;
let hBtn, oBtn, lBtn, aBtn;

function setup() {
    createCanvas(400, 400);
    background(220);

    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    hBtn = createButton('H');
    hBtn.position(80, 350);
    hBtn.mousePressed(() => sendButtonClick('H'));

    oBtn = createButton('O');
    oBtn.position(160, 350);
    oBtn.mousePressed(() => sendButtonClick('O'));

    lBtn = createButton('L');
    lBtn.position(240, 350);
    lBtn.mousePressed(() => sendButtonClick('L'));

    aBtn = createButton('A');
    aBtn.position(320, 350);
    aBtn.mousePressed(() => sendButtonClick('A'));
}

function draw() {
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

function sendButtonClick(letter) {
    port.write(letter);
}
````
#### Código micro:bit 
````
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)
display.show(Image.DUCK)
display.show(Image.HEART)
display.show(Image.SNAKE)

while True:

        data = uart.read(1)
        if data:
            if data[0] == ord('H'):
                display.show(Image.BUTTERFLY)
                sleep(500)
                

            if data[0] == ord('O'):
                display.show(Image.DUCK)
                sleep(500)
                
            if data[0] == ord('L'):
                display.show(Image.HEART)
                sleep(500)
            
            if data[0] == ord('A'):
                display.show(Image.SNAKE)
                sleep(500)
````
Se utiliza la misma variable como en ejemplo de "Send Love" para hacer que al precionar ciertas letras se envíe la señal para generar 
ciertas imágenes. También se utiliza la misma base del código pero duplicando la variable para poner las letras que se iban a utilizar 
para enviar la señal y generar las imágenes. 
