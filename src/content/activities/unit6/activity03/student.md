## El Servidor (Node.js)  

Las librerías son de gran ayuda porque contienen fragmentos de código ya desarrollados y comprobados, lo que facilita mucho la programación al reutilizarlos. Al intentar abrir el proyecto cambiando la carpeta, aparece un error 404. Esto ocurre, según entiendo, porque el servidor está solicitando información que no encuentra en el nuevo directorio, y por tanto no sabe qué mostrar. Sin embargo, si actualizo correctamente la ruta, esta nueva versión funciona y la anterior deja de hacerlo, ya que se desvincula del servidor.

Socket
Cuando se conecta un cliente, aparece el mensaje Cliente conectado: fdO1Z9v_XYQfhykHAAAB, y al desconectarse, el mismo ID se muestra como Cliente desconectado: fdO1Z9v_XYQfhykHAAAB. Aunque ambas pestañas del navegador muestran IDs distintos porque se conectan desde terminales diferentes, el servidor sigue registrando los eventos correctamente.

En el experimento con socket.broadcast, los datos de movimiento solo llegan a la terminal de una de las páginas, ya que el mensaje se está enviando únicamente al socket opuesto, y no a todos. En cambio, otra línea de código logra enviarlo a todos los sockets conectados. Además, al cambiar el número de puerto a 3001, el servidor comienza a funcionar en ese puerto, mientras que deja de hacerlo en el anterior. Esto sucede porque tanto la variable del puerto (port) como la función listen deben coincidir para que la comunicación se establezca correctamente.
