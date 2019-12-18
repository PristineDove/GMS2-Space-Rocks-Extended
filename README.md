# Space Rocks Extended

## Introduction
This is a follow up from [GMS2 First Look](https://github.com/maubanel/GMS2-First_Look) and is meant as a follow up/companion to **Space Rocks - GML Tutorial** which is a freely available tutorial at [YoYo Games Marketplace](https://marketplace.yoyogames.com/assets/7423/space-rocks-gml).  This beginner tutorial teaches you how to make a simplified version of Asteroids.  It uses GameMaker's GML programming language.

The extended tutorial is a follow up to creating a structure where the developer can create escalation in diificulty. It is meant as a starting point and not a finished game! 

In this tutorial:

* Import assets from other projects
* Add variables and comments to all scripts without changing functionality
* Resize ship 
* Add flame behind ship when accelerating
* Add ship explosion animation
* Change player death and end game timing
* Add friction and maximum speed
* Use timeline for spawning rocks and add custom spawning script
* Trigger waves either by time or by score

## Controls
* Left and Right arrow rotate the ship
* Up arrow accelerates
* Space bar shoots
* Enter starts game

## Game Design Concept
The infrastructure for the  following game design concept is introduced in this tutorial.


| Game Design Concept | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Escalation          | A positive feedback loop in which the game gets more difficult the closer the player gets to the goal.  This is often combined with risk/reward scenarios which allows for faster completion but with greater risk to the player. Escalation allows the designer to slow down better players by escalating the difficulty faster, slowing the  player's progression through the level.  This can be achieved through various means but common ones are speed (Pac Man ghosts speed up as level progresses), increase in number of enemies or objects you need to deal with (tetris has more falling shapes) or aggressiveness of the attack.  It is good to model in breaks so that there are peaks and rest periods in the level driving the player to completion.      |

## Programming Concepts
The following programming concepts are raised in FirstLook.yyp.


motion_add(direction, speed);
instance_destroy()
instance_create_layer()
irandom_range(start, end)
chosse()
draw_text_transformed_color()
instance_exists()
clamp()


@"string"

exit;
switch statements

alarm[]
score
lives
sprite_index
