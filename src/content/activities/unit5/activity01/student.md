## Repasa el caso de estudio  

### ¿Cómo se están comunicando el micro:bit y el sketch de p5.js? ¿Qué datos envía el micro:bit?  

El micro:bit se comunica con el sketch de p5.js a través de datos enviados por el puerto serial, utilizando el siguiente formato:

```` python
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
````

Esto significa que el micro:bit transmite cuatro valores: las lecturas del acelerómetro en los ejes X e Y, y el estado de los botones A y B (como True o False). En p5.js, estos datos se reciben y se procesan mediante la línea:  
```` javascript
let values = data.split(",");
if (values.length == 4) {
  microBitX = int(values[0]) + windowWidth / 2;
  microBitY = int(values[1]) + windowHeight / 2;
  microBitAState = values[2].toLowerCase() === "true";
  microBitBState = values[3].toLowerCase() === "true";
}
````

### ¿Cuál es la estructura del protocolo ASCII usado?

El micro:bit transmite los datos en formato ASCII. Por ejemplo, la secuencia:

````mathematica
39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A
````  
corresponde al texto "969,652,True,False\n". Cada número representa un carácter ASCII (por ejemplo, 39 36 39 representa "969"), 2C es la coma (,) que separa los valores, y 0A es el carácter de nueva línea (\n), indicando el fin del mensaje.

### ¿Dónde se leen los datos del micro:bit en p5.js y cómo se transforman en coordenadas de pantalla?

En el código de p5.js, los datos del micro:bit se procesan en el draw() mediante esta sección:  
````javascript
if (microBitAState === true) {
  let x = microBitX;
  let y = microBitY;

  if (keyIsPressed && keyCode === SHIFT) {
    if (abs(clickPosX - x) > abs(clickPosY - y)) {
      y = clickPosY;
    } else {
      x = clickPosX;
    }
  }
}
````

### ¿Cómo se generan los eventos "A pressed" y "B released" en p5.js a partir de los datos enviados por el micro:bit?

El programa en p5.js evalúa continuamente los estados de los botones A y B. Cuando detecta que el botón A ha pasado de no estar presionado a estar presionado (False a True), se activa el evento "A pressed". En cambio, el evento "B released" ocurre cuando el botón B cambia de True a False, es decir, cuando deja de estar presionado.
