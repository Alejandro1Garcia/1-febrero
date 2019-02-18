# 1-febrero
Cambio del color de fondo al dar clic dentro del área de un cuadrado

// variables para los valores de rojo, verde y azul (r, g, b)
let r, g, b;

function setup() {
  createCanvas(400, 400);
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
  fill(r, g, b, 190);
  rect(100, 100, 200, 200);
}

// cuando el usuario hace click
function mousePressed() {
  // revisar si el ratón está dentro del círculo
  let d = dist(mouseX, mouseY, 360, 200);
  if (d < 230) {
    // escoger nuevos colores aleatorios
    r = random(255,0,0);
    g = random(0,255,255);
    b = random(255,0,0);
  }
}



//2. Círculos que rebota a lo ancho de la pantalla


let balls = [];

let threshold = 30;
let accChangeX = 0;
let accChangeY = 0;
let accChangeT = 0;

function setup() {
  createCanvas(400, 400);

  for (let i = 0; i < 20; i++) {
    balls.push(new Ball());
  }
}

function draw() {
  background(0);

  for (let i = 0; i < balls.length; i++) {
    balls[i].move();
    balls[i].display();
  }

  checkForShake();
}

function checkForShake() {
  accChangeX = abs(accelerationX - pAccelerationX);
  accChangeT = accChangeX + accChangeY;
  // Si hay agitamiento
  if (accChangeT >= threshold) {
    for (let i = 0; i < balls.length; i++) {
      balls[i].shake();
      balls[i].turn();
    }
  }
  // Si no hay
  else {
    for (let i = 0; i < balls.length; i++) {
      balls[i].stopShake();
      balls[i].turn();
      balls[i].move();
    }
  }
}

class Ball {
  constructor() {
    this.x = random(width);
    this.y = random(height);
    this.diameter = random(10, 30);
    this.xspeed = random(-2, 2);
    this.oxspeed = this.xspeed;
    this.oyspeed = this.yspeed;
    this.direction = 0.7;
  }

  move() {
    this.x += this.xspeed * this.direction;
    //this.y += this.yspeed * this.direction;
  }

  // Rebota cuando toca el borde del lienzo
  turn() {
    if (this.x < 0) {
      this.x = 0;
      this.direction = -this.direction;
    } else if (this.y < 0) {
      this.y = 0;
      this.direction = -this.direction;
    } else if (this.x > width - 20) {
      this.x = width - 20;
      this.direction = -this.direction;
    } else if (this.y > height - 20) {
      this.y = height - 20;
      this.direction = -this.direction;
    }
  }

  // Cambia la velocidad en x e y (xspeed, yspeed) según
  // el cambio en el valor de la aceleración en x, accelerationX
  shake() {
    this.xspeed += random(5, accChangeX / 3);
    this.yspeed += random(5, accChangeX / 3);
  }

  // Desacelera gradualmente
  stopShake() {
    if (this.xspeed > this.oxspeed) {
      this.xspeed -= 0.6;
    } else {
      this.xspeed = this.oxspeed;
    }
    if (this.yspeed > this.oyspeed) {
      this.yspeed -= 0.6;
    } else {
      this.yspeed = this.oyspeed;
    }
  }

  display() {
    ellipse(this.x, this.y, this.diameter, this.diameter);
  }
}

