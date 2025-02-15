#### Manipulando entradas digitales  
#### Experimento 1: lectura del estado del botón A: 

- Quería verificar si el micro:bit detecta correctamente cuando el botón A es presionado y si muestra un símbolo en la pantalla.
- Si presiono el botón A, el micro:bit mostrará la letra A en la pantalla LED.
- Código:
````
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    else:
        display.clear()
````
- Cuando presiono el botón A, la pantalla muestra la letra A. Y al soltarlo, la pantalla se apaga.
- El código funciona correctamente ya que button_a.is_pressed() devuelve True solo cuando el botón está presionado. Cuando se suelta. la
condición deja de cumplirse y la pantalla se borra con display.clear().
- El micro:bit puede detectar en tiempo real si el botón A está siendo presionado y responder con una acción visible en la pantalla LED.

#### Experimento 2: Presionar el botón B y mostrar una imágen: 

- Quería verificar si puedo asignar una imagen especifica cuando presiono el botón B
- Si presiono el botón B, el micro:bit mostrará un corazón en la pantalla LED.
- Código:
````
from microbit import *

while True:
    if button_b.is_pressed():
        display.show(Image.HEART)
    else:
        display.clear()
````
- Cuando presiono el botón B, aparece un corazón en la pantalla LED. Al soltarlo, la pantalla se apaga. 
- El código funciona correctamente ya que button_b.is_pressed() verifica si el botón está presionado. Al soltarlo, la pantalla se limpia,
lo que indica que el sistema responde a cambios en la entrada del boton en tiempo real.
- El micro:bit permite asociar diferentes respuestas a cada botón, lo que permite diseñar interacciones variadas para distintos eventos.

#### Experimento 3: Usar el logo táctil como otro boton: 

- Quería ver si el logo del micro:bit puede usarse como un botón táctil y mostrar una animación cuando se toca.
- Si toco el logo del micro:bit, se mostrará una animación de una flecha en movimiento.
- Codigo:
````
from microbit import *

while True:
    if pin_logo.is_touched():
        display.show(Image.ARROW_W)
        sleep(500)
        display.show(Image.ARROW_E)
        sleep(500)
    else:
        display.clear()
````
- Cuando toco el logo del micro:bit, aparece una animación con una flecha moviéndose de un lado a otro. Al soltarlo, la pantalla se apaga.
- El logo del micro:bit puede actuar como un botón táctil, detectando el contacto a través de pin_logo.is_touched(). Esto amplía las
posibilidades de interacción sin necesidad de botones físicos.
- El logo táctil del micro:bit es una entrada funcional que permite diseñar interacciones adicionales en proyectos interactivos sin usar
pines externos.



