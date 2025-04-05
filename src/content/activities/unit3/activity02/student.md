### Bomba 2.0  

#### Código: 
````
from microbit import *
import utime
import music

MODO_CONFIG = 0
MODO_ACTIVO = 1
MODO_EXPLOSION = 2

estado_actual = MODO_CONFIG
contador_tiempo = 20
marca_tiempo = utime.ticks_ms()

codigo_desactivacion = [button_a, button_b, button_a, "shake"]
posicion_codigo = 0
ultima_interaccion = utime.ticks_ms()

def mostrar_tiempo(tiempo):
    display.show(str(tiempo))

def detonacion():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

display.scroll("Config")

while True:
    if estado_actual == MODO_CONFIG:
        mostrar_tiempo(contador_tiempo)

        if button_a.was_pressed():
            if contador_tiempo < 60:
                contador_tiempo += 1
                mostrar_tiempo(contador_tiempo)

        if button_b.was_pressed():
            if contador_tiempo > 10:
                contador_tiempo -= 1
                mostrar_tiempo(contador_tiempo)

        if accelerometer.was_gesture("shake"):
            estado_actual = MODO_ACTIVO
            display.scroll("Armed")
            marca_tiempo = utime.ticks_ms()

    elif estado_actual == MODO_ACTIVO:
        tiempo_actual = utime.ticks_ms()

        if posicion_codigo < len(codigo_desactivacion):
            if codigo_desactivacion[posicion_codigo] == button_a and button_a.was_pressed():
                posicion_codigo += 1
            elif codigo_desactivacion[posicion_codigo] == button_b and button_b.was_pressed():
                posicion_codigo += 1
            elif codigo_desactivacion[posicion_codigo] == "shake" and accelerometer.was_gesture("shake"):
                posicion_codigo += 1

        if posicion_codigo == len(codigo_desactivacion):
            estado_actual = MODO_CONFIG
            contador_tiempo = 20
            display.scroll("Reset")
            posicion_codigo = 0

        if tiempo_actual - marca_tiempo >= 1000:
            marca_tiempo = tiempo_actual
            if contador_tiempo > 0:
                contador_tiempo -= 1
                mostrar_tiempo(contador_tiempo)
            else:
                estado_actual = MODO_EXPLOSION

    elif estado_actual == MODO_EXPLOSION:
        detonacion()

        while not pin_logo.is_touched():
            sleep(50)

        estado_actual = MODO_CONFIG
        contador_tiempo = 20
        display.scroll("Reset")
````

#### Explicación  
Este programa simula una bomba temporizada con una cuenta regresiva en el micro:bit. Tiene tres estados principales:

- Modo Configuración: Se ajusta el tiempo con los botones A y B.  
- Modo Armado: La cuenta regresiva inicia al agitar el micro:bit.  
- Modo Explosión: Cuando el tiempo llega a 0, la bomba "explota" y muestra una calavera en la pantalla.  
Además, se puede desactivar la bomba ingresando una secuencia específica:  
- Presionar A → Presionar B → Presionar A → Agitar el micro:bit.  
Si la secuencia es correcta, la bomba se reinicia. Si no, sigue la cuenta regresiva.  
