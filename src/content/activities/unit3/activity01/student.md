## Volvamos a la actividad del semáforo  

#### Código  
````
from microbit import *
import utime

class Semaforo:
    ROJO = 0
    AMARILLO = 1
    VERDE = 2
    
    def __init__(self, x, tiempos):
        self.estado = self.ROJO
        self.tiempos = tiempos
        self.inicio_tiempo = utime.ticks_ms()
        self.x = x  # Posición en la pantalla
        self.actualizar_display()
    
    def actualizar_display(self):
        """Muestra el estado actual en la columna correspondiente."""
        for y in range(5):
            display.set_pixel(self.x, y, 0)  # Apagar todos los LEDs en la columna
        
        if self.estado == self.ROJO:
            display.set_pixel(self.x, 0, 9)  # Rojo en la fila superior
        elif self.estado == self.AMARILLO:
            display.set_pixel(self.x, 2, 5)  # Amarillo en el centro (brillo medio)
        elif self.estado == self.VERDE:
            display.set_pixel(self.x, 4, 3)  # Verde en la fila inferior (brillo bajo)
    
    def update(self):
        """Actualiza el estado del semáforo basado en el tiempo transcurrido."""
        tiempo_actual = utime.ticks_ms()
        if utime.ticks_diff(tiempo_actual, self.inicio_tiempo) > self.tiempos[self.estado]:
            self.inicio_tiempo = tiempo_actual
            self.estado = (self.estado + 1) % 3  # Ciclo Rojo -> Amarillo -> Verde -> Rojo
            self.actualizar_display()

# Inicializar los semáforos con sus respectivos tiempos
semaforo1 = Semaforo(0, [5000, 2000, 3000])  # Semáforo 1
semaforo2 = Semaforo(2, [3000, 1000, 2000])  # Semáforo 2
semaforo3 = Semaforo(4, [4000, 3000, 2000])  # Semáforo 3

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
    utime.sleep(0.1)  # Pequeña pausa para evitar sobrecarga
````

#### Reflexión  
Usar una clase (Semaforo) facilita la organización y reutilización del código, permitiendo manejar múltiples semáforos sin duplicar 
lógica. Cada semáforo es un objeto independiente con sus propios tiempos y estados, lo que mejora la modularidad y escalabilidad.

Además, la técnica de programación basada en máquinas de estado permite que el programa gestione transiciones de manera clara y 
eficiente. Cada semáforo sigue su propio ciclo sin afectar a los demás, lo que ayuda a manejar concurrencia sin necesidad de hilos o 
procesos adicionales. Esto es clave en sistemas embebidos como el micro:bit, donde los recursos son limitados.
