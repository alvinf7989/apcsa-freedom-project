# Entry 5
##### 4/1/26

Another day calls for another blog entry. Yes, this was done one April 1st. No, this is not a joke entry. In this entry I will describe the days that I've worked on my Godot project and followed along with my plan. Matter of fact, this is the entry where I finally completed my MVP of the project. So without further ado let's take a look at...

## Day 13 - 3/16/26
Day 13 was nothing special. All I did was change the colors of the ships. How did I do that? Well, I looked through the Inspector right after putting up a screenshot of the top ship and Godot's interface and it told me to go to the Modulate property in the Visibility tab where the Inspector panel is. So I went there and this color gradient popped up ![](../screenshots/colorgrad.png) Since, I want the top ship to stand out, I changed the color to red by messing with the color gradient above.

## Day 14 - 3/20/26
Now it's the next day and I decided to add pellets to my top ship to shoot automatically every second at the bottom ship. This is to showcase a proper vice versa 2d shooter game. Of course, looking this up on Google gave me complicated results, so I realized that it would be better if I made a separate pellet scene for the top ship.

Now, I started by adding a Timer Node as the child of Top Ship to have a function happen every second as shown in the inspector section. Of course, I used code from Day 11 to have the pellets shoot at the bottom shio in the pellet scene's script for the top ship
```java
func shoot():
	var p = pellet_top.instantiate()
	get_parent().add_child(p)
	p.global_position = global_position
```
Google also said to call the `shoot()` function for the timer node called `_on_timer_timeout():`
```java
func _on_timer_timeout():
	shoot();
```
I also had to connect the timeout function to the pellet node for the top ship, so it could actually be responsive. ![](../screenshots/node-panel.png) The pellets did not pop up, and after some Googling, it told me to check off Autostart, as that's what makes the pellets pop up. Tested again, and the pellets finally pop up, but they're in the wrong direction and are too big. So, what I did was change the size the same way I did with the bottom ship's pellets. I also changed the direction by replacing the `-` to a `+` in the code `position.y -= speed * delta`.

## Day 15 - 3/23/26
You may notice I'm already up to the third day for this entry, I have worked on a total of 19 days on my Godot project. The first thing I did this day, was look at my [plan](../prep/plan.md) for my MVP, and saw that the next step was to make the top ship disappear after getting hit with enough pellets. When I looked this up on Google, it showed me that the recommendation for the amount of health the ships should have is 5, so I set a variable called `health` to be equal to 5.
```java
@export var health: int = 5
```
Then the `take_health` function was thus created with the help of Google AI and inside this function first has the health get decreased by the parameter of the function
```java
func take_damage(amount: int):
    health -= amount
    print("Top ship hit! Health remaining: ", health)
```
Then, the `if` condition for the `health` variabe has been created to have the ship disappear when health runs out.
```java
    if health <= 0:
        // You can add an explosion effect here later
        queue_free() // This removes the ship from the scene
```
Google gave me a method of testing if the code works and put a print statement after `health -= amount`. (It does) After this, I made changes to my Scene tree by setting a Collision Shape as the child of the Area2D which is also the child of the Top Ship scene overall. Now comes in the `on_area_entered` function, which was created to get the pellet to function like it would like a normal 2d shooter. Inside the function egts the parent of the current node which is the Top Ship and uses the `take_damage` function from before to remove one health and once it hits the ship.
```java
func _on_area_entered(area: Area2D):
	// Check if the thing we hit has the take_damage function
	var hit_object = area.get_parent() // Gets the Top Ship node
	if hit_object.has_method("take_damage"):
		hit_object.take_damage(1)
		queue_free() // Destroy the pellet after impact
```

## Day 16 - 3/30/26
Now today I found out that this Godot project has to go on Github, but I didn't know how to do that. Luckily, this was found in a classroom with students, which means I can ask these students about how I can have my Godot Project on Google. They showed me a video on [how to share my Godot repositories to Github](https://www.youtube.com/watch?v=qT8ut3EaIpM). When I first tried this, the repositories that I made didn't have any attributes or scenes. That's why I believe it was better to watch the whole video throughout doing this and after finishing, this is what I ended up with.![](../screenshots/gitimport.png) Now you could see for yourself how this [repository looks.](https://github.com/alvinf7989/2d-shooter-vice-versa)

## Day 17 - 4/6/26
I'm on the next day and this is during Spring Break, and boy, this was the worst task to do on my Freedom Project. I looked at the plan and it said to put in a "Game Over" screen once the player's ship has been hit with enough pellets. I thought it would be that easy. I thought just putting this in the player ship script
```java
@export var health: int = 5

func take_damage(amount: int):
	health -= amount

	if health <= 0:
		# You can add an explosion effect here later
		queue_free() # This removes the ship from the scene
```
(It's the same as the top ship's) And then this code
```java
func _on_area_entered(area: Area2D):
	// Check if the thing we hit has the take_damage function
	var hit_object = area.get_parent() // Gets the Top Ship node
	if hit_object.has_method("take_damage"):
		hit_object.take_damage(1)
		queue_free() // Destroy the pellet after impact
```
And finally setting up the connections with the functions. This is when the nightmare begins. The code doesn't work and the ship at the bottom isn't getting the pellets. I tried changing the name of the `take_damage` function because I thought that the function being related to the other ship would be the issue. That's not the case, so I tried changing the scene tree enough to have a collision and area 2d node to the player's sprite. Didn't work, so then I thought, "what if the collision shape isn't at the global position at the top ship?".

After changing the position, guess what? That doesn't fix anything! This is where I wanted to quit, but I couldn't leave without finishing my task. This took me a lot of googling and a lot of Google AI, but I was finally able to organize how my code looks and it successfully shoots the player's ship with pellets. While, I was googling, it introduced to me to groups in Godot so you might see some instances of the groups being used in the following codes.

Player's pellet:
```java
func _on_area_entered(area: Area2D) -> void:
    // Check if the thing we hit has the take_damage function
    var hit_object = area.get_parent() // Gets the Top Ship node
    if hit_object.is_in_group("enemies") and hit_object.has_method("take_damage"):
        hit_object.take_damage(1)
        queue_free() # Destroy the pellet after impact
```

Top ship:
```java
func _on_area_entered(area: Area2D) -> void:
	// Check if the thing that hit us is a PLAYER pellet
	if area.is_in_group("player_bullets"):
		take_damage(1)
		area.queue_free() // Destroy the pellet that hit us
```

Enemy's pellet:
```java
func _on_Enemy_area_entered(area: Area2D) -> void:
	var hit_obj = area.get_parent()

	if hit_obj.is_in_group("players") and hit_obj.has_method("take_damage"):
		hit_obj.take_damage(1)
		queue_free()
```

Player ship:
```java
func _on_area_entered(area: Area2D) -> void:
	# Only take damage from ENEMY pellets
	if area.is_in_group("enemy_bullets"):
		take_damage(1)

func take_damage(amount: int):
	health -= amount

	if health <= 0:
		// You can add an explosion effect here later
		queue_free()
```
Here are all the scenes with the group names that are listed and grouped respectively.
* Pellet - player_bullets
* Pellet Top - enemy_bullets
* Top Ship - enemies
* Player - players

The last thing that was fixed was the layering and masking for both ships, so they have proper hitboxes. When running this code, both ships disappear when the top ship hit's the player ship enough times, which would be a place for a "Game Over" screen, but after working hard on this, I decided to leave that for tomorrow.

## Day 18 - 4/7/26
It's tomorrow, and before I made my Game Over screen, I git cloned my repository with my Godot project into my IDE, so I can save commits to it. Now, I googled how to add text to Godot after a certain point, and Google's AI told me to define a signal that the player has died and have that emitted when the player's health is less than or equal to 0.
```java
signal player_died

if health <= 0:
		player_died.emit()
```
This was all that was put in the player ship's script by the way. Then, I had to add a child node known as the label and then put in text saying "GAME OVER!". Google showed me how to put the GAME OVER screen on when the signal's emitted and that's when the `hide`, `connect`, & `show` methods were put into play.
```java
func _ready():
	// Hide the text immediately when the game starts
	game_over_label.hide()

	// Connect to the player's signal
	player.player_died.connect(_on_player_died)

func _on_player_died():
	// This runs the moment queue_free() is called in the player script
	game_over_label.show()
```
The label is called `game_over_label` and all of this code was put in the shooter area's script. The reason the code didn't work though while I was testing it was because of the `@onready` variables. It was hard to find the location of the game_over_label when it's in a different scene compared to the player's scene. That's when I learned that I can drag the nodes into my code and drop them while holding cmd to get the `@onready` variable.
```java
@onready var player = get_node("../CharacterBody2D")
@onready var game_over_label = $ParallaxLayer/gameover
```
Now Google also gave me a thing to test if the code works which was a print statement in an `if` statement where the `connect` method is located.
```java
	if player:
		player.player_died.connect(_on_player_died)
	else:
		print("Still can't find the player! Check the name in the Scene Tree.")
```
Now with all that put together, this was my "game over" screen ![](../screenshots/game-over.png).

## Day 19 - 4/8/26

[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
