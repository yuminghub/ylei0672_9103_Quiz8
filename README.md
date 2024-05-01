# ylei0672_9103_Quiz8

## **Part 1: Imaging Technique Inspiration**


![An image of low soundwave](/assets/soundwave_low.png)
Low sound level of soundwave

![An image of high soundwave](/assets/soundwave_high.png)
High sound level of soundwave

__*"Vibe"*__ *Video for concept brand from Alexis Kimbrough on YouTube. In the art world, this visualization technique is reminiscent of digital art and sound visualization work, where artists often merge sound and visual data to create immersive experiences. For example, the works of Ryoji Ikeda, a Japanese visual and sound artist, often explore similar themes, using data and sound to create dynamic visual landscapes in galleries and performances. These images reflect a modern approach to integrating audiovisual elements, showcasing how digital tools can translate auditory information into captivating visual displays.*


## **Part 2: Coding Technique Exploration**

![An image of Low sound matrix](/assets/matrix_low.png)
![An image of High sound matrix](/assets/matrix_high.png)

*Audio signals are captured through code, then quantified and converted into digital signals. Each point in the matrix dynamically changes based on real-time audio data, creating a sound-driven visual effect, suitable as part of an art installation or interactive exhibition.*

*This adjustment method allows the points in the matrix to not only reflect the intensity of the sound but also to display it in a more concentrated form, making the overall visual effect more focused and dynamic. Such implementations are more suitable for music visualization and other interactive displays that require dynamic responses to audio inputs.*

According to the code obtained from the [Working with sounds and speech in P5.js](https://medium.spatialpixel.com/sounds-bd05429aba38), this website contains many methods for using audio in p5.js.

### **Here is the code used from the link:**
```
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
```