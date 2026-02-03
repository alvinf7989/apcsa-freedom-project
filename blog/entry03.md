# Entry 3
##### 2/3/26

I am back once again with another blog entry about my Freedom project. In this entry, I will talk about what I accomplished so far as of my Winter Break plan and the three days I worked on my Godot Game Project. From adding small ships next to my main ship to making the top ship still, these are the days that I've worked on my Freedom Project of Senior Year.

## Day 7 - 12/30/25
This day was known as the last tinkering day of 2025 and I decided to do some progress like I said I would in my last entry. What I wanted to do was create two more sprites that move next to the main sprite. This wasn't my first idea because I wanted to initially duplicate that pink ship sprite, but the problem was when putting in values in the `Vector()` method, it wasn't working. So, I looked up how to duplicate my sprite on Google and it turns out I didn't need to change anything in the script. I just added two sprite 2d nodes as children of the 2d Character Body node. To add the ship sprites next to each other I went to the texture section on the right side of Godot's interface to look for the small ship sprite ![](../screenshots/position-values.png) Now you see what's circled right here and it's the position section. I tinkered with this and put 30 and -30px on both x-values to put the ships next to the main pink ship. When I ran this code, I notices the ships were upside down, so I changed the rotation to 180. The y-value was only adjusted to match the y-value of the main ship. 

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
