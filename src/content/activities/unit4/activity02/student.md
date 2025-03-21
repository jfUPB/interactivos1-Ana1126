### Exploración inicial

#### Introducción
El sketch: [sketch P_2_2_1_01](http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_1_01) de Generative Design es un ejemplo de arte generativo en p5.js. Este sketch permite crear patrones visuales interactivos basados en la repetición y variación de formas.

### Análisis del Código

1. **Configuración Inicial**
   - Se define un lienzo (“canva”) donde se dibujan las formas.
   - Se configuran variables de color y tamaño.
   - Se habilitan interacciones con el mouse para modificar el diseño en tiempo real.

2. **Bucle `draw()`**
   - Se limpia el fondo en cada iteración.
   - Se generan formas (como líneas, círculos o rectángulos) organizadas en una grilla.
   - Se aplican transformaciones como rotaciones y escalas, a menudo basadas en valores aleatorios o en la posición del mouse.

3. **Interactividad**
   - Al mover el mouse, se pueden modificar parámetros del dibujo, como el grosor de las líneas o los colores.
   - Algunas versiones del sketch permiten cambiar entre diferentes patrones con teclas.

4. **Generación de Variaciones**
   - Se pueden cambiar las proporciones de los elementos en la grilla.
   - Al modificar valores de ruido o aleatoriedad, se pueden generar composiciones diferentes en cada ejecución.

### Ejemplos de Dibujos

1. **Dibujo con Patrón Regular**
   - Ajustando la repetición en una cuadrícula uniforme.
   - Rotando cada elemento un ángulo fijo para crear efectos de onda.

2. **Dibujo con Aleatoriedad**
   - Aplicando `random()` en la rotación y escala para un patrón orgánico.
   - Variando la transparencia para un efecto más fluido.

### Posibles Extensiones
- Integrar un sistema de paletas de colores aleatorios.
- Implementar una interfaz para controlar los parámetros sin modificar el código.
- Exportar imágenes generadas de forma automática.

