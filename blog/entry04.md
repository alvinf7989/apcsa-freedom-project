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


[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
