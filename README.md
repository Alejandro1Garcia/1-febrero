# 1-febrero
Cambio del color de fondo al dar clic dentro del área de un cuadrado


// variables para los valores de rojo, verde y azul (r, g, b)
let r, g, b;

function setup() {
  createCanvas(720, 400);
  // colores aleatorios
  r = random(255);
  g = random(255);
  b = random(255);
}

function draw() {
  background(127);
  // dibujar el círculo
  strokeWeight(2);
  stroke(r, g, b);
  fill(r, g, b, 127);
  rect(260, 100, 200, 200);
}

// cuando el usuario hace click
function mousePressed() {
  // revisar si el ratón está dentro del círculo
  let d = dist(mouseX, mouseY, 360, 200);
  if (d < 100) {
    // escoger nuevos colores aleatorios
    r = random(0,255,0);
    g = random(0,0,255);
    b = random(255,0,0);
  }
}
