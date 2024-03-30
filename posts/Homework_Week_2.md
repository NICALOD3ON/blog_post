# Homework Week 2
### 2024-03-13

Welcome to my Week 2 documentation! Before I get into my homework task, I want to utilise this space fot further note taking and learning. We took the time today to 

if phase is redundant you put it into the fallers array

when we say new faller in the sketch tab, it sets the colours array and curves array in the faller class. This makes it efficient when wanting to add a new faller object, rather than retyping code or copy-pasting into the sketch. 

This is like defining a method - which is a function that lives in an object.

For this homework task, I found it quite challenging to wrap my head around what a 'class' was and how to set one up. Due to this, I looked for extra help in understanding. I learnt that by creating a class, the sketch tab will be able to read the class easier and input will be more efficient, as it refers to the class and its internal scripting.

```js
class Faller {
  constructor (bg) {
    this.colours = [ bg, rand_col () ]
    this.start_points = [
      { x: 0, y: height / 2 },
      { x: 0, y: 0 },
      { x: width / 4, y: 0 },
      { x: width / 2, y: 0 },
      { x: width * 3 / 4, y: 0 },
      { x: width, y: 0 },
      { x: width, y: height / 2 },
    ]
    this.end_points = []
    for (let i = 1; i < 8; i++) {
      this.end_points.push ({
        x: i * width / 8,
        y: height
      })
    }
    this.curves = new Array (7).fill ().map (rand_curve)
    this.phase  = 0
  }
  
  draw () {
    colorMode (RGB)
    fill (lerpColor (this.colours[0], this.colours[1], this.phase))
    beginShape ()
    vertex (0, height)
    this.start_points.forEach ((s, i) => {
      const p = find_point (s, this.end_points[i], this.phase ** this.curves[i])
      vertex (p.x, p.y)
    })
    vertex (width, height)
    endShape ()
    this.phase += 0.008
  }
}

function find_point (start, end, phase) {
  const delt = {
    x: end.x - start.x,
    y: end.y - start.y
  }
  const x = start.x + delt.x * phase
  const y = start.y + delt.y * phase
  return { x, y }
}

function rand_col () {
  colorMode (HSB)
  const h = floor (random () * 360)
  return color (h, 100, 100)
}

function rand_curve () {
  return random () * 2 + 1
}
```
This is still quite confusing to me, however I hope that in time and practice, I will be able to understand the fundamentals and pieces within the structure easy to follow along with.

What I understand from this currently is that its important to create points for the start and end phase. There are 8 points at the start and end. This allows for the fallers to fall toward the middle - creating almost an arch.

The random colour and random curve functions enable each of the fallers to have a different colour, whilst also falling at different levels and curves.

#### Choosing a work by Rafaël Rozendaal

![Alt text](<../static/HW1/rafweek2.png>)
This work 'pink, yellow, blue' by Rozendaal is something I hope to recreate. This seems simpler than the last inspirational work I looked to, and also intertwines well aesthetically with the assignment. However, I wonder how Rozendaal achieved these colours? I wonder what he had put in the colour colour mode. My guess would be HSB as the hues have differing saturation and brightness levels in this screen print! I hope I can figure out how Rozendaal made the two shapes slowly move around yet not overlap each other. This is something I hope to implement in my assignment.