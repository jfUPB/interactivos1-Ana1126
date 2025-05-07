### Algunos ejemplos inspiradores  
### Ejemplo en processing.
**- Enlace de ejemplo**: https://openprocessing.org/sketch/2397114  
**- Decripción y funcionamiento**: 
Genera patrones visuales dinámicos que evolucionan con el tiempo, creando una experiencia visual atractiva. Lo que más me llamó la atención fue la complejidad emergente a partir de reglas aparentemente simples, y cómo la interacción del usuario puede influir en la generación de patrones.

El sketch utiliza varias funciones y técnicas de p5.js:​  
- Funciones de dibujo: Se emplean funciones como line(), ellipse(), y rect() para crear formas básicas en el lienzo.​  
- Transformaciones: Se utilizan translate(), rotate(), y scale() para posicionar y orientar las formas en el espacio.​  
- Interactividad: El sketch responde a eventos del mouse y del teclado, permitiendo al usuario influir en la generación de patrones.​  
- Estructuras de control: Se aplican bucles for y declaraciones if para controlar la lógica de dibujo y la evolución de los patrones.

**- Modificaciones**: He modificado el código para agregar colores dinámicos a los elementos y cambiar la apariencia de las líneas. Ahora cada círculo tiene un color aleatorio y las líneas se colorean según el elemento al que están conectadas.
https://editor.p5js.org/generative-design/sketches/ByZZgqcqpk4

### Ejemplo en Generative Design.
**- Enlace de ejemplo**: http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_3_01  
**- Decripción y funcionamiento**: 
Este sketch genera formas orgánicas en constante cambio usando puntos conectados que se mueven de manera aleatoria. Me pareció interesante cómo las formas parecen vivas, casi como si fueran organismos flotando en el espacio. También me llamó la atención cómo los puntos siguen al mouse y cómo el usuario puede interactuar para generar nuevas formas.
El código utiliza puntos distribuidos en un círculo que se mueven aleatoriamente y están conectados mediante curvas suaves. Se implementa un sistema de agentes que flotan y se deforman en cada frame, lo que genera un efecto fluido y dinámico.

Funciones principales utilizadas en p5.js
- setup(): Configura el lienzo y los valores iniciales.
- draw(): Se ejecuta en bucle para generar el movimiento y la interacción.
- mousePressed(): Reinicia la figura cuando se hace clic en la pantalla.
- keyReleased(): Controla la interacción del usuario (borrar, cambiar estilos, guardar imagen, pausar el dibujo).
- curveVertex(): Permite dibujar formas suaves y curvas fluidas conectando puntos.
- random(): Se usa para generar la variación en el movimiento de los puntos.
- noFill() y fill(): Controlan si las formas están rellenas o solo con contorno.
- noLoop() y loop(): Pausan y reanudan la animación.

**- Modificaciones**: He modificado los colores para que sean más dinámicos y vibrantes, además de oscurecer el fondo para un mejor contraste. También ajusté el grosor de las líneas para mayor presencia visual. 
https://editor.p5js.org/generative-design/sketches/ByZZgqcqpk4  

### Ejemplo en P5js examples.
**- Enlace de ejemplo**: https://p5js.org/examples/repetition-bezier/     
**- Decripción y funcionamiento**:  
Este sketch genera líneas Bézier con colores cambiantes que responden a la posición del cursor. Me pareció llamativo cómo las líneas siguen una estructura curva y crean un efecto dinámico y vibrante con la combinación de colores en modo HSB.
Funciones principales utilizadas en p5.js
- setup(): Define el lienzo y la configuración inicial (modo de color, grosor de línea, eliminación de rellenos).
- draw(): Se ejecuta en bucle para actualizar las curvas y sus colores en cada frame.
- background(): Establece un fondo oscuro para resaltar los colores vivos.
- for loop: Genera múltiples curvas Bézier en diferentes posiciones.
- bezier(): Dibuja las líneas Bézier con diferentes puntos de control.
- stroke(): Aplica el color a las líneas.
- colorMode(HSB): Usa el modo de color HSB en lugar de RGB para manejar los tonos con más facilidad.
- mouseX: Controla la posición de los puntos de la curva para que las líneas sigan el movimiento del cursor.

**- Modificaciones**  
- Color más vibrante: Se aumentó la saturación y el brillo en stroke(), creando un efecto más colorido.
- Efecto de oscilación: Se añadió sin(frameCount * 0.05), que hace que las curvas se muevan ligeramente con el tiempo.
- Curvas más dinámicas: Se cambió la distribución de las líneas Bézier para que tengan una variación más marcada en la curvatura.  
[https://editor.p5js.org/](https://editor.p5js.org/hannah26/sketches/wWigqOTOV)
