# Entry 1
##### 11/7/25

Welcome to my firstblog entry of the final Freedom Project of high school. It has been 3 years and this year is when the Freedom Projects get interesting. We were given the option to choose any tool in APCSA and we decide what we will be trying to make with that tool. Let's get to talking about my tool.

## My Tool
So, the tool that I chose this time wasn't Kaboom, but instead was this advanced programming application called Godot (guh-dow). In this tool, I will try to make a unique 2d shooter game, but I haven't gotten to the part that makes it unique just yet. Of course every tool comes with a learning log which is what I used in this one. Like the Learning log from Sep10, I took 2 days to study on what I did to tinker with this tool on the [APCSA Learning Log](../tool/learning-log.md). When looking at the months between those two days, they are very far apart, but for a good reason. Ever since, September ended, there was no due date assigned for the next learning log, and most of the Mondays on October were days off. But hey, let's get started on talking about Godot.

### Day 1
So to start tinkering with my tool, I needed to understand the basics of Godot. That is why I watched a [Godot Crash Course](https://www.youtube.com/watch?v=S8lMTwSRoRg) for 13 minutes for this day. What I learned to do during this day was how to create a button by clicking the plus icon on the top left and searching up button.

There was a place to put in text on the right side. However, when I put text there, it seemed to not show up on the button. In the end it turns out, it's only visible if you zoom in enough.
### Day 2
We are in next month, and the next thing I do here includes code. So, a way to try and actually code the buttons to have a function is to go to where it says script. I watched a few minutes of that same Godot Crash Course and I made the play button change the scene to a different one.
```js
func _on_play_pressed() -> void:
	get_tree().change_scene_to_file("res://shooter_area.tscn")
```
The function on the first line is to be run once the play button that I created is pressed. The second line shows how once that button is pressed the main scene now switches to the scene file shown inside the `change_scene_to_file()` parenthesis.

This wasn't all that I just did on this day. When making the new scene, I named it "shooter area" because that's when the shooting game starts. Inside the shooting area, I added another node by clicking the plus icon to search up label, just to test if the button will actually go to the directed scene. This label node also includes a text box. I had the label say "this is the label".

### Day 3
Psyche! You thought I only used 2 days to tinker my tool. I actually used the recent day to add a background to my shooter game. This background would show up after the user clicks on the play button. A way that I made the background is by going to Photoshop and creating one. It's the same technique I used for my last Freedom Project. I dragged my exported background into Godot, removed the label, and added a Parallax Background & layer as the new nodes. When I first did this, it wasn't working because the background was still. So, I changed the function from `extends 2DSprite` to `extends ParallaxBackground`, so it properly works. Here's the code for how the scrolling works
```js
extends ParallaxBackground

var scrolling_speed = 100

func _process(delta):
	scroll_offset.y += scrolling_speed * delta
```
The scrolling speed is set to 100 to maintain a well-balanced speed of how fast the background should move. The inside of the `func _process(delta)` is where the scrolling code runs. The `scroll_offset` could be x to move horizontally or y to move vertically. I chose to move vertically. To get the background to move downwards, I used the `-=` operator with multiplying the scrolling speed. Now, I wasn't done yet because I set the mirroring of the y value to equal where the background ended from the bottom. Godot has those measuring tools to see what numbers to put in. Also `+=` with y moves upwards. But yeah, that is all of the days that I have used to tinker with my tool.
## EDP
Since this is the first blog entry, I would say that I am on the defining part of the Godot Freddom Project in the Engineering Design Process. I think you could also say that I am also in the Research part of the EDP by looking up a crash course for Godot on Youtube and following the steps provided by that video. Everytime I talk about the EDP I'm on in the 1st entries of these Freedom Project, I always feel like I'm in the Researching & Defining part of the process.
## Skills
* **Embracing Failure**: This skill is something that I've acquired on the 3rd day, when I noticed my background wasn't moving at all. I made a mistake and forghot to put any mirroring values and have whatevers next to `extends` be `ParallaxBackground`.

* **Debugging**: In a way, while I was embracing failure, I was also accomplishing the skill of debugging by testing code after putting it in the script, and then, I found out what was wrong and changed the first line of code for the background a little bit, so the background could appear accurately.

## Sources
[Godot Crash Course](https://www.youtube.com/watch?v=S8lMTwSRoRg)

[My Learning Log](../tool/learning-log.md)

[Next](entry02.md)

[Home](../README.md)
