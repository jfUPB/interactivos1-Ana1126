## Autoevaluación  
### **¿Qué tanto aprendí en esta unidad?**

Durante esta unidad, he adquirido conocimientos sobre varios conceptos clave en programación, especialmente en el uso de máquinas de estados y la integración entre p5.js y micro:bit. A continuación, detallo los conceptos aprendidos, los que aún me cuestan y las estrategias que seguiré para mejorar.

### **Conceptos Aprendidos**

1. **Máquinas de Estado**  
   Aprendí cómo estructurar una aplicación usando máquinas de estados finitos. Esto me permitió organizar mejor el flujo de mi programa y manejar los distintos eventos de forma eficiente.  
   **Ejemplo:** Implementé una máquina de estados para la simulación de una bomba en p5.js, con estados de configuración, armado y explosión.

2. **Manejo de eventos y concurrencia**  
   Aprendí a manejar eventos generados tanto en p5.js como en micro:bit, lo que me permitió interactuar entre ambos dispositivos.  
   **Ejemplo:** Implementé eventos como la detección de botones presionados y el gesto de sacudida en micro:bit para cambiar los estados de la bomba.

3. **Comunicación Serial**  
   Entendí cómo establecer una comunicación entre p5.js y micro:bit utilizando el puerto serial para el intercambio de datos.  
   **Ejemplo:** Logré que los eventos en micro:bit se transmitieran a p5.js mediante código en MicroPython y la función `port.read()` en p5.js.

4. **Pruebas y Depuración**  
   Aprendí la importancia de las pruebas de regresión para asegurar que las modificaciones no generaran nuevos errores.  
   **Ejemplo:** Diseñé distintos vectores de prueba para evaluar si la bomba respondía correctamente en cada estado y corregí errores detectados.

### **Conceptos que aún me cuestan**

1. **Manejo avanzado de concurrencia**  
   Aunque entiendo el concepto básico, me cuesta aplicar estrategias más complejas para manejar eventos simultáneos sin que el programa se bloquee o tenga comportamientos inesperados.

2. **Optimización del código**  
   Aún me cuesta identificar cómo mejorar la eficiencia de mi código, reduciendo redundancias y mejorando el rendimiento.

3. **Uso de estructuras de datos avanzadas**  
   Aunque entiendo los arreglos y objetos básicos, me falta práctica en estructuras más complejas como colas o pilas para manejar eventos de manera más eficiente.

### **Estrategias para mejorar**

1. **Investigar y practicar más sobre concurrencia**  
   - Leer artículos y documentación sobre técnicas de manejo de eventos y concurrencia en JavaScript.
   - Implementar pequeños programas que requieran manejar eventos concurrentes.
   - Tiempo estimado: 2 horas a la semana.
   - Inicio: La próxima semana.

2. **Optimización del código**  
   - Analizar mi código en busca de patrones repetitivos y encontrar formas de refactorizarlo.
   - Usar herramientas como linters y analizadores de rendimiento.
   - Tiempo estimado: 1 hora a la semana.
   - Inicio: Inmediato.

3. **Aprender estructuras de datos avanzadas**  
   - Leer documentación sobre colas y pilas en JavaScript.
   - Implementar pequeños ejercicios usando estas estructuras.
   - Tiempo estimado: 3 horas al mes.
   - Inicio: En dos semanas.

### **Conclusión**

He avanzado bastante en la comprensión de máquinas de estado, manejo de eventos y comunicación serial. Sin embargo, aún tengo aspectos por mejorar, especialmente en concurrencia, optimización y estructuras de datos avanzadas. Con las estrategias que planteé, espero reforzar estos conceptos y mejorar mi nivel de programación en las próximas semanas.

