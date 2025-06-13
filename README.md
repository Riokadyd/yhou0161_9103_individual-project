# yhou0161_9103_individual-project_Perlin Noise Animation

Perlin Noise can introduce smooth random movements and enhance visual effects. For this personal assignment, I will also use Perlin Noise to create various animation effects.

## 🎮 Interaction

Since my task is to animate with Perlin Noise, the animation is random. Therefore, I didn’t create many interactions. Instead, I focused more on effects and animations. The only interaction present is a slider on the right side of the game console, which controls the movement range of the Green Ghost:
- Slide to the right to increase its range of motion.
- Slide to the left to decrease its range of motion.

The concert will play automatically after you open the window and will loop.

## 💡 Details and Approaches

In the arcade screen, we have set up five characters, including four colourful ghosts and a yellow Pac-Man. I created unique animation effects for each of these five characters.

### Red Ghost <img src="assets/RedGhost.png" width="20" height="20" />

The red ghost moves back and forth parallel to the passage it occupies. However, it is clearly more restless. Perlin Noise causes it to shake up and down, floating within the channel range, enhancing its ghostly effect.

```
function drawRedGhost() {
  // change the location
  redGhostX += redGhostSpeed * redDirection;

  // change the direction
  if (redGhostX >= 375) {
    redGhostX = 375;
    redDirection = -1;
  }else if (redGhostX <= 235) {
    redGhostX = 235;
    redDirection = 1;
  }

  //nosie to shake the ghost.
  //Redefine the range of noise to ensure that the fluctuations of the target up, down, left, and right are controlled within 5 pixels.
  let noiseX = map(noise(redGhostNoiseX), 0, 1, -5.5, 5.5);
  let noiseY = map(noise(redGhostNoiseY), 0, 1, -5.5, 5.5);

  //the frequency (larger = faster)
  redGhostNoiseX += 0.03;
  redGhostNoiseY += 0.03;

  // draw Red Ghost
  drawPixelGhost(redGhostX - 40 + noiseX, 175 + 260 + noiseY, color(255, 0, 0));
}
```

### Orange Ghost <img src="assets/Orange Ghost.png" width="20" height="20" />

Similar to the principle of the red Ghost, the Perlin Noise here controls Orange Ghost's speed. Keep it between 0.5 and 2.

```
let noiseSpeed = map(noise(orangeGhostNoise), 0, 1, 0.5, 2);
  orangeGhostY += orangeGhostSpeed * orangeDirection * noiseSpeed;
```

### Purple Ghost <img src="assets/blue Ghost.jpg" width="20" height="20" />

Compared to other ghosts, the purple ghost appears quite shy. Perlin Noise influences its transparency, causing it to flicker. The Alpha channel defines the transparency of pixels. Thus, I adjust its random range between 25 and 255 to ensure it is not completely transparent.

```
let alphaNoise = map(noise(purpleNoise), 0, 1, 25, 255);

  purpleNoise += 0.03;

  let purpleColour = color(90, 90, 255, alphaNoise);
  drawPixelGhost(purpleGhostX - 40, 285, purpleColour);
```

### Green Ghost <img src="assets/GreenGhost.png" width="20" height="20" />

The green ghost is a lively and cheerful character, and it is very eager to interact with you. I set up a slider for the green ghost, which controls the amplitude of the green ghost’s movement.

```
let noiseValue = greenGhostSlider.value();

  let noiseX = map(noise(greenNoiseX), 0, 1, -noiseValue, noiseValue);
  let noiseY = map(noise(greenNoiseY), 0, 1, -noiseValue, noiseValue);

  greenNoiseX += 0.02;
  greenNoiseY += 0.02;

  drawPixelGhost(greenGhostX + noiseX - 40, 635 + noiseY, color(0, 200, 0));
```

### Green Ghost <img src="assets/pacman.png" width="20" height="20" />

Pac-Man is the protagonist of the game, but this time it encounters four ghosts with different abilities, so it appears nervous this time. Perlin Noise affects its size, making it seem as if it is breathing tensely.

```
function drawPacman(){
  pacmanScale = map(noise(pacmanNoise), 0, 1, 1, 2);

  pacmanNoise += 0.02;

  drawPixelPacman(143, 485, color(255, 255, 0), pacmanScale);
}
```

Since my team members completed the Pac-Man drawing work, it was ineffective when I tried to change its size. Subsequently, during the inspection, I found that my teammate fixed the size in the code.

```
function drawPixelPacman(x, y, bodyColor) {
  const s = 2;
  ...
  rect(x + col * s, y + row * s, s, s);}
```

Therefore, I modified it to turn it into a variable.
```
function drawPixelPacman(x, y, bodyColor, pacmanScale) {
  const s = pacmanScale;
  ...
  rect(x + col * s, y + row * s, s, s);}
```