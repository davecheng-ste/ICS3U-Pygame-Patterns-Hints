# Pygame Patterns: Hints
Here are some hints to help you out on your 2.10 Pygame Patterns assignment.

## Quadrant 1: Grid
Although this assignment requires the use of `for` or `while` loops, I often find it helpful to plan my code by writing things out step-by-step at first.

For example, consider these steps to [draw lines](https://www.pygame.org/docs/ref/draw.html#pygame.draw.line):

```python
pygame.draw.line(screen, BLACK, (0, 0), (0, 100))
pygame.draw.line(screen, BLACK, (10, 0), (10, 100))
pygame.draw.line(screen, BLACK, (20, 0), (20, 100))
pygame.draw.line(screen, BLACK, (30, 0), (30, 100))
pygame.draw.line(screen, BLACK, (40, 0), (40, 100))
```

Can you see a pattern developing? Look at the coordinates for `start_pos` and `end_pos`. Think about how you can use a `for` loop and `range()` function in this case to step though your sequence of `0`, `10`, `20`, `30`, `40`, etc.

<br><br>

## Quadrant 2: Circles
Drawing evenly-spaced circles requires a bit of math to divide the height and width evenly.

First, remember that the [`pygame.draw.circle(surface, color, center, radius)`](https://www.pygame.org/docs/ref/draw.html#pygame.draw.circle) function accepts the centre of a circle.

Next, think about what kind of linear grid you migle use to map out the centres of each circle. Divide your height and width based on the rows and columns of this grid.

<br><br>

## Quadrant 3: Greyscale
### Defining Colours
So far, we've been defining colours using constants, such as:

```python
BLACK = (0, 0, 0)
pygame.draw.line(screen, BLACK, (0, 0), (0, 100))
```

However, we can also do this within the draw function explicitly:

```python
pygame.draw.line(screen, (0, 0, 0), (0, 0), (0, 100))
```

Since you'll want to change the colour with each iteration, you can also use a variable for the colour. Note the use of lower_case here instead of ALL_CAPS to denote that it is a variable and not a constant:

```python
changing_colour = (0, 0, 0)
pygame.draw.line(screen, changing_colour, (0, 0), (0, 100))
```

Next, we'll look at the three numbers in a colour definition: 

`my_colour = (0, 0, 0)` or `my_colour = (red, green, blue)`

The numbers `red`, `green`, and `blue` are integers between 0 - 255 specifying the amount of each colour. Red, green, and blue in equal parts gives you a neutral white, black, or grey. Thus, you can have colours like:

```python
BLACK = (0, 0, 0)
GREY_DARK = (16, 16, 16)
GREY_LIGHT = (127, 127, 127)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
```

Think about how you can change these numbers as you iterate through your draw functions.

### Even Spacing
Finally, and perhaps the most challenging in this quadrant, is how you create an even gradient across the width of your drawing space. For this, you'll have to do some math. 

You know you have a range of 0 - 255 for black to white. 

If you computed that Quadrant 1 required 40 pixel steps for the line grid, how did you come up with this number? Consider applying the same math to the distribution of this 0 - 255 colour range.

<br><br>

## Quadrant 4: Random Colours
This quadrant builds on Quadrant 3 by changing the colour of something as the program runs.

### Generating random colours
In this case, however, you can use the [`random.randint()`](https://www.w3schools.com/python/ref_random_randint.asp) function to generate a random integer for your colour. 

Consider this code for a randomly coloured 50x50 square with top-left corner at `(x, y) = (100, 100)`:

```python
colour = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
pygame.draw.rect(screen, colour, (100, 100, 50, 50))
```
When you run this code, why does the colour continue to change?

Remember that Pygame runs inside an infinite `while` loop that goes as long as the Pygame graphics window is kept open. (This is the `while running:` line at the top of your main game loop.)

Each time the `random.randint()` function is called, a new integer value is generated at random.

### Drawing pixels
A pixel is a single 1x1 square in your 800x800 grid. You can draw a 1x1 pixel by calling the `pygame.draw.rect()` then use a `width = 1` and `height = 1`. For example:

```python
pygame.draw.rect(screen, BLACK, (100, 100, 1, 1))
```

The above would draw a single black 1x1 pixel at `(x, y) = (100, 100)`.

<br><br>


## Other Hints

### Use of `for` vs `while` for looping
Consider these two identical programs to draw a row of circles:

```python
# Initialize x_coodinate to 50
x_pos = 50

while x_pos <= 200:
    pygame.draw.circle(screen, BLACK, (x_pos, 100), 20)
    x_pos += 40  # Increment x_coordinate by 40
```

And using `for` with the `range()` function:

```python
for x_pos in range(50, 201, 40):
    pygame.draw.circle(screen, BLACK, (x_pos, 100), 20)
```

Hopefully, you can see how much easier it is to read the code using `for` and `range()`. The parameters for `x_pos` are all listed on the same line:
- `x_pos` starts at `50`
- `x_pos` stops at `201` (NOTE: Remember, `range` is not inclusive, so if we want `200` to be the final value, we need to specify a number greater than `200`.)
- `x_pos` increases or steps by `40` on each iteration

If you are using `while` loops in your implementation, consider replacing them with `for` and `range()` functions for cleaner code.