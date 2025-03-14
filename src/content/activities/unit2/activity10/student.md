#### Controlando la Pantalla con una Máquina de Estados y Concurrencia

### Explicación del Programa y la Concurrencia
Este programa usa una máquina de estados finitos para gestionar la concurrencia entre la secuencia automática de imágenes y la interacción 
del usuario mediante el botón A.

¿Cómo logra la concurrencia?

- Usa una estructura de máquina de estados para manejar transiciones entre imágenes (HAPPY, SMILE, SAD).
- Cada estado tiene un tiempo predefinido (HAPPY_INTERVAL, SMILE_INTERVAL, SAD_INTERVAL).
- Si no se presiona el botón A, la secuencia sigue automáticamente.
- Si se presiona el botón A, el sistema interrumpe la secuencia y cambia de estado según las reglas establecidas.
- El bucle while True revisa constantemente el tiempo y el estado, permitiendo responder a los eventos sin bloquear la ejecución.

### Vectores de Prueba
Para verificar que el programa funciona correctamente, probaremos distintos escenarios con eventos y observaremos el comportamiento esperado.

- Vector de Prueba:            
-Prueba 1 - Secuencia Normal   
-Prueba 2 - Interrupción con Botón A  
-Prueba 3 - Botón A en SAD  

- Condicion inical:  
-Estado: HAPPY, sin presionar botón  
-Estado: HAPPY, presionar botón A  
-Estado: SAD, presionar botón A  

- Evento:  
-Esperar 1.5s  
-Presión de botón A    
-Presión de botón A  

- Estado Esperado:  
-SMILE  
-SAD  
-SMILE  

- Resultado Obtenido:  
-Pasa  
-Pasa  
-Pasa  



