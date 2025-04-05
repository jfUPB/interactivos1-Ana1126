#### Analizando un Programa con Máquinas de Estados

### Resumen visual del flujo:  
- Estado "int" - evento: ses crea el objeto
  - Acción: se muestra el pixel con el estado inicial
  - Transición: "int" - "WaitTimeout"
- Estado "WaitTimeout" - evento: pasa el tiempo definido
  - Acción: Se alterna el brillo del pixel
  - Transición: Permanece en "WaitTimeout" para seguir parpadeando
- utime.ticks_ms(): Devuelve el tiempo en milisegundos desde que se inició el micro:bit.
- utime.ticks_diff(a, b): Calcula la diferencia entre dos tiempos.
- Brillo de píxeles: Va de 0 (apagado) a 9 (máximo brillo).

El programa muestra como usar una máquina de estados para controlar la animación de dos pixeles parpadeantes con diferentes intervalos. 
Utilizando el estado "WaitTimeout" para esperar el tiempo necesario antes de alterar el brillo. Esto permite controlar de forma precisa los
cambios visuales en la pantalla LED. 
