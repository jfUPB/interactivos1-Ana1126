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

  ## Vector de Prueba                ## Condición Inicial                ## Evento        ## Estado Esperado      ## Resultado Obtenido
Prueba 1 - Secuencia Normal     Estado: HAPPY, sin presionar botón      Esperar 1.5s           SMILE                      Pasa
Prueba 2 - Interrupción con      Estado: HAPPY, presionar botón A    Presión de botón A         SAD                       Pasa
       Botón A  
Prueba 3 - Botón A en SAD         Estado: SAD, presionar botón A     Presión de botón A        SMILE                      Pasa
