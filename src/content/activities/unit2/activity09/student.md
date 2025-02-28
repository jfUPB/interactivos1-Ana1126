### Semáforo con máquinas de estados  

#### Código: 
````
from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.state = "ROJO"
        self.startTime = utime.ticks_ms()

    def update(self):
        if self.state == "ROJO":
            display.show(Image("99999:00000:00000:00000:00000"))  # Fila superior encendida
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 3000:
                self.state = "AMARILLO"
                self.startTime = utime.ticks_ms()

        elif self.state == "AMARILLO":
            display.show(Image("00000:00000:99999:00000:00000"))  # Fila central encendida
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 2000:
                self.state = "VERDE"
                self.startTime = utime.ticks_ms()

        elif self.state == "VERDE":
            display.show(Image("00000:00000:00000:00000:99999"))  # Fila inferior encendida
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 3000:
                self.state = "ROJO"
                self.startTime = utime.ticks_ms()

semaforo = Semaforo()

while True:
    semaforo.update()
````

#### Estados del Programa:
- "ROJO"  El semáforo muestra la luz roja.
- "AMARILLO" → El semáforo muestra la luz amarilla.
- "VERDE" → El semáforo muestra la luz verde.
- Cada estado se mantiene activo durante un tiempo determinado antes de cambiar al siguiente.

#### Eventos Evaluados en Cada Estado:
- En "ROJO": Se evalúa si han pasado 3 segundos desde que entró en este estado.
- En "AMARILLO": Se evalúa si han pasado 2 segundos desde que entró en este estado.
- En "VERDE": Se evalúa si han pasado 3 segundos desde que entró en este estado.
- Estos eventos ocurren a través de la función utime.ticks_diff(), que verifica el tiempo transcurrido.

#### Acciones Ejecutadas Cuando se Presenta un Evento:
-En "ROJO" - "AMARILLO":

- Se cambia la pantalla LED para mostrar la luz "amarilla" (cambia la posición de loss LED).
- Se cambia el estado a "AMARILLO".
- Se reinicia el tiempo (startTime).
- En "AMARILLO" → "VERDE":

- Se cambia la pantalla LED para mostrar la luz "verde" (cambia la posición de loss LED).
- Se cambia el estado a "VERDE".
- Se reinicia el tiempo (startTime).
- En "VERDE" → "ROJO":

- Se cambia la pantalla LED para mostrar la luz "roja"  (cambia la posición de loss LED).
- Se cambia el estado a "ROJO".
- Se reinicia el tiempo (startTime).

