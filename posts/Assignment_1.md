# A1: Cute! Documentation
#### Published 2023-03-31
### Introduction 
This first creative coding assignment requres us to explore the conventions of a 'Cute!' creative genre in p5. However, this first poses the question of: what makes a creative coding piece 'Cute'? This is something I hope to explore and iterate on upon further research and implementation of practice. I will also look to the works of artists such as Rafaël Rozendaal and course content to build my knowledge further.

### Reading Sianne Ngai - Zany, Cute, Interesting (Wark 2020)

The aesthetic idea of 'cute' derives from the word acute (Wark, 2020), creating a cute version of a more-so edgy word. Ngai delves into the contrast yet astonishing balance of the 'zany' and 'cute'. The sharp and the fuzzy. The zany focuses on the 'performance' of objects, whilst the cute represent the 'being' of the subject in itself. To see and imagine the genre of cute, we must understand first the contextual ideas behind it.

The word cute, or kawaii in Japanese sounds almost to similar as Kowai - scary. From this alone, we are almost able to understand, see, and feel the affect of this genre. That the cute can be sweet, but biting and chaotic (Wark, 2020).

From this reading, my understanding of the cute phenomenon and intricately simple aesthetic is that; the cute requires a balance between coherance and a little bit of chaos. This brings about a feeling of interest within an aesthetic composition of work due to its sweet aesthetic, and the movement between calm and subtle chaos. This is something I hope I'll be able to achieve in my assignment, therefore i will take into consideration the use of colour, shape, and composition.

### Looking at Creative Inspiration! Rafaël Rozendaal

When looking at the different works of Rozendaal, I looked to the ones that spoke most to me in the genre of 'Cute'. I started with:

pink yellow blue (2014)
![Alt text](<../static/HW1/rafweek2.png>)
I liked the colours as well as the floating/wandering objects (the square and the circle)! I hope to incorporate this aspect somewhat in my work.

deep sadness (2014)
![Alt text](<../static/A1/RAFas3.png>)
I absolutely adored the interactivity when clicking the mouse! I find that it is very engaging, somewhat cute yet somewhat chilling due to the sound effects when clicked. I also liked the change of colour in the background and shape. Whilst I feel like I may not be exactly sure on how to incorporate this, I hope I will at least be able to add shape, sound, and changing colours of the background!

double never (2017)
![Alt text](<../static/A1/RAFas5.png>)
This artwork I found interesting as I adored the movement of the sharp edges. I feel like if I were to create something similar like this, I would bring it closer to Ngai's genre of cute through a change in colour. However, I may not work with this idea as I am quite unsure on how I can recreate this movement, and I hope to learn so in future!


### Iterative Process
To kick off the first step of this assignment, I first must create a setup function to create a canvas. This assignment requires the sketch to be presented full screen, so to do that;
```ps
function setup() {
  createCanvas(400, 400);
  createCanvas(displayWidth, displayHeight);

  background(200);
}
```
I then want to set a colour mode and the order of colours that appear on my background. So this is what I input into the setup function;
```ps
colorMode(HSB, 100);

  for (let x = 0; x < 100; x += 1) {
    for (let y = 0; y < 100; y += 1) {
      stroke(x, y, 100);
      point(x, y);
    }}
```
However, after doing this I found that the colours did not suit the aethetic vision I aimed for as it went through dark reds instead of lighter/higher value hues. Therefore, I will attempt to change this.

```ps
bgColor = color( random(255), random(255), random(255) );
```
Using this allows me to set a random colour without going through mostly reds. I do like the look of this more as it chooses from a various amount of colours on the wheel with less clicks. However, I find that it still occasionally picks dark blues and reds. This is something I am not quite fond of, but I hope I can learn to change this in future practice!

The coding I used to allow users to click the screen was;
```ps
// Allows user to interact (click mouse) 
    function mousePressed(){
      
      // Background changes colour when clicked
      bgColor = color( random(255), random(255), random(255) );
    }
```
This was suprisingly easy to figure out! I had to look at the p5 references to understand the code, but was suprised at how little steps it took.

This is what my cont and var list currently looks like:

```ps
// LIST OF CONSTANT
  // Creates 35 circles
  const NUM_CIRCLES = 35;
  // Movement speed
  const FLOAT_SPEED = 2;
  // Size of circle
  const CIRCLE_SIZE_DIVISOR = 12;

  // VARIABLES
  // Background Colours
  var bgColor; 
  // X direction
  var circledirectionx = 1;
  // Y direction
  var circledirectiony = -1;
  // Sound Effect
  var note;
  // Stores all 25 circles
  let circles = [];
  // Boolean logic - makes circles float around screen
  let float = true;
```
I created a list for my constants as well as variables! I am hoping to add sound effects, so I had added that in my variables as 'note'. If I cannot seem to figure this out, I will comment this out as it's not essential in my idea, but more so of a preferred touch!

To create moving circles in my sketch, I had to first create constants and variables. I iterated between different sizes; 50, 40, 30, and 25 (higher is smaller, lower is bigger). I found I liked 25 circles as it filled the screen and matched well with the speed I ideated.



As I was going through my code, the console told me that there was a missing value or number for my circle position. However, I struggled to figure it out..

```ps
// draws circle in array
      for (let i = 0; i < circles.length; i++) {
  
        // Draw the circle new position (wrong sybtax?)
        // ellipse(cicrcle.x, circle.y, circleSize, circleSize);
        ellipse(circle.x, circle.y, circleSize, circleSize);
      }
```
After checking I had realised I left out two lines that aided in setting the circle positions using'if'. This was the part of code I didn't think to add (should have been under 'let'.) However I had figured it out (as shown below) and now have working circles!

```ps
let circle = circles [i];
```
When looking at the circles, I didn't quite like how the circles would disappear off the frame. So I changed the direction and bounce code from:
```ps
 // Test to see if the shape exceeds the boundaries of the screen
      // If it does, reverse its direction by multiplying by -1
      if (circle.x > width - random || circle.x < random) {
        xdirection *= -1;
      }
      if (circle.y > height - random || circle.y < random) {
        ydirection *= -1;
      }
```
  To then:
```ps
if (circle.x > width - random || circle.x < CIRCLE_SIZE_DIVISOR) {
        circle.x *= -1;
      }
      if (circle.y > height - random || circle.y < CIRCLE_SIZE_DIVISOR) {
        circle.y *= -1;
      }
```
However, now that the circles didn't disappear off to the sides, the circles moved alomg the edge instead of bouncing off when coming into contact with the sides of the screen. I attempted to fix this with:

```js
    // Off the left screen
    if(circle.x < 0){
      circledirectionx = circledirectionx*-1
    }
    
    // Off the right screen
    if(circle.x > width){
      circledirectionx = circledirectionx*-1
    }
       
    // Off the top of screen
    if(circle.y < 0){
      circledirectiony = circledirectiony*1;
    }
        
    // Off the bottom of screen
    if(circle.y > height){
      circledirectiony = circledirectiony*1;
    }
```
This however, still didn't quite work for me even when adding circledirectionx and circledirectiony as a variable. From here, I will try work out a different method.

```ps
 // Draws circle in array
      for (let i = 0; i < circles.length; i++) {
        let circle = circles [i];
        if (float) {
          // Update the circle position based on its speed
          circle.x += circle.speedX;
          circle.y += circle.speedY;
          
        }
          // Checks collision with left and right sides, reverse back
          if (circle.x < 0 + circleSize / 2 || circle.x > width - circleSize / 2) {
            circle.speedX = -circle.speedX;
          }
        
        if (circle.y < 0 + circleSize / 2 || circle.y > width - circleSize / 2) {
            circle.speedY = -circle.speedY;
          
       } else {
          
        }
    
  
        // Draw the circle new position (wrong sybtax?)
        // ellipse(cicrcle.x, circle.y, circleSize, circleSize);
        ellipse(circle.x, circle.y, circleSize, circleSize);
      
      }
```

This took a few hours to figure out after checking the module and p5 help referencing. I struggled to understand setting up collisions, but figured it out! All comments are on my sketch.

AFter this I wanted to add multiple sound effects by adding sound files (wav) from a free audio library Pixabay.com! I then shortened the wav files to fit into one second to play nicely when user clicks - preventing any empty spaces before sound. However, when trying to implement the sound effects randomly, I struggled to figure out how to randomize sound effects when clicked. Therefore, I stuck with one sound that felt 'cute' yet slightly 'chaotic' when interacted with.

```ps
// If clicked, sound plays, if not, no sound
      if ( note.isPlaying() ) { // .isPlaying() returns a boolean
        
        note.stop();
        background(255);
        
      } else {
        
        note.play();
        background(0);
      }
```
This worked as I had previously added the sound effect file in the setup function:
```ps
// Loads in sound effect
      note = loadSound('quack.wav');
```

I am quite happy with this result as I personally struggled with the fundamentals. However, I am now quite excited to learn more!!

<iframe src="https://editor.p5js.org/NICALOD3ON/full/KK-eQZj8q"></iframe>
