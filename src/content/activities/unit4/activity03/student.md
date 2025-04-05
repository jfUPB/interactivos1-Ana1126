### Caso de estudio: micro:bit  

xValue representa el grado de inclinación que detecta el acelerómetro en el eje X, mientras que yValue mide la inclinación en el eje Y. aState indica si el botón A está siendo presionado (True) o no (False), y bState hace lo mismo con el botón B.

La línea ````"{},{},{},{}\n".format(xValue, yValue, aState, bState)```` es la que organiza y empaqueta estos valores en un formato conocido como CSV (Comma Separated Values), que permite que los datos se almacenen o transmitan de forma ordenada, separados por comas y finalizados con un salto de línea (\n). Esto facilita que otros programas, como p5.js, los puedan leer y procesar fácilmente. Sin estas comas o sin el salto de línea, los datos se juntarían y serían difíciles de interpretar, por ejemplo: 969652TrueFalse969652TrueFalse.

Esta información se transmite cada 100 milisegundos, gracias al sleep(100), lo cual genera una frecuencia de envío de 10 Hz. Si no se usara esta pausa, los datos se enviarían de forma continua y muy rápida, lo que podría saturar el puerto serial y causar fallos en la comunicación.

Los valores de xValue y yValue cambian dependiendo de cómo se incline el micro:bit. En las pruebas, los valores máximos detectados en cualquier dirección fueron aproximadamente 1024. Cuando alguno de los botones es presionado, su valor cambia a True; de lo contrario, permanece en False.

Si en lugar de is_pressed() se usara was_pressed(), el comportamiento sería diferente: este último detecta si el botón fue presionado una sola vez, y luego vuelve a False, en cambio is_pressed() se mantiene en True mientras el botón esté siendo presionado.

En cuanto a los datos que se envían por el puerto serial, se codifican como caracteres ASCII. Por ejemplo, si se manda la cadena "969,652,True,False\n", los bytes que realmente se transmiten serían:

mathematica  
Copiar  
Editar  
````39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A````  
Cada número o letra es traducido a su equivalente en código ASCII. Por ejemplo, 969 se convierte en 39 36 39, las comas se representan como 2C y el salto de línea como 0A.
