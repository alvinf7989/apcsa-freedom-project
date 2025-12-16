# Entry 2
##### 12/15/25

Welcome back to another blog entry for my Freedom Project of Senior Year. Last time, we left off on creating a 2d shooter on Godot and the last day I talked about it, I createed a background from Photoshop and imported it into the Godot engine. I put in three more days into this Godot tool and now it's for us to talk about how I learned my tool in each and every one of them.

## Day 4 - 11/18/25
Starting with day 4, I started to leasrn how to add sprites to my Godot game engine. The way I did this was I watched more of that [Godot Crash Course](https://www.youtube.com/watch?v=S8lMTwSRoRg) and what I did afterwards was create a `CharacterBody2D` node and put that in a separate scene, with a separate script, so I can add some features to what this sprite should do. Dragging and dropping sprites from a sprite pack that I downloaded that most fits with my current idea of the project was easier than all that stuff in Godot. After that was done I followed more steps to have one sprite in there and here was what my Godot sprite currently looks like ![Text](../screenshots/Godotex1.png) In the photo, you can see a bit of the code template that I used to make my sprite responsive in the scene.

Of course, using this code, makes my sprite on the top left corner and fall off screen because of the code below inside my script.
```java
    if not is_on_floor():
    velocity += get_gravity() * delta
```
Due to the lack of ground in the scene, the sprite has no place to land on.

## Day 5 - 12/3/25
Moving onto day 5, I fix that issue with the sprite falling off screen, I just googled how to make my sprite not fall off and just move left and right. This was the code that was given:
```java
extends CharacterBody2D

@export var speed = 400

func _physics_process(delta):
    # Get input for the horizontal axis
    var direction_x = Input.get_axis("ui_left", "ui_right")

    # Set velocity only for the x-axis
    velocity.x = direction_x * speed
    velocity.y = 0 # Ensure no vertical movement

    # Apply movement
    move_and_slide()
```
Now, I am aware of what the comments say about this code while copying and pasting it into Godot. After running that code, the sprite is static and moves ;eft and right. While that's good, the position isn't exactly where I want my ship prite to be located at. So, I googled once again to figure out how to change the sprite and it turns out i just had to set the `position` variable to `Vector2(200, 150)` The two values inside the parenthesis represent x and y values and they also put my ship at the same position of where normal 2d shooters are.
```java
func _ready():
    // Set the sprite's position to (200, 150)
    position = Vector2(200, 150)
```

## Day 6 - 12/8/25
Alright, we are onto the final day for this blog entry to talk about. I changed the size of the sprite, because it was initially way too small when being shown in the scene. When I googled how to resize a 2D sprite, they gave me this code.
```java
$player.scale = Vector2(0.5, 0.5)
```
When this was put in, an error ocurred after I pressed Start in the runner. I watched another Youtube video on [How To Scale a 2D Object in Godot](https://www.youtube.com/watch?v=hWAy7ajhg2c) and it was simple and gave me code like this:
```js
scale.x = 10
scale.y = 10
```
Well, it didn't actually give me code, I just typed in what was shown nin the video, but this works and resizes my sprite. But, I changed the values from 10 to 3, so my sprite could be the right size.

## My FP Goal for Winter Break
So, here I talk about my goal for the upcoming winter break.

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)
