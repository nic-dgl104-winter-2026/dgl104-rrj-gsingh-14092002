# Contributions – 
 
---
 
## Week 8 – Processing Basics
 
**Language:** Processing  
**Topic:** Shapes, color, and animation  
 
### Code Snippet
 
```processing
// Basic Processing sketch: animated bouncing circle
 
float x, y, speedX, speedY;
 
void setup() {
  size(600, 400);
  x = width / 2;
  y = height / 2;
  speedX = 3;
  speedY = 2;
}
 
void draw() {
  background(30);
  fill(100, 200, 255);
  ellipse(x, y, 50, 50);
 
  x += speedX;
  y += speedY;
 
  if (x > width || x < 0) speedX *= -1;
  if (y > height || y < 0) speedY *= -1;
}
```
 
### What This Code Does
 
- The `setup()` function runs once to set the canvas size and starting position of a circle, while `draw()` runs repeatedly like a loop to create animation — this structure is fundamental to how Processing works.
- The circle moves across the screen by updating its `x` and `y` coordinates each frame, and reverses direction when it hits the edge of the canvas, demonstrating basic **conditional logic** and **motion**.
- This sketch introduced me to Processing's event-driven, visual programming model, which is very different from text-based languages like Python or JavaScript, and showed how programming can be used as a creative and artistic tool.
 