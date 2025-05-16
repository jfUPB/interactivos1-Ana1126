## Consolidación de lo aprendido  

### 1. Tabla de comparación  
![image](https://github.com/user-attachments/assets/3f500a3f-102c-4311-9b52-0fe9e3e2bb5c)  

### 2. ¿Por qué fue necesario introducir framing en el protocolo binario?  
En el protocolo binario se transmiten datos en bruto, sin separadores visibles como en ASCII. Además, se manejan más bytes por mensaje, lo que puede saturar el canal si no se controla. El framing permite estructurar los datos en bloques definidos, asegurando que el receptor pueda reconocer dónde empieza y termina cada paquete.  

### 3. ¿Cómo funciona el framing?  
El framing agrupa los datos en paquetes organizados. De esta forma, el receptor sabe cuándo comienza un nuevo conjunto de datos y puede procesarlo.  

### 4. ¿Qué es un carácter de sincronización?  
Es un byte especial que marca el inicio de un paquete. Sirve como punto de referencia para que el receptor se sincronice y pueda leer correctamente los datos que siguen.  

### 5. ¿Qué es el checksum y para qué sirve?  
El checksum es un valor numérico calculado a partir de todos los bytes del paquete. Se utiliza para verificar que los datos llegaron sin errores. Si el valor recibido no coincide con el calculado, se descarta el paquete.  

### 6. En la función readSerialData() del programa en p5.js:

#### - ¿Qué hace la función concat? ¿Por qué?  
```` js
function readSerialData() {
    let available = port.availableBytes();
    if (available > 0) {
        let newData = port.readBytes(available);
        serialBuffer = serialBuffer.concat(newData);
    }
````
La función concat une los nuevos datos recibidos con los que ya estaban en el buffer. Esto es necesario porque los datos pueden llegar por partes, y se necesita completar un paquete antes de procesarlo.  

#### - En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?  
```` js
  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift();
      continue;
    }
````
Se verifica que haya al menos 8 bytes porque ese es el tamaño mínimo de un paquete completo en el protocolo binario. Así se evita procesar datos incompletos.  

#### - En el código anterior qué significa 0xaa?  
0xAA es un valor hexadecimal que representa el byte de inicio del paquete. Se usa como referencia para identificar el comienzo de los datos.  

#### - En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?  
shift() elimina el primer byte del buffer si no es el de inicio (0xAA). continue salta al siguiente ciclo del bucle para seguir buscando el comienzo de un paquete válido.  

#### - Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?  
```` js
    if (serialBuffer.length < 8) break;
````
break detiene el bucle cuando no hay suficientes datos para formar un paquete completo. Así se espera a que lleguen más bytes antes de seguir procesando.  

#### - ¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?  
```` js
let packet = serialBuffer.slice(0, 8);
serialBuffer.splice(0, 8);
````
slice copia una parte del buffer sin modificarlo, mientras que splice elimina esos bytes del buffer original. Se usan juntas para extraer y luego eliminar los datos ya procesados.  

#### - A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?  
```` js
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
````
reduce recorre un arreglo y acumula un resultado, en este caso, sumando todos los bytes. Luego se aplica un módulo 256 para obtener un número entre 0 y 255, que se usa como checksum.  

#### - ¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?  
```` js
if (computedChecksum !== receivedChecksum) {
    console.log("Checksum error in packet");
    continue;
}
````
La comparación sirve como verificación: si ambos coinciden, el paquete es válido. Si no, se considera corrupto y se descarta.  

#### - En el código anterior qué hace la instrucción continue? ¿Por qué?  
Si el checksum no coincide, continue omite el paquete actual y pasa a revisar el siguiente, evitando procesar datos erróneos.  

#### - ¿Qué es un DataView? ¿Para qué se usa?  
```` js
let buffer = new Uint8Array(dataBytes).buffer;
let view = new DataView(buffer);
````
DataView es una forma de leer datos binarios con distintos tipos (como enteros de 16 bits o bytes sin signo). Se usa para interpretar correctamente los bytes recibidos según el formato original.  

#### -¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?  
```` js
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
````
Los datos en el buffer llegan en formato binario y no tienen un significado claro por sí solos. Es necesario convertirlos usando métodos como getInt16 o getUint8 para darles sentido en el contexto del programa y poder usarlos adecuadamente.
