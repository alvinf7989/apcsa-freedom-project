# Entry 4
##### 3/10/26

We are back once again with another blog entry and I have three more days that I've logged in about my tool Godot. Now, this is just a normal entry which means there's no explanation about a break plan, but it's possible that I might say something special in the next entry. But without further ado, let us go through these days on Godot.

## Day 10 - 3/2/26
I start off strong with Day 10, where I finished settign up my plan and organizing dates. I looked at my plan and it said I need to make my ship on the top move side to side automatically, so I used my "How to Google" skill and looked up, "i want to make my ship on 2d godot move side to side automatically". With Google being new and AI existing, whenever I look up an answer like this, it gives me an AI Overview and while it is useful, it doesn't help me find any sources to put in my entry. So what I had to do was attach a code that exports the initial speed and width of the top ship in the top ship script.
```java
@export var speed: float = 200.0
@export var width: float = 300.0
var time: float = 0.0
```
And then I put in the `_process(delta)` function where inside, is `time += delta` followed by code that moves the top ship side to side.
```java
func _process(delta):
	time += delta
	// Oscillates side-to-side based on a sine wave
	position.x += sin(time * speed * 0.01) * speed * delta
```
Putting this altogether in my top ship script, the ship when running my code was successfully moving side to side, but the ship was mostly moving to the right while also going side to side. So, I had to tinker with the `Vector()` value at the global position by changing the x and y values so the position is fully centered.
```java
global_position = Vector2(350, 100)
```
Running the code again, the side to side movement isn't spread out enough, so I tinkered with the decimal from `sin(time * speed * 0.01)` enough to find out that if you increase the decimal the side to side movement is faster, so I changed the amount to `0.005`.
```java
position.x += sin(time * speed * 0.005) * speed * delta
```
Position x is the only thing that's being affected by the top ship. Now I must look on to my plan on the next day.

## Day 11 - 3/9/26
For this day, I looked back at my plan and realized that my next step is to add the pellets when to shoot from the ship. It took me a few Google searches, but when I finally looked at the final code it told me to create a separate pellet scene with a `colorRect` node and in that pellet script I put in the code that Google gave me
```java
extends Area2D

var speed = 600 // Initializes speed

func _physics_process(delta):
	// moves up
	position.y -= speed * delta
```
To explain, this pellet code intializes the speed of it which is okay with me, and also creates the function that allows the pellet to move up with `position.y`. But before I did that, I had to add the `shoot()` function in my player script, so the pellet knows where to be shot from.
```java
func shoot():
	var p = pellet_scene.instantiate()
	get_parent().add_child(p)
	p.global_position = global_position
```
This is to ensure that the pellets aren't at the top right, I set up the global position of the pellets to be aligned with the bottom ship. To actally have this function work I used a condition called `if Input.is_action_just_pressed("ui_accept"):`, where `ui_accept` is the same as pressing `enter` or `spacebar`. Now to have these scenes connected I put on the top
```java
@export var pellet_scene: PackedScene = preload("res://pellet.tscn")
```
to export the pellet scene for the pellets to work. Finally, after running the code, the pellets were accurately shooting.

## Day 12 - 3/10/26
So, the pellets were working, but they were too big and not centered right, so all the changes that I did were all from the Inspector side of the color Rectangle. So, this is the day after Day 11 because the blog entry was due the next Monday, so I have to put in one more day. Anyways, I explored through the Inspector tab of some of the nodes in the Pellet scene and when I did, I found the Transform node of the `colorRect` node. ![](../screenshots/crees.png) Now since the size was too big, I tried to decrease the x and y values from 40 to 10 px. I also changed the position a little t be centered with the ship that's at the bottom shooting pellets. That is pretty much it for all the days that I've gone through with this entry, and I gotta say, I've acquired some new skills, that I'd like to talk about.

## EDP
But before I get to the skills, I must talk about my Engineering Design Process. Now here's what's interesting, I created a [plan](../prep/plan.md) a few weeks ago and listed off what I would be in the MVP and beyond MVP and set up all the dates for when I should do the subtasks by. So I guess this means I'm back in the **Planning** part of the process. This means that it's possible that I have also gone to the **Creating** part of the Engineering Design Process for my Godot project.

## Skills
**How To Google: UPDATE** So, google has been giving me this thing called AI Overview where whatever I type, the AI will give answers using sources found from Google to generate a full summary out of them. While this gives me an advantage with solving the problems and issues with Godot, it doesn't help me with adding sources to my source list below.

**How To Learn** Day 12 was when I was looking for the Inspector panels to see what I can do to change the characteristics of my yellow pellet with no googling whatsoever. I was able to find the Transform node on the Color rect node in my Pellet scene and from there, I changed the position and size of the pellets. This is a good example of "Learning on my Own" because I didn't use any resources and with how many times I 've looked in the Inspector panel in Godot, I was able to look for the Transform panels myself.

**Organization** Organization is anothe skill that comes form the [plan preparation](../prep/plan.md) that I've set up along with the deadlines. I accurately followed the steps based on the deadlines that I created for my plan preparation and with that time I was able to organize my tasks and subtasks for MVP and Beyond MVP for my Godot Project.

## Sources
[Blog Entry 1](entry01.md)

[Blog Entry 2](entry02.md)

[Blog Entry 3](entry03.md)

[Screenshots](../screenshots)

[My MVP Plan](../prep/plan.md)


[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
