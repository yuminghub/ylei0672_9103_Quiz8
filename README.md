# ylei0672_9103_Quiz8

## **Part 1: Imaging Technique Inspiration**


![An image of low soundwave](/assets/soundwave_low.png)
Low sound level of soundwave

![An image of high soundwave](/assets/soundwave_high.png)
High sound level of soundwave

__*"Piano Piano"*__ by Adrien M & Claire B, a visual design that translates sounds into undulating lines. The artwork features two representations: one depicting a relatively static sound and another showing dynamic feedback. Each image consists of a single line. For the major project, this can be paired with Nasreen Mohamedi's __*"Untitled-1"*__ or Piet Mondrian's __*"Broadway Boogie Woogie"*__ to create a multi-dimensional exploration of auditory and visual interactions, thereby enriching the sensory experience.


## **Part 2: Coding Technique Exploration**

![An image of Low sound matrix](/assets/matrix_low.png)
![An image of High sound matrix](/assets/matrix_high.png)


### **Here is the code used from the link:**

let mic, fft;
let gridRows = 10; 
let gridCols = 10; 

function setup() {
  createCanvas(800, 600);
  mic = new p5.AudioIn();
  mic.start();
  fft = new p5.FFT();
  fft.setInput(mic);
}

function draw() {
  background(0);
  let spectrum = fft.analyze();
  let cellWidth = width / gridCols; 
  let cellHeight = height / gridRows; 

  for (let i = 0; i < gridRows; i++) {
    for (let j = 0; j < gridCols; j++) {
      let freqIndex = floor(map(i * gridCols + j, 0, gridRows * gridCols, 0, spectrum.length));
      let amplitude = spectrum[freqIndex]; 
      
      let size = map(amplitude, 0, 255, 5, cellWidth/2); 
      let xOffset = map(amplitude, 0, 255, 0, cellWidth - size); 
      let yOffset = map(amplitude, 0, 255, 0, cellHeight - size); 

      fill(255);
      noStroke();
      ellipse(j * cellWidth + xOffset + size/2, i * cellHeight + yOffset + size/2, size, size);
    }
  }
}