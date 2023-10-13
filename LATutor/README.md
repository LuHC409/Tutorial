# OOP
In this project, we used the core concepts of object-oriented programming, including the following key points:

Classes and Objects:

We created a class named Ball that has properties and methods that describe the blobs.
Each ball is an instance of the Ball class with separate properties and methods.

Encapsulation:

Encapsulation is the concept of wrapping data and related operations in an object.
In the Ball class, we encapsulate the properties of the ball such as position, radius, and speed, as well as the methods for updating and displaying the ball.


First let's draw a very simple circle
```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(200);
  fill(255,0,0);
  ellipse(width/2,height/2,50,50);
}

```
Before learning object-oriented programming, we had actually been doing procedural-oriented programming. This circle we have drawn is not actually an object, so it's very hard for us to modify it. What if we want to do some modifications on what we have drawn. Hence the concept of object need to be brought up.
Now lets look at the basic syntax of OOP
```javascript
class Ball {
  constructor(x, y, radius, speedX, speedY) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.speedX = speedX;
    this.speedY = speedY;
  }
}
function setup() {
  createCanvas(400, 400);
}
function draw(){
    pass
}
```
This code defines a class named Ball, which is a classic example of object-oriented programming (OOP). Let's go through each part of this class definition:
class Ball { ... }: This line starts the definition of a new class named Ball. In OOP, a class is an abstract blueprint that describes a category of objects, in this case, representing balls.

constructor(x, y, radius, speedX, speedY): This is the class constructor. The constructor is automatically called when a new instance (object) of the class is created. It accepts parameters (in this case, x, y, radius, speedX, and speedY) and uses them to initialize the properties of the newly created object.

x: Represents the horizontal position of the ball.
y: Represents the vertical position of the ball.
radius: Represents the radius of the ball, determining its size.
speedX: Represents the speed of the ball in the horizontal direction.
speedY: Represents the speed of the ball in the vertical direction.
this.x = x; and similar statements: These statements assign the values of the constructor's parameters to the properties of the newly created object. The this keyword refers to the current object, allowing us to access and use its properties. So, this.x represents the x property of the object, and it assigns the value of the x parameter from the constructor to this property, making it accessible for later operations.

```javascript
class Ball {
  constructor(x, y, radius, speedX, speedY) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.speedX = speedX;
    this.speedY = speedY;
  }
}
function setup() {
  createCanvas(400, 400);
  let ball = new Ball(100, 200, 20, 2, -1);
}
function draw(){
    pass
}
```
However it now looks like this
![image](assets/1.png)
This is because we just defined a certain object, but we did not do anything to display it.
Now lets display it
```javascript
class Ball {
  constructor(x, y, radius, speedX, speedY) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.speedX = speedX;
    this.speedY = speedY;
  }
  display() {
    fill(255, 0, 0);
    ellipse(this.x, this.y, this.radius * 2);
  }
}
function setup() {
  createCanvas(400, 400);
  let ball = new Ball(100, 200, 20, 2, -1);
}
function draw(){
    ball.display()
}
```
Now let's see the result of the codes
![image](assets/2.png)

To sum up, the display function we called is to make the ball shown.

Now let us make the ball to move:
```javascript
class Ball {
  constructor(x, y, radius, speedX, speedY) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.speedX = speedX;
    this.speedY = speedY;
  }
  display() {
    fill(255, 0, 0);
    ellipse(this.x, this.y, this.radius * 2);
  }
  update() {
    this.x += this.speedX;
    this.y += this.speedY;

    if (this.x + this.radius > width || this.x - this.radius < 0) {
      this.speedX *= -1;
    }
    if (this.y + this.radius > height || this.y - this.radius < 0) {
      this.speedY *= -1;
    }
  }
}
function setup() {
  createCanvas(400, 400);
  let ball = new Ball(100, 200, 20, 2, -1);
}
function draw(){
    ball.display()
    ball.update()
}
```
After having the function update, now we changed the static ball into a bouncing ball.
It looks like this
![image](assets/3.gif)

We have already learned to draw a basic bouncing ball, what we are doing now is actually transforming the ball into an object.
Now we know the basic syntax of the OOP, let's make a project based on that:
```javascript
let balls = [];

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  for (let ball of balls) {
    ball.update();
    ball.display();
  }
}

function mousePressed() {
  for (let ball of balls) {
    let d = dist(mouseX, mouseY, ball.x, ball.y);
    if (d < ball.radius) {
      ball.accelerate();
    }
  }
}

class Ball {
  constructor(x, y, radius, speedX, speedY) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.speedX = speedX;
    this.speedY = speedY;
  }

  update() {
    this.x += this.speedX;
    this.y += this.speedY;

    if (this.x + this.radius > width || this.x - this.radius < 0) {
      this.speedX *= -1;
    }
    if (this.y + this.radius > height || this.y - this.radius < 0) {
      this.speedY *= -1;
    }
  }

  display() {
    fill(255, 0, 0);
    ellipse(this.x, this.y, this.radius * 2);
  }

  accelerate() {
    this.speedX *= 1.5;
    this.speedY *= 1.5;
  }
}

function keyPressed() {
  if (key === ' ' && balls.length < 5) {
    let radius = random(10, 50);
    let x = random(radius, width - radius);
    let y = random(radius, height - radius);
    let speedX = random(-3, 3);
    let speedY = random(-3, 3);
    let ball = new Ball(x, y, radius, speedX, speedY);
    balls.push(ball);
  }
}

```

Now we will have a accomplished project, you can add ball by clicking the SPACE and it will accelerate once you clicked on the balls.
Feel Free to copy the code and try it in your own sketch. The final project looks like this:

![image](assets/4.gif)