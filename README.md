# Plausible_Heartbeat_Amoeba
let vertices = [];
let numVertices = 100; 
let maxOffset = 20;
let loopSpeed = 0.005;
let loopOffset = 0;
let time = 0;

function setup() {
  createCanvas(1080, 1080);
  frameRate(15);
  colorMode(HSB, 360, 100, 100);
}

function draw() {
  background(0);
  translate(width / 2, height / 2);

  stroke(0);
  strokeWeight(0.5);

  vertices = [];
  for (let i = 0; i < TWO_PI; i += TWO_PI / numVertices) {
    let r = 250 + noise(i + loopOffset) * maxOffset + sin(time + i) * 20; // Make vertices move
    let x = r * cos(i);
    let y = r * sin(i);
    vertices.push(createVector(x, y));
  }

  noFill();
  beginShape();
  for (let vert of vertices) {
    let hue = map(vertices.indexOf(vert), 0, vertices.length, 0, 360);
    stroke(hue, 100, 100);
    vertex(vert.x, vert.y);
  }
  endShape(CLOSE);

  for (let vert of vertices) {
    let hue = map(vertices.indexOf(vert), 0, vertices.length, 0, 360);
    stroke(hue, 100, 100);
    line(0, 0, vert.x, vert.y);
  }

  let heartBeatSize = sin(frameCount * 0.3) * 40 + 80;
  noFill();
  for (let i = 0; i < 10; i++) {
    let hue = map(i, 0, 10, 0, 360);
    stroke(hue, 100, 100);
    let size = heartBeatSize - i * 3;
    if (size > 0) {
      ellipse(0, 0, size);
    }
  }

  loopOffset += loopSpeed;
  time += 0.05;  // Update time for sine function
}
