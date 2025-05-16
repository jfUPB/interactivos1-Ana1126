## Caso de estudio: micro:bit
### Resultado del experimento con datos binarios en SerialTerminal

![image](https://github.com/user-attachments/assets/02cefbad-11a7-400d-a9c0-6cf08fc9ed94)
![image](https://github.com/user-attachments/assets/dd6f577d-509b-4ebf-aff6-8e6682368d1a)

Enviar los datos en formato ASCII facilita mucho la lectura, ya que los datos son fácilmente comprensibles. Si se tiene claro qué datos se van a enviar, el formato binario es más eficiente debido a la compresión, pero para pruebas o situaciones en las que la legibilidad es más importante, el formato ASCII es preferible. En el caso del gesto "shake", se están enviando 6 datos.

Cada dato tiene un valor entero que no parece tener un propósito claro junto a él. Los primeros dos corresponden a la posición en X y Y del micro:bit cuando se realiza el gesto, y los otros dos indican el estado de los botones A y B (True o False). Cuando están en True, se representan como 1, y al intentar obtener resultados negativos, solo aparece 00, lo cual no entiendo bien.  

![image](https://github.com/user-attachments/assets/eba4a0fb-1c71-4d13-910d-040f7104c1f4)  

Es mucho más sencillo leer los datos en formato texto, pero en formato hexadecimal se vuelve mucho más complejo y se generan más datos de los necesarios. Creo que ambos formatos tienen diferentes aplicaciones, dependiendo de cómo se quiera usar la información. Por ejemplo, si el proyecto tiene una alta interacción con el usuario, sería mejor usar formato ASCII. Sin embargo, para evitar sobrecargar el puerto serial, el formato binario sería más adecuado.

### Diferencias entre ASCII y binario:

En formato binario: los datos ocupan menos espacio y son más compactos, pero no son legibles de inmediato.

En formato ASCII: los datos son fácilmente legibles y comprensibles, pero ocupan más espacio y pueden ser más lentos para procesar.

### Ventajas y desventajas:

#### Binario:

Ventaja: Menos uso de ancho de banda, más eficiente en términos de tamaño.

Desventaja: Difícil de leer directamente.

#### ASCII:

Ventaja: Fácil de leer y entender.

Desventaja: Requiere más espacio y es más lento de procesar.

### Conclusión:

Usar binario es más eficiente en términos de rendimiento y espacio, pero es más difícil de interpretar sin herramientas específicas.

El formato ASCII es más accesible y fácil de trabajar cuando se necesitan leer los datos directamente, pero tiene un costo mayor en espacio y tiempo de procesamiento.

