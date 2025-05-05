### Caso de estudio: p5.js  

Una de las primeras diferencias que noto es que el código original contiene muchas más librerías o archivos adicionales. En cuanto al sketch, no encuentro diferencias demasiado marcadas a simple vista. La sección donde aparece la función preload se encarga de cargar archivos esenciales como vectores, sonidos u otros recursos que el programa necesita antes de comenzar a ejecutarse.

Después viene la parte relacionada con la comunicación serial. Los datos se envían mediante esta línea:

````python   
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
````

Esta estructura organiza los cuatro datos en posiciones específicas dentro de la cadena de texto. Cada valor se separa por comas y se representa en formato ASCII. El salto de línea \n indica el final del conjunto de datos. Si por algún motivo no se reciben correctamente los cuatro datos, el programa intentará procesar lo que haya recibido, lo que puede provocar errores en el funcionamiento general.

El uso de windowWidth/2 y windowHeight/2 sirve para centrar los valores en la pantalla, ya que el punto (0,0) en p5.js se encuentra en la esquina superior izquierda. Sin este ajuste, los elementos aparecerían alineados hacia esa esquina.

La función updateButtonState tiene como propósito verificar si hubo un cambio en el estado de algún botón, por ejemplo, si pasó de no estar presionado a estarlo. Esto es útil para detectar un solo clic en lugar de una acción sostenida. Si no se controlara este cambio de estado, el programa interpretaría que el botón sigue presionado todo el tiempo, dificultando distinguir entre una pulsación corta y una larga.

En el nuevo código, noté que la acción de borrar el fondo ahora se activa con la tecla Delete, en lugar de la barra espaciadora como en versiones anteriores. Esto lo que hace es simplemente volver a colocar el fondo blanco. También se incluyen nuevas funciones específicas para la integración con el micro:bit, que no estaban en el primer código.

Finalmente, respecto al mensaje que indica “no se están recibiendo cuatro datos del microbit”, no me apareció en ningún momento, incluso después de probar diferentes formas de provocar el error. Parece que no se presenta en mi caso.
