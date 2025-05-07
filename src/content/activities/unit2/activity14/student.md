### Probando y Depurando la Bomba 

#### Pruebas y Resultados
- Presionar A varias veces en Configuración
El contador aumenta correctamente hasta un máximo de 60. FUNCIONA

- Presionar B varias veces en Configuración
El contador disminuye correctamente hasta un mínimo de 10. FUNCIONA

- Agitar el micro:bit
El sistema cambia al estado ARMADO y comienza la cuenta regresiva. FUNCIONA

- Esperar a que la cuenta regresiva llegue a 0
El sistema entra en el estado EXPLOSIÓN cuando el tiempo se agota. FUNCIONA

- Tocar el logo en EXPLOSIÓN
El sistema debería reiniciarse, pero en algunos casos no detecta el toque. NO SIEMPRE FUNCIONA

#### Errores y soluciones  
 - El sensor táctil del logo no siempre respondía correctamente  
Problema: A veces, el toque no se registraba de manera confiable.  
Solución: Se aumentó el tiempo de detección y se implementó un bucle que verifica varias veces la entrada para asegurar la respuesta.

 - Falta de indicación visual al iniciar  
 Problema: No había una señal clara para indicar que el sistema estaba en modo de configuración.  
 Solución: Se agregó un mensaje inicial en la pantalla que muestra "Config" al encender el dispositivo.

 - Inexactitud en la cuenta regresiva  
 Problema: El temporizador no mantenía un conteo preciso debido a la forma en que se manejaban los milisegundos.  
 Solución: Se ajustó la estructura de control del temporizador para mejorar la precisión de la cuenta regresiva.

#### Código corregido  
````
from microbit import *
import utime
import music

CONFIGURACION = 0
ARMADO = 1
EXPLOSION = 2

estado = CONFIGURACION
contador = 20
ultimo_tiempo = utime.ticks_ms()

def actualizar_display(tiempo):
    display.show(str(tiempo))

def explotar():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

while True:
    if estado == CONFIGURACION:
        display.scroll("Config")
        actualizar_display(contador)

        if button_a.was_pressed():
            if contador < 60:
                contador += 1
                actualizar_display(contador)

        if button_b.was_pressed():
            if contador > 10:
                contador -= 1
                actualizar_display(contador)

        if accelerometer.was_gesture("shake"):
            estado = ARMADO
            display.scroll("Armed")
            ultimo_tiempo = utime.ticks_ms()

    elif estado == ARMADO:
        tiempo_actual = utime.ticks_ms()
        if tiempo_actual - ultimo_tiempo >= 1000:
            ultimo_tiempo = tiempo_actual
            if contador > 0:
                contador -= 1
                actualizar_display(contador)
            else:
                estado = EXPLOSION

    elif estado == EXPLOSION:
        explotar()

        while not pin_logo.is_touched():
            sleep(100)

        estado = CONFIGURACION
        contador = 20
        display.scroll("Reset")
````




