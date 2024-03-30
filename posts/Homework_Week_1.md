# Homework Week 1
### 2024-03-08
In our first session of week 1, we experimented with our newly developed skills in p5 to build a creative piece with code. Through utilising squares, colours, and forms of movement, we were able to create something fascinating!

For this weeks homework, our first goal is to try learn how to create a grid based on the skills we learnt this week.

![Alt text](<../static/HW1/GRIDiteration1.png>)

I first attempted to get the squares still, so I had gotten rid of the framecount and left the constand at 10, thinking it would keep the size at 10 but this wasn't the case. The squares stopped moving but were all different sizes from one another as if they were stuck in their first state of movement.

![Alt text](<../static/HW1/GRIDiteration2.png>)

In hopes of adjusting the height and width of the squares, I thought that by changing the numbers in both the height and the width it would change all the squares to one size. Instead, it left only one very small square! At this point, perhaps it's worth starting from the beginning.

![Alt text](<../static/HW1/GRIDiteration3.png>)

I started again by creating a canvas using the setup function, and I was able to set a canvas for 400x400 to create a well-sized square. From this point, I will try create a coloured square like I had done in last classes tutorial.

```js
function setup() {
  createCanvas(400, 400);
  colorMode (HSB)
  noStroke ()
   noLoop ()
}

const size = 8
```

To bring colour to the canvas and the square grids, I had set the colour mode to HSB (Hue, Saturation, and Brightness) to access a wider variation of colour.

```js
function draw() {
  for (let x = 0; x < width; x += size) {
    for (let y = 0; y < height; y += size) {
      const col = rand_col ()
      fill (col)
      square (x, y, size)
    }
  }
  ```
 I created a draw function that would bring the grid to life. 
```js
 function rand_col () {
  const h = Math.random () * 360
  return color (h, 100, 100)
}
```
This function generates a random colour to each of the grid squares. The colours are selected from the whole colour wheel as expected from the * 360.

### Choosing a work by Rafaël Rozendaal
The next part of this homework task requires us to pick a work from the creative coding artist, Rafaël Rozendaal. He makes gorgeous abstract pieces that resonate to feelings, colour, and movement. Hence, when looking through his pieces, I resonated most with this particular work titled "*'good bye farewell.com'*" (2011).

![Alt text](<../static/HW1/RAFpic1.png>)

To replicate this, I may have to do my own research as I had only worked with four dimensional shapes like squares, whilst Rozendaal has utilised circular and organic forms of line and shape to create this piece.

To be quite honest, I struggled trying to figure out how to create a circle in p5, and especially struggled in attempting to recreate the movement in the water. I hope to re-visit this with more knowledge as I develop in practice.