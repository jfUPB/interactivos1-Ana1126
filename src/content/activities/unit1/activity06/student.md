#### Herramientas y tecnologías  

#### 1. Punto 15  
Al precionar el botón A del micro:bit, el circulo que aparece en la pantalla se vuelve de color rojo, y aparece una "A" dentro del círculo. 
Y al precionar el botón B de la pantalla el circulo se vuelve de color amarillo, y aparece una "B" dentro del círculo. 

¿Cómo se logra?: Cuando se preciona el botón A o  B en el micro:bit, este envía una letra (A o B) a través del puerto serial.  
- Cuando se presiona el botón A, el micro:bit envía la letra "A"
- Cuando se presiona el botón B, el micro:bit envía la letra "B"
- port.availableBytes() > 0: verifica si hay datos nuevos en el puerto serial
- let dataRx = port.read(1);: lee un carácter de los datos recibidos. y dependiendo del valor de dataRx:
  - Si presionas "A", usa fill ("red") para cambiar el color a rojo
  - Si presionas "B", usa fill ("yellow") para cambiar el color a amarillo  

#### 2. Punto 16  
Al sacudir el micro:bit, el círculo de la pantalla se vuelve de color verde, y aparece una letra "C" en la pantalla.  

¿Cómo se logra?:  Igual que en el punto 15, se lee un carácter de datos recibidos, en este caso: 
- Dependiendo del valor de dataRx:
  - Si recibe otro dato, usa fill ("green") por defecto 

#### 3. Punto 17  
Al precionar el botón "Send Love", se muestra un corazón por un momento en el micro:bit, y luego se queda viendo la representación de una 
carita feliz.  

¿Cómo se logra?: No estoy muy segura de este punto, pero lo que entiendo es que cuando se presiona el botón "Send Love", se ejecuta la 
función sendBtnClick(), que envía la letra "h" al micro:bit
