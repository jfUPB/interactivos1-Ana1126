## Explorando los clientes (p5.js + Socket.IO)  

Cuando intenté cerrar el servidor, apareció el siguiente mensaje:  
````ruby
GET http://localhost:3000/socket.io/?EIO=4&transport=polling&t=... net::ERR_CONNECTION_REFUSED
WebSocket connection to 'ws://localhost:3000/socket.io/?EIO=4&transport=websocket&...' failed:
````

Esto indica que el navegador intentó conectarse al servidor, pero no recibió respuesta, lo cual ocurre porque el servidor estaba apagado. Una vez que lo reinicio, estos errores desaparecen.

Al comentar la línea de código correspondiente a la conexión, la página 1 aparece inicialmente en blanco y solo se actualiza cuando interactúo con la página 2. Este comportamiento puede ser útil dependiendo del tipo de interacción deseada, por ejemplo, si se quiere que el espectador no pueda generar ningún cambio hasta que reciba una señal específica del servidor.  

````yaml
Page 2 received: { x: 217, y: 109 }
 ````

Este mensaje fue enviado desde la página 2. Sucede porque el evento es gestionado por el servidor, que transmite la señal a todos los sockets excepto al que la originó. Por lo tanto, quien recibe la información es la página 1.

Al realizar una prueba con una condición if, observé que el mensaje "Page 2 detected change…” aparece solo cuando hay un leve movimiento en la página. Si no hay cambios, desaparece. Esto es similar al uso de datos binarios o ASCII optimizados, que buscan evitar el envío innecesario de paquetes para no sobrecargar el servidor.

Actividad final:
Implementé todos los ajustes requeridos en el código. Logré que el fondo se oscureciera cuando la ventana se alejaba, que el círculo creciera en función del tamaño de la ventana de la página 2 (o la ventana remota), y que una línea cambiara de color entre verde y rojo dependiendo de si se encontraba en el lado izquierdo o derecho. Aunque este último efecto no fue del todo preciso, sí cumplía parcialmente con la intención.
