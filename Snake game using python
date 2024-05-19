# Imports
import turtle
import time
import random

# Score and delay
current_score = 0
high_score = 0
movement_delay = 0.1

# Set up the screen
game_screen = turtle.Screen()
game_screen.title('Snake Game by Subhonil')
game_screen.bgcolor("blue")
game_screen.setup(width=800, height=700)
game_screen.tracer(0)  # Turns off screen updates

# Outline of the playing field
boundary_drawer = turtle.Turtle()
boundary_drawer.speed(0)
boundary_drawer.shape('circle')
boundary_drawer.color('black')
boundary_drawer.penup()
boundary_drawer.hideturtle()
boundary_drawer.goto(310, 310)
boundary_drawer.pendown()
boundary_drawer.goto(-310, 310)
boundary_drawer.goto(-310, -310)
boundary_drawer.goto(310, -310)
boundary_drawer.goto(310, 310)
boundary_drawer.penup()

# Snake head
snake_head = turtle.Turtle()
snake_head.speed(0)  # 0 is the maximum animation speed of turtle module
snake_head.shape("circle")
snake_head.color('black')
snake_head.penup()
snake_head.goto(0, 0)
snake_head.direction = 'stop'

# Snake Food
snake_food = turtle.Turtle()
snake_food.speed(0)  # 0 is the maximum animation speed of turtle module
snake_food.shape("square")
snake_food.color('red')
snake_food.penup()
snake_food.goto(0, 100)

# Contains information about snake body
snake_body_segments = []

# Pen
score_pen = turtle.Turtle()
score_pen.speed(0)
score_pen.shape('circle')
score_pen.color('white')
score_pen.penup()
score_pen.hideturtle()
score_pen.goto(0, 310)
score_pen.write('Score: 0 High Score: 0',
                align='center',
                font=('Courier', 24, 'normal'))


### Functions
# Function to update the score
def update_score():
    score_pen.clear()
    score_pen.write('Score: {} High Score: {}'.format(current_score,
                                                      high_score),
                    align='center',
                    font=('Courier', 24, 'normal'))


# Functions that move snake in response to keyboard keys
def move_up():
    if snake_head.direction != 'down':
        snake_head.direction = 'up'


def move_down():
    if snake_head.direction != 'up':
        snake_head.direction = 'down'


def move_left():
    if snake_head.direction != 'right':
        snake_head.direction = 'left'


def move_right():
    if snake_head.direction != 'left':
        snake_head.direction = 'right'


# Function that helps the snake move
def move_snake():
    # Move the end segments first in reverse order
    for index in range(len(snake_body_segments) - 1, 0, -1):
        x = snake_body_segments[index - 1].xcor()
        y = snake_body_segments[index - 1].ycor()
        snake_body_segments[index].goto(x, y)
    # Move segment 0 to the head
    if len(snake_body_segments) > 0:
        x = snake_head.xcor()
        y = snake_head.ycor()
        snake_body_segments[0].goto(x, y)
    # Keep the snake moving in the same direction
    if snake_head.direction == 'up':
        snake_head.sety(snake_head.ycor() + 10)
    if snake_head.direction == 'down':
        snake_head.sety(snake_head.ycor() - 10)
    if snake_head.direction == 'left':
        snake_head.setx(snake_head.xcor() - 10)
    if snake_head.direction == 'right':
        snake_head.setx(snake_head.xcor() + 10)


# Function that tells the game what to do when collision occurs
def collision():
    time.sleep(0.5)
    snake_head.goto(0, 0)
    snake_head.direction = 'stop'
    # Hide the segments
    for segment in snake_body_segments:
        segment.hideturtle()
    # Clear the segments list
    snake_body_segments.clear()
    current_score = 0
    update_score()
    # Reset the delay
    movement_delay = 0.1


### Keyboard bindings
game_screen.listen()
game_screen.onkeypress(move_up, 'Up')
game_screen.onkeypress(move_down, 'Down')
game_screen.onkeypress(move_left, 'Left')
game_screen.onkeypress(move_right, 'Right')

### Loop that runs the game code
while True:
    # Updates the window repeatedly
    game_screen.update()

    # Check for collision with border
    if snake_head.xcor() > 290 or snake_head.xcor() < -290 or snake_head.ycor(
    ) > 290 or snake_head.ycor() < -290:
        collision()

    # Check if the snake eats the food
    if snake_head.distance(snake_food) < 20:
        # Move the food to a random spot
        snake_food.goto(random.randint(-290, 290), random.randint(-290, 290))
        # Add a segment
        new_segment = turtle.Turtle()
        new_segment.speed(0)
        new_segment.shape('circle')
        new_segment.color("grey")
        new_segment.penup()
        snake_body_segments.append(new_segment)
        # Shorten the delay - this increases speed of snake as it gets longer
        movement_delay -= 0.001
        # Increase the score
        current_score += 10
        if current_score > high_score:
            high_score = current_score
        update_score()

    # Move the snake in the game
    move_snake()

    # Check for head collision with the body segments
    for segment in snake_body_segments:
        if segment.distance(snake_head) < 10:
            collision()
    # Delay so that we can see things move
    time.sleep(movement_delay)

# Makes the window visible and runs everythings
game_screen.mainloop()
