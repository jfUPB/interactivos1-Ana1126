## Reflexión sobre el diseño de la bomba  

El diseño de la máquina de estados para la bomba temporizada implicó una serie de decisiones estratégicas para garantizar una experiencia 
interactiva clara y funcional. Opté por estructurarla en tres estados principales: CONFIG_MODE, donde el usuario puede ajustar el tiempo
inicial; COUNTDOWN, que gestiona la cuenta regresiva; y EXPLODE, que representa el final del temporizador con una alerta visual.
Una de las mayores dificultades fue manejar correctamente la transición entre estados sin generar inconsistencias, especialmente en la 
detección de eventos como el shake para armar la bomba y el touch para resetearla. Para mejorar la experiencia, se podría implementar una 
señal visual más clara al cambiar de estado, como una animación progresiva en la cuenta regresiva. También sería útil permitir una pausa en 
la cuenta regresiva antes de que explote, agregando otro estado de espera o desactivación temporal. Reflexionar sobre estas decisiones me 
permitió ver cómo el diseño de interacciones en sistemas dinámicos es clave en la creación de experiencias inmersivas, algo fundamental en 
mi camino en el diseño de entretenimiento digital.
