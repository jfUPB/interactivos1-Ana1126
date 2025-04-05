### Vectores de prueba  
![image](https://github.com/user-attachments/assets/9d72255f-c892-4823-a825-6920c5b4003e)  

### Pruebas de regresión  
- El contador no actualizaba en p5.js al recibir datos de micro:bit: port.readLine() no es una función válida en p5.js Serial; Se cambió a
port.readUntil("\n") y se usó .trim() para eliminar espacios en blanco.
- Explosión se activaba instantáneamente al cambiar a ARMADO: ultimoTiempo no se reiniciaba al cambiar a ARMED; Se añadió ultimoTiempo = millis(); al entrar en ARMED
- Reset no restauraba la secuencia ingresada: La lista secuencia no se vaciaba al resetear; Se añadió secuencia = []; en la función resetear()
- Comandos inválidos provocaban errores en consola: No se manejaban caracteres desconocidos en manejarEntrada(); Se añadió un default en el switch para ignorar entradas no válidas
