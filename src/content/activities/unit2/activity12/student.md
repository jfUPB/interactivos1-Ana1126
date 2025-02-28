## Implementando la Bomba Temporizada  

### Código  
````
from microbit import *
import utime

# Definir estados
CONFIG_MODE = 0
COUNTDOWN = 1
EXPLODE = 2

# Variables
current_state = CONFIG_MODE
countdown_time = 20  # Tiempo inicial en segundos
start_time = 0

# Límites del temporizador
MIN_TIME = 10
MAX_TIME = 60

while True:
    if current_state == CONFIG_MODE:
        display.show(str(countdown_time % 10))  # Muestra solo la última cifra
        
        if button_a.was_pressed() and countdown_time < MAX_TIME:
            countdown_time += 1
        elif button_b.was_pressed() and countdown_time > MIN_TIME:
            countdown_time -= 1
        elif accelerometer.was_gesture("shake"):  # ARMED - Iniciar cuenta regresiva
            start_time = utime.ticks_ms()
            current_state = COUNTDOWN

    elif current_state == COUNTDOWN:
        remaining_time = countdown_time - (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000)
        display.show(str(remaining_time % 10))  # Muestra solo la última cifra
        
        if remaining_time <= 0:
            current_state = EXPLODE

    elif current_state == EXPLODE:
        display.show(Image.SKULL)  # Explosión visual
        for _ in range(5):
            
            utime.sleep_ms(200)
        
        if pin_logo.is_touched():  # RESET
            countdown_time = 20
            current_state = CONFIG_MODE
````

### Enlace (video)  
https://youtu.be/eC-D3ytV1CU?si=Sm9pUvFigrWb6eKf 
