#### Exploración de micro:bit y Micropython  

#### Entradas y salidas del micro:bit:  

#### - Entradas

-Botón A y B: Dos botones físicos en la parte frontal del micro:bit que detectan cuando son presionados.  

-Acelerómetro: sensor que mide la aceleración en los ejes X, Y y Z, permitiendo detectar inclinaciones y movimientos.

-Pin 0, 1 y 2: pines táctiles que pueden usarse como entrada para detectar contacto o señales eléctricas externas.  

-Sensor de luz: usa la matriz de LEDs para medir la cantidad de luz ambiental.  

#### - Salidas  

-Matriz de LEDs 5x5: pantalla compuesta por 25 LEDs que pueden encenderse de manera individual para mostrar patrones e información.
 
-Buzzer interno: permite generar sonidos de diferentes frecuencias. 

-Pin 0, 1 y 2: también pueden actuar como salidas para controlar otros dispositivos como motores o luces eternas.  

-Comunicación serial (UART): permite enviar datos a una computadora u otro dispositivo mediante USB o Bluetooth.  


#### Funciones de Micropython para controlar el micro:bit:

#### Funciones para entrada  

1. button_a.is_pressed() - Verifica si el botón A esta presionado.

````
from microbit import *
while True:
    if button_a.is_pressed():
        display.show("A")
````

2. accelerometer.get_x() - Obtiene el valor de aceleración en el eje X.

````
from microbit import *
while True:
    x = accelerometer.get_x()
    display.scroll(str(x))
````

3. pin0.read_analog() - Lee un valor analógico del pin 0 (de 0 a 1023).

````
from microbit import *
while True:
    valor = pin0.read_analog()
    display.scroll(str(valor))
````

#### Funciones para salida  

1. display.show() - Muestra un número, letra o imágen en la matriz de LEDs.

````
from microbit import *
display.show("Hi")
````
2. music.play() - Reproduce un sonido utilizando el buzzer interno o un altavoz externo.

````
from microbit import *
import music
music.play(music.NYAN)
````
3. pin1.write_digital(1) - Envía una señal digital (1 o 0) a un pin específico.

````
from microbit import *
while True:
    pin1.write_digital(1)  # Activa el pin 1
    sleep(1000)
    pin1.write_digital(0)  # Desactiva el pin 1
    sleep(1000)
```` 
