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