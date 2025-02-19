#### Produciendo sonidos en el micro:bit  

#### Código en micro:bit:

```` 
from microbit import *
import music  # Módulo para controlar sonidos

# Sonido 1: Tonos agudos (cuando se presiona el botón A)
# Sonido 2: Tonos graves (cuando se presiona el botón B)

while True:
    if button_a.is_pressed():
        music.play(['C5:4', 'E5:4', 'G5:4'])  # Secuencia de notas agudas
        display.show('A')
        sleep(500)
        display.clear()

    if button_b.is_pressed():
        music.play(['C3:4', 'E3:4', 'G3:4'])  # Secuencia de notas graves
        display.show('B')
        sleep(500)
        display.clear()
````

#### Explicación del código: 

- Módulo "music": Permite reproducir notas musicales con diferentes frecuencias y duraciones.
- 'C5': Nota Do aguda (alta frecuencia)
- 'C3': Nota Do grave (baja frecuencia)
- :4 indica la duración de la nota.
- Botón A: Reproduce una melodía de notas agudas.
- Botón B: Reproduce una melodía de notas graves.
- Se muestra la letra del botón presionado en la pantalla LED mientras suena el tono.
