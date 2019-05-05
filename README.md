# Flappy Birds
<img width="567" alt="屏幕快照 2019-05-04 下午10 50 43" src="https://user-images.githubusercontent.com/47285199/57200030-240b8880-6f3b-11e9-98e4-8d818c027d42.png">

It is a interactive game with a creepy vibrating bird jump over the galaxy obstacles by clicking up arrow key.

## Summary

I attempt to make the bird keep bouncing when it still on the ground to make it looks funny. And I make the galaxy obstacles different sizes to make it visually more interesting.
When players use play it at the online editor, they have to click the Preview Screen at first before they using up arrow key to jump.

## Component Parts

I has images that create the character of bird and obstacles. There is an color gradient for backgroud from yellow to green so that the visual part
of this game is more appealing to people. Besides, there is text said Game Over when the bird touch the obstacle.

So there are two movement in this game, one is the bird jumping, another is obstacle moving from right to left.

## Timeline

What did you do in each of the past four weeks?

- Week 0: Write Proposal
- Week 1: Writing first draft
- Week 2: Writing and improve my code with CCA coach
- Week 3: To solve the problem I have
- Week 4: Present!

## Challenges

I think it is really interesting to see that add images can make the game looks like those games in Apple Store. But to make the bird jump is a big
challenge for me because the caculations. Also, I had a problem of writing key code but I finally figured it out with the help of teacher.
I think the Examples Library of p5.js is really helpful for us as a reference!
## Completed Work

Link to the editor:
https://editor.p5js.org/xinyaoxu/sketches/Vtl7mROZ1

```javascript
var bg;//Before you jump, clikc the screen at first.
var flight;
var score= 0;
var bgstep = 0; //Background

var fl_y = 0;
var vy = 0; //Jump

var obst_x = 1200;
var obst_y;
var obst_size = 80; // obstacle

var over_flag = 0; // game over

var num = 4;
var picNo = 0;
var pic_cnt = 0;
var walker = new Array(num);

function preload() {
 bg = loadImage("2.jpg");
  flight = loadImage("a.png");
  d = loadImage("b.png");
  /////////////Picture
  for (var i = 0; i < walker.length; i++) {
    walker[i] = loadImage("walker" + i + ".png");
  }
    soundFormats('wav');
  mySound = loadSound('1.wav');
}
  

function setup() {
  createCanvas(800, 600);
  frameRate(150);


  fl_y = height / 4 * 2;
  obst_y = height / 4 * 3;
}


function draw() {

  //background movement 
  bgstep = bgstep - 1;
  if (bgstep <= -5600) {
    bgstep = 0;
  }
  image(bg, bgstep, 0);

  //check if the game is over
  if (dist(width / 3, fl_y, obst_x, obst_y) <= (obst_size / 3)) {
    over_flag = 1; //gameover
  }
  ///////////////////////Avoide obstacles

  if (over_flag == 0) {
    //bird move
    obst_x = obst_x - 5;
     // if (obst_x== width/2-obst_size/2) {
     //  score+=10;
     // }
    if (obst_x + obst_size <= 0) {
      obst_x = width + obst_size;
      var size = random(100, 200);
      obst_size = size;
    
    }

    //Jump
    vy = vy + 0.4;
    fl_y = fl_y + vy;
    if (height / 6 * 5 < fl_y) {
      fl_y = height / 4 * 3;
    }
  }

  if (height / 6 * 5 <= fl_y) { //walk
    pic_cnt++;
    if (pic_cnt >= 10) {
      pic_cnt = 0;
    }

    if (pic_cnt == 0) {
      picNo++;
      if (picNo >= num) {
        picNo = 0;
      }
    }
    image(walker[picNo], width / 3, fl_y, 142, 77);
  } else {
    image(flight, width / 3, fl_y, 142, 90);
  }


  image(d, obst_x, obst_y, obst_size, obst_size); //bird


  /////////////When Game is over
  if (over_flag == 1) {
    fill(255, 0, 0, 100);
    textAlign(CENTER);
    textSize(48);
    text("GAME OVER", width / 2, height / 5 * 3);
  }
}

////Keyboard 
function keyPressed() {
   mySound.stop();
  if (keyCode == UP_ARROW) {
    mySound.play();
    print("Up key kit");
    if (fl_y >= height / 4 * 3) {
      vy = -15; //speed upward
    }
    
  }
}

```

## References

P5.js Example Library
