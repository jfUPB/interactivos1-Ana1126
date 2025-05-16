## Consolidacion de lo aprendido
### 1.¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial? 
Un protocolo de comunicación es un conjunto de reglas que define cómo se intercambian los datos entre dispositivos. En la comunicación serial, es importante porque garantiza que los datos sean entendidos correctamente por ambos dispositivos. Un protocolo asegura que se sigan ciertas reglas de formato y secuencia, lo que evita errores en la transmisión. Ejemplo en código:
````javascript
microbit.send_string("xValue:123,yValue:456\n")
````

### 2. ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos? 
Se separan con comas para permitir una fácil separación de los diferentes valores enviados. En este caso, cada dato (por ejemplo, valores del acelerómetro y el estado de los botones) está claramente delimitado, lo que facilita su procesamiento en el receptor. Ejemplo:
````javascript
microbit.send_string(str(xValue) + ',' + str(yValue) + ',' + str(aState) + ',' + str(bState))
````
### 3. ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje? 
Es necesario para que el receptor sepa cuándo ha llegado el mensaje completo. Sin un carácter de fin, el receptor podría no saber cuándo termina un mensaje, lo que podría resultar en una lectura incompleta. Ejemplo:
````javascript
microbit.send_string("xValue:123,yValue:456\n")
````

### 4. ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js? 
Una máquina de estados es necesaria para gestionar diferentes estados de la comunicación serial. Puede estar esperando datos, procesándolos o esperando que se complete un mensaje. Esto permite un control más organizado de los diferentes estados en que puede estar la comunicación. Ejemplo:

````javascript
if (estado == "esperando") {
    // Esperar por nuevos datos
} else if (estado == "procesando") {
    // Procesar los datos recibidos
}
````

### 5. ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial? 
Los datos se formatean en el micro:bit como cadenas de texto, con valores concatenados y enviados a través del puerto serial. Ejemplo en Python:
````javascript 
data_to_send = str(xValue) + "," + str(yValue) + "\n"
microbit.uart.write(data_to_send)
````

### 6. ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
Significa que los caracteres y números enviados por el micro:bit están representados como códigos numéricos que corresponden a caracteres ASCII. Por ejemplo, "123" en texto es enviado como sus valores ASCII correspondientes para cada carácter. Ejemplo:
````javascript
microbit.uart.write("123\n")
````

### 7. ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos? 
Es necesario para evitar leer datos que no han llegado completamente o que no están disponibles aún. Esto ayuda a prevenir errores en la lectura y procesamiento de datos incompletos. Ejemplo:
````javascript
// Verifica si hay bytes disponibles antes de intentar leer
if (port.availableBytes() > 0) {
    let data = port.readUntil("\n");
}
````

### ¿Qué pasa si esto no se hace?
Si no se verifica si hay bytes disponibles, el código podría intentar leer datos que aún no han sido enviados, lo que resultaría en errores o en la obtención de datos incompletos.

### 8. ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js? 
Se puede usar la función trim() para eliminar los espacios en blanco al principio y al final, incluidos los saltos de línea. Ejemplo:
````javascript
let data = data.trim();
````

### 9. Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías? 
Se usaría la función split(), que divide una cadena en un arreglo de subcadenas. Ejemplo:
````javascript
let values = data.split(" ");
````

### 10. ¿Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js? 
Es necesario convertir las cadenas a números para realizar operaciones matemáticas o lógicas con ellas. Las cadenas no pueden ser sumadas, restadas ni utilizadas en comparaciones numéricas sin ser convertidas primero. Ejemplo:
````javascript
let xValue = int(values[0]);
````

### 11. Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial? 
Los bytes enviados serían los valores ASCII correspondientes a la representación de los números y los valores booleanos en formato de texto:
````javascript
"123,756,False,True\n"
````

### 12. ¿Qué aprendiste nuevo del micro:bit que no sabías antes? 
Aprendí cómo utilizar el puerto serial para enviar datos desde el micro:bit a una aplicación en p5.js, y cómo se deben formatear y enviar los datos correctamente para asegurar que sean recibidos y procesados correctamente.

### 13. ¿Qué aprendiste nuevo de p5.js que no sabías antes? 
Aprendí cómo usar el puerto serial en p5.js para recibir datos y cómo manejar esos datos de manera eficiente utilizando funciones como port.availableBytes() y port.readUntil(). Además, aprendí a trabajar con datos recibidos y a convertirlos en números para utilizarlos en gráficos interactivos.
