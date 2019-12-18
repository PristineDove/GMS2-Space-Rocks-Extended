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
The following programming concepts are raised in GMS2-ExtendingSpaceRocks.yyp.

| Programming Concept                                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Example                                                                                                                                                                                                                                             |
|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| switch statement                                    | It is a type of control statement that controls flow and acts like an if - else if - else statement.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | switch (age) <br>{    <br>&#160;&#160;&#160;case (18): <br>&#160;&#160;&#160;draw_text(x,&#160;y,&#160;"adult");<br>&#160;&#160;&#160;break;<br><br><br>&#160;&#160;&#160;case(12):<br>&#160;&#160;&#160;draw_text(x,&#160;y,&#160;"twelve&#160;years&#160;old");<br>&#160;&#160;&#160;break;<br><br>&#160;&#160;&#160;case(5):<br>&#160;&#160;&#160;draw_text(x,&#160;y,&#160;"5&#160;years&#160;old");<br>&#160;&#160;&#160;break;<br>} |
| dot accessing game objects<br>(`obj_game.p1_score`) | There are multiple ways of accessing other game objects variables (not local variables with var keyword).  All variables in GMS2 are considered public and are accessible by other objects in the game.  For example we have an enemy object called `obj_enemy`.  The player needs to know where the enemies position is on screen so it can access its `x` and `y` value by calling them inside the `obj_player` object with `obj_enemy.x` and `obj_enemy.y`. This only works if there is only a single instance of obj_enemy in the game.  If there are multiple instances of this object this way of accessing it is unreliable as ultimately will go through all instances and end up with the value from the final instance that was loaded in the level. | <br>in&#160;`obj_player step`&#160;event<br><sub><sup>`direction=point_direction(x,y,obj_enemy.x,obj_enemy.y);`</sup></sub>                                                                                                                                                         |
| @string                                             | To preserve formatting when drawing strings in gamemaker you can use the special @"strings" to preserve spacing and line breaks.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `draw_text(x, y, @"This will draw on line 1,`<br>`this is line 2`,<br>`this is the final line 3.");`                                                                                                                                                     |
| Force                                               |  F⃗ = ma⃗.  Force equals mass times acceleration.  In this example we will use a mass of 1 so we can skip it from the formula.  Our force F⃗ vector is kept in the built in `speed` and `direction` variables.  Acceleration is a user variable called `acceleration` that is found in `obj_player`.                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                     |
| Friction                                            | We simplify friction by just reducing the magnitude of the speed by a small amount (smaller than acceleration or it would not move) every frame.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                                                     |
| Velocity                                            |  V⃗ = V⃗ + a⃗. A new velocity is calculated by adding the acceleration to the existing velocity                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                     |



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
