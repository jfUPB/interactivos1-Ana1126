## Diseño de la Lógica de una Bomba Temporizada  

### Estados de la Máquina
#### Configuración (CONFIG_MODE)

- La bomba está desarmada y permite modificar el tiempo con los botones UP y DOWN.
- Rango de tiempo: 10 - 60 segundos.

#### Eventos:
- Presionar UP ➝ Aumenta tiempo en 1s (máx. 60s).
- Presionar DOWN ➝ Disminuye tiempo en 1s (mín. 10s).
- Shake (ARMED) ➝ Transición a COUNTDOWN.

### Cuenta Regresiva (COUNTDOWN)
- Muestra el tiempo restante en la pantalla LED.
- Resta 1 cada segundo hasta llegar a 0.

### Eventos:
- Tiempo llega a 0 ➝ Transición a EXPLODE.

### Explosión (EXPLODE)
- La pantalla muestra una animación de explosión.
- Se activa el sonido en el speaker.

### Eventos:
- Touch (RESET) ➝ Transición a CONFIG_MODE.

### Diagrama de estados  
![Diagrama de flujo](https://github.com/user-attachments/assets/4d0870a2-dfda-4098-9201-7d694a9109b4)
