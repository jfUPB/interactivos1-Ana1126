### Crear la bomba en p5.js  

````
const ESTADOS = {
  CONFIGURACION: 0,
  ARMADO: 1,
  EXPLOSION: 2
};

let bomba = {
  estado: ESTADOS.CONFIGURACION,
  contador: 20,
  ultimoTiempo: 0,
  secuenciaEsperada: ['A', 'B', 'A', 'Shake'],
  secuenciaActual: [],
};

let botones = {};
let displayText = "";

function setup() {
  createCanvas(200, 210);
  
  botones.A = crearBoton("Botón A", 20, 150, () => manejarEntrada('A'));
  botones.B = crearBoton("Botón B", 100, 150, () => manejarEntrada('B'));
  botones.Shake = crearBoton("Shake", 20, 180, () => manejarEntrada('Shake'));
  botones.Reset = crearBoton("Reset", 100, 180, resetear);

  textAlign(CENTER, CENTER);
  textSize(32);
  displayText = "Config";
}

function draw() {
  background(220);
  manejarEstados();
  text(displayText, width / 2, height / 2);
}

function crearBoton(etiqueta, x, y, accion) {
  let btn = createButton(etiqueta);
  btn.position(x, y);
  btn.mousePressed(accion);
  return btn;
}

function manejarEstados() {
  switch (bomba.estado) {
    case ESTADOS.CONFIGURACION:
      displayText = bomba.contador;
      break;

    case ESTADOS.ARMADO:
      let tiempoActual = millis();
      if (tiempoActual - bomba.ultimoTiempo >= 1000) {
        bomba.ultimoTiempo = tiempoActual;
        if (bomba.contador > 0) {
          bomba.contador--;
        } else {
          bomba.estado = ESTADOS.EXPLOSION;
          displayText = "BOOM!";
        }
      }
      verificarSecuencia();
      break;

    case ESTADOS.EXPLOSION:
      background(255, 0, 0);
      displayText = "BOOM!";
      break;
  }
}

function manejarEntrada(evento) {
  if (bomba.estado === ESTADOS.CONFIGURACION) {
    if (evento === 'A' && bomba.contador < 60) bomba.contador++;
    if (evento === 'B' && bomba.contador > 10) bomba.contador--;
  } 

  if (bomba.estado === ESTADOS.ARMADO) {
    bomba.secuenciaActual.push(evento);
  }

  if (evento === 'Shake' && bomba.estado === ESTADOS.CONFIGURACION) {
    bomba.estado = ESTADOS.ARMADO;
    bomba.ultimoTiempo = millis();
    displayText = "Armed";
  }
}

function verificarSecuencia() {
  if (bomba.secuenciaActual.length === bomba.secuenciaEsperada.length) {
    if (JSON.stringify(bomba.secuenciaActual) === JSON.stringify(bomba.secuenciaEsperada)) {
      resetear();
    } else {
      bomba.secuenciaActual = [];
    }
  }
}

function resetear() {
  bomba.estado = ESTADOS.CONFIGURACION;
  bomba.contador = 20;
  bomba.secuenciaActual = [];
  displayText = "Config";
}
````
