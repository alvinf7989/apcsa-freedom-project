# Tool Learning Log

## Tool: **Godot**

## Project: **A 2d Shooting Game**

---

### Day 1 - 9/29/2025:
* So, starting this day was when I decided on using the tool Godot. However, I didn't know much about this app, so I watched this [Crash Course](https://www.youtube.com/watch?v=S8lMTwSRoRg) on YouTube and it teaches me how to get started on it. So far I followed its steps by creating a button and setting a 2d Scene for my project. When I first tried to add text, it didn't seem to pop up on the black button. I didn't know what was wrong, but it turns out that the text was too small from the 2d scene.

### Day 2 - 10/27/2025:
It has almost been a month since I updated my learning log. Anyways, I watched more of that [Crash Course](https://www.youtube.com/watch?v=S8lMTwSRoRg) on YouTube, and I learned some new functions like giving my play button the ability to change scenes after it has been clicked. Here's the code that was put in the script:
```js
func _on_play_pressed() -> void:
	get_tree().change_scene_to_file("res://shooter_area.tscn")
```
In the function, it will determine that when the play button is pressed, the 2nd line of code will run where it changes the scene to the file where the link to that scene is in parenthesis. Afterwards, I put in a label like the guy in the video did on the shooter area scene where it says, "This is the label."

### Day 3 - 11/7/2025:
It's the next day, and I have decided to try and create a background to put in my shooting area. I went back to photoshop like my previous freedom project and created a background that would scroll once the user hits the play button. This meant that I had to remove the label and export my background as a png to drag into my Godot project. Now, I watched the crash course video once again and he had his background scrol horizontally, while I had mines move vertically. Here was my code:
```js
extends ParallaxBackground

var scrolling_speed = 100

func _process(delta):
	scroll_offset.y += scrolling_speed * delta
```
The mathematical operator for the `scroll_offset` part of this code is to change direction depending on the axis the background is scrolling on. For my code, I chose to have the background scroll downwards by setting the offset to y instead of x like in the video. If it was `-=`, the background would scroll up. Now before this, I had issues with how to get this to work, like how I have to change the script line where it says `extends` to Parallax Background.

After that has been finished, I had to adjust the mirroring for the y-value of the background, so it could repeatidely scroll infinite backgrounds. Without this, the background would just move downwards leaving the screen.

### Day 4 - 11/18/25
On the 4th day, I learned how to add my ship sprite to my background. I watched more of that Godot Crash Course and added my ship sprite from the spaceship shooter gamekit pack that I just downloaded. So, what I did was add a new node which was called `CharacterBody2D` in a separate scene, attached a separate script to that scene, and I added a capsule collision shape node, so we know where the ship sprite's hitbox is. How I even got the sprites from the pack to pop up in the Godot project was through dragging and dropping.

Now I could only find a sprite sheet of the ship, so when making sprite frames, I selected one frame to be the ship by setting the horizontal to 2 and the vertical to zero, and simply selected one. ![Text](../screenshots/Godotex1.png) Seen on the image below shows the script being made by attaching a node script to the player sprite. I chose a default "CharacterBody2D: Basic Movement" template to have the script that's shown. Now witth the entire script attached, once the user presses play from the starting scene. the ship sprite appears on the top left corner as tiny and then falls off screen.
```js
if not is_on_floor():
		velocity += get_gravity() * delta
```
This function is the reason for why it falls off screen because there is no ground or floor or anything for the sprite to collide on. This code itself adds gravity according to the comments of the template.

### Day 5 - 12/3/25
So, it's the next day, and where I left off, whenevr I ran the game, my sprite fell off screen from the top left. So, what I did was google how to change script to try and change that, so I deleted the previous script, thinking I would have to find a new template, but I didn't. So, I googled on how to make my sprite not fall off and only move left to right, and it gave me this code
```js
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
So, I copied this, and don't worry, I see the comments that tell me what these functions do. Now when running the code, the spite successfully stays and moves left and right, the only issue is it's on the position, I don't want it to be. So, I googled once again on how to change position of the sprite and it said that I got to put in this code
```java
func _ready():
    # Set the sprite's position to (200, 150)
    position = Vector2(200, 150)
```
What this does is set the sprite's position at xertain axes by setting the position to the vector with x and y values in the parenthesis. The initial values seen on the code above have my spaceship on top, usually where the enemy is located, so I changed both values to 550, to finally put the sprite in the position like normal 2d shooter games do.

### Day 6 - 12/8/25
It's the next day, and I decided to change the size of my ship sprite. I looked up on Google how to change size of a 2d sprite and I tried putting in this code:
```js
$player.scale = Vector2(0.5, 0.5)
```
I thought this would work, but when I ran the code, it gave me an error after I pressed start. So I watched another Youtube video on [How To Scale a 2D Object in Godot](https://www.youtube.com/watch?v=hWAy7ajhg2c) and it turns out I just had to use this code:
```js
scale.x = 10
scale.y = 10
```
When I tried 10 for these values, the ship sprite was too big for me, so I tested 5, and then finally 3 to get my ship sprite at just the right sides.

### Day 7 - 12/30/25
I am back on December and felt like I should do one last tool tinkering day of the year before 2026. I was starting on duplicating the sprites first but when I tried this on the script it was really confusing and any number I put in the `Vetcor2()` value wasn't working, so I decided to add the small ship sprites and with a Googling trick, I was able to figure out that I don't need to use the script to make changes on the positioning I just created two sprite 2d nodes as children of the 2dCharcaterBody and to add the sprites I went to the texture part in the right side and looked for the small ship sprites. ![](../screenshots/position-values.png) Now I can't change how big this screenshot is, but if you look at the position section you'll see I put 30 px as the values to turn my sprite to the right, -30 to go to the left. I also change the angle to 180 because they seemed upside down when I ran the code. Finally, I adjusted the y-value to go a little more down enough to make them fit with the main player sprite. So far, I'm meeting half of my Winter Break goal.

### Day 8 - 1/12/26
Welcome to the first learning log day of 2026, previously I added 2 small ship sprites on each side of the main ship sprites. What I wanted to do was add another ship sprite at the top as part of my goal from one of my blog entries. The ship sprite would be the same as the main sprite at the bottom but it would be a different color. So, I added another Sprite2D node to represent the top ship, then since the other ships were too small, I decided to add my previous ship that I've used before. Of course there's two of them, and since I don't know how to make it one sprite, I had to improvise and take the frame from my AnimatedSprite2D node. I also noticed my orginal ship sprite was upside down so I changed the rotation value of that sprite to 180 degrees to flip it. Unfortunately, while I did good on putting the ship sprite up top, the color still remains the same and I'm trying to change it.

### Day 9 - 2/2/26
Another day, another Godot review. So, I left off on trying to figure out how to change the code, but then went to a different step which is making the top ship still even when I'm oving my bottom ships, because right now, it's moving with my ships in sync. I don't want that, so I tried creating a script and googling solutions. Yes, I used Google again. I tried many scripts, but nothing worked. I then enabled Top-level which was in the Inspector section of my sprite that caused my top ship to disappear. Here was the final script that I used.
```java
extends Sprite2D

func _ready():
	# Set the global position when the scene loads.
	global_position = Vector2(555, 100)
```
This was to fix that issue of the ship not showing up. I tinkered with the x value, so it wasn't originally 555. Once I set up that position it's tiny now. Which means I gotta change the scale from (1, 1) to (2, 2). After doing such a thing, The ship is now still and no longer moves with the bottom ships.
<!--
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
