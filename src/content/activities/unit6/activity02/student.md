## El Viaje de los datos - De tu navegador al servidor y de regreso

### 1. ¿Qué pasaría si se corta la “rampa de acceso” a Internet?
En mi casa me conecto mediante Wi-Fi. Si se corta esa “rampa de acceso” (por ejemplo, se va el Wi-Fi o se desconecta el cable), mi dispositivo ya no tendría forma de llegar a los servidores. Es como si intentara conducir hacia un destino, pero la carretera estuviera destruida o bloqueada. No podría acceder a ninguna página web ni enviar o recibir datos. Además, muchas aplicaciones que dependen de conexión dejarían de funcionar. En términos prácticos, es como si estuviera aislado digitalmente.

### 2. Pausa activa: ¿Ejemplos no digitales del modelo Cliente-Servidor?
Un ejemplo muy claro es un restaurante:

Cliente: la persona que entra y pide la comida.

Servidor: el mesero o la cocina que entrega la comida solicitada.

Petición: el cliente pide una hamburguesa.

Respuesta: el mesero entrega la hamburguesa lista.

Otro ejemplo sería una biblioteca:

Cliente: el lector que pide un libro.

Servidor: el bibliotecario que busca y entrega el libro solicitado.

Estos ejemplos muestran claramente cómo funciona el modelo: uno solicita algo y el otro lo entrega, si puede.

### 3. Pausa activa: Analiza una URL
URL seleccionada: https://www.netflix.com/browse/genre/839338

Protocolo: https:// – Indica que se usa HTTP seguro (cifrado).

Nombre de dominio: www.netflix.com – Es el “edificio” donde está el contenido.

Ruta: /browse/genre/839338 – Es la sección específica del sitio, en este caso, una categoría de películas o series.

Si solo escribo www.google.com sin ruta, el servidor me envía la página por defecto, que es la página principal del buscador. Probablemente esté configurada como /index.html o equivalente, aunque no siempre se ve.

### 4. Pausa activa: Comparación de HTTP y protocolos seriales (como UART)
Similitudes:

Ambos definen reglas de comunicación entre dos partes (cliente y servidor, o micro:bit y computador).

Usan una estructura definida para enviar mensajes entendibles por ambas partes.

Hay un orden en el intercambio de mensajes (pedido → respuesta).

Diferencias:

HTTP es mucho más complejo porque tiene que manejar tipos de contenido, errores, seguridad (como HTTPS), cabeceras, etc.

Los protocolos seriales como UART son más simples, centrados solo en enviar datos crudos byte a byte.

HTTP trabaja en un entorno global (Internet), mientras que UART es más local (microcontroladores).

HTTP necesita esta complejidad porque maneja muchos tipos de dispositivos, contenido multimedia, seguridad y múltiples usuarios al mismo tiempo, lo cual no es necesario en UART.

### 5. Pausa activa: HTML, CSS y JavaScript en un formulario de login
HTML: la estructura del formulario, como los campos para ingresar usuario y contraseña, y el botón de enviar.

CSS: el color del fondo, el estilo del botón, la fuente de los textos, la alineación de los elementos.

JavaScript: cuando el usuario escribe mal la contraseña y aparece un mensaje de error sin que la página se recargue. También puede validar que los campos no estén vacíos antes de enviar.

Cada uno cumple una función esencial y trabajan juntos para dar forma, estilo y funcionalidad a la experiencia web.

### 6. Pausa activa: ¿Cómo se ejecuta JavaScript?
JavaScript se ejecuta cuando el navegador encuentra una etiqueta <script> en el HTML. Si está en la parte superior, detiene la carga de la página para ejecutarlo. Si está al final o tiene defer, se ejecuta después que la página está lista.

Una vez activo, el JS no necesariamente se ejecuta línea por línea como un programa normal, sino que espera a que ocurran eventos (como clics, envíos de formularios, etc.) para actuar. Por eso se dice que es "dirigido por eventos", lo cual es ideal para páginas interactivas.

### 7. Pausa activa: draw() vs modelo basado en eventos
Ventajas del modelo basado en eventos:

Más eficiente, porque solo se ejecuta código cuando es necesario (por ejemplo, cuando el usuario hace clic).

Mejor rendimiento: no se desperdician recursos redibujando toda la interfaz constantemente como en draw().

Escalabilidad: permite múltiples interacciones y funcionalidades sin sobrecargar el sistema.

Tener un draw() redibujando todo sin que nada cambie sería ineficiente y poco óptimo, especialmente en interfaces con muchos elementos.

### 8. Pausa activa: ¿Por qué usar JavaScript en cliente y servidor?
Usar el mismo lenguaje (JavaScript) en cliente y servidor tiene muchas ventajas:

Facilita el aprendizaje: el mismo lenguaje para ambos lados reduce la curva de aprendizaje.

Menos errores de compatibilidad: los datos pueden moverse entre cliente y servidor con más facilidad.

Mayor eficiencia de desarrollo: los equipos pueden trabajar más integrados y compartir funciones o estructuras comunes.

Además, es práctico para proyectos pequeños o medianos donde un mismo desarrollador puede trabajar en ambos lados.

### 9. Pausa activa final: HTTP vs WebSockets
HTTP tradicional: es como enviar una carta o correo. Haces una petición, esperas la respuesta, y ya.

WebSockets: es como hacer una llamada telefónica directa y permanente. Ambas partes pueden hablar en cualquier momento, sin esperar nuevas peticiones.

Aplicaciones que usan WebSockets o similares:

Chats en línea (WhatsApp Web, Discord).

Juegos multijugador en tiempo real.

Edición colaborativa (Google Docs).

Transmisión de datos en vivo (como actualizaciones de precios en plataformas financieras).

Este tipo de comunicación permite respuesta inmediata, algo que no se puede lograr eficientemente con solo HTTP.
