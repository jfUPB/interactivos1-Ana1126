### Bomba 3.0  

#### Código: 
````
from microbit import *
import utime
import music

# Definición de estados
MODO_CONFIG = 0
MODO_ACTIVO = 1
MODO_EXPLOTA = 2

estado_actual = MODO_CONFIG
contador_tiempo = 20
ultimo_tick = utime.ticks_ms()

evento_detectado = False
evento_recibido = ""

secuencia_desactivacion = ['A', 'B', 'A', 'S']
posicion_secuencia = 0
tiempo_secuencia = utime.ticks_ms()

def mostrar_tiempo(valor):
    display.show(str(valor))

def activar_explosion():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

def capturar_evento():
    global evento_detectado, evento_recibido
    if button_a.was_pressed():
        evento_recibido = 'A'
        evento_detectado = True
    elif button_b.was_pressed():
        evento_recibido = 'B'
        evento_detectado = True
    elif accelerometer.was_gesture("shake"):
        evento_recibido = 'S'
        evento_detectado = True
    elif uart.any():
        entrada_serial = uart.read().decode('utf-8').strip()
        if entrada_serial:
            evento_recibido = entrada_serial
            evento_detectado = True

def gestionar_bomba():
    global estado_actual, contador_tiempo, ultimo_tick, evento_detectado, evento_recibido, posicion_secuencia

    if estado_actual == MODO_CONFIG:
        mostrar_tiempo(contador_tiempo)
        if evento_detectado:
            if evento_recibido == 'A' and contador_tiempo < 60:
                contador_tiempo += 1
            elif evento_recibido == 'B' and contador_tiempo > 10:
                contador_tiempo -= 1
            elif evento_recibido == 'S':
                estado_actual = MODO_ACTIVO
                display.scroll("Armed")
                ultimo_tick = utime.ticks_ms()
        evento_detectado = False

    elif estado_actual == MODO_ACTIVO:
        tiempo_actual = utime.ticks_ms()
        if posicion_secuencia < len(secuencia_desactivacion) and evento_detectado:
            if evento_recibido == secuencia_desactivacion[posicion_secuencia]:
                posicion_secuencia += 1
            evento_detectado = False

        if posicion_secuencia == len(secuencia_desactivacion):
            estado_actual = MODO_CONFIG
            contador_tiempo = 20
            display.scroll("Reset")
            posicion_secuencia = 0

        if tiempo_actual - ultimo_tick >= 1000:
            ultimo_tick = tiempo_actual
            if contador_tiempo > 0:
                contador_tiempo -= 1
                mostrar_tiempo(contador_tiempo)
            else:
                estado_actual = MODO_EXPLOTA

    elif estado_actual == MODO_EXPLOTA:
        activar_explosion()
        while True:
            if uart.any():
                entrada_serial = uart.read().decode('utf-8').strip()
                if entrada_serial == 'T':
                    estado_actual = MODO_CONFIG
                    contador_tiempo = 20
                    display.scroll("Reset")
                    break
            sleep(50)

sleep(500)
display.scroll("Config")

while True:
    capturar_evento()
    gestionar_bomba()
````
#### Explicación  
Estructura General:  
- Se mantiene la lógica de la máquina de estados, pero con nombres de variables y funciones distintos.   
- MODO_CONFIG, MODO_ACTIVO y MODO_EXPLOTA representan los estados.   
- capturar_evento() recoge las acciones del usuario, ya sea desde los botones, el acelerómetro o el puerto serial.  
- gestionar_bomba() maneja la lógica de la bomba según el estado actual.  

Captura de Eventos:  
- Se almacena en evento_recibido lo que ocurrió ('A', 'B', 'S', etc.).  
- Se usa evento_detectado como bandera para indicar que se debe procesar.  

Lógica de Estados:  
- MODO_CONFIG: Permite aumentar/disminuir el tiempo y activar la bomba con un "shake".   
- MODO_ACTIVO: Reduce el contador, verifica si la secuencia de desactivación es correcta.  
- MODO_EXPLOTA: Muestra la explosión y espera la reactivación por comando serial ('T').  
