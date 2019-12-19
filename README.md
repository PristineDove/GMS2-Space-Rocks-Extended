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
The following programming concepts are raised in GMS2-ExtendingSpaceRocks.yyp. Here are the new programming concepts that are introduced in this second walk through.

| Programming Concept                                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Example                                                                                                                                                                                                                                             |
|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| switch statement                                    | It is a type of control statement that controls flow and acts like an if - else if - else statement.  The variable in parenthesis after the `switch` statement is used to control the flow of the statement.  If that variable matches a `case` then the code after it is run until it hits a `break;`.  Be careful, if the break is omited the next case will apply as well and can be the cause of hard to find bugs.A `default` case at the end can be added in the event that all other cases are false and acts as a default (like the final `else` in an if statement).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | switch (age) <br>{    <br>&#160;&#160;&#160;case (18): <br>&#160;&#160;&#160;draw_text(x,&#160;y,&#160;"adult");<br>&#160;&#160;&#160;break;<br><br><br>&#160;&#160;&#160;case(12):<br>&#160;&#160;&#160;draw_text(x,&#160;y,&#160;"twelve&#160;years&#160;old");<br>&#160;&#160;&#160;break;<br><br>&#160;&#160;&#160;case(5):<br>&#160;&#160;&#160;draw_text(x,&#160;y,&#160;"5&#160;years&#160;old");<br>&#160;&#160;&#160;break;<br>} |
| dot accessing game objects<br>(`obj_game.p1_score`) | There are multiple ways of accessing other game objects variables (not local variables with var keyword).  All variables in GMS2 are considered public and are accessible by other objects in the game.  For example we have an enemy object called `obj_enemy`.  The player needs to know where the enemies position is on screen so it can access its `x` and `y` value by calling them inside the `obj_player` object with `obj_enemy.x` and `obj_enemy.y`. This only works if there is only a single instance of obj_enemy in the game.  If there are multiple instances of this object this way of accessing it is unreliable as ultimately will go through all instances and end up with the value from the final instance that was loaded in the level. | <br>in&#160;`obj_player step`&#160;event<br><sub><sup>`direction=point_direction(x,y,obj_enemy.x,obj_enemy.y);`</sup></sub>                                                                                                                                                         |
| @string                                             | To preserve formatting when drawing strings in gamemaker you can use the special @"strings" to preserve spacing and line breaks.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `draw_text(x, y, @"Line 1,`<br>`this is line 2`,<br>`this is the final line 3.");`                                                                                                                                                     |
| Force                                               |  F⃗ = ma⃗.  Force equals mass times acceleration.  In this example we will use a mass of 1 so we can skip it from the formula.  Our force F⃗ vector is kept in the built in `speed` and `direction` variables.  Acceleration is a user variable called `acceleration` that is found in `obj_player`.    | `acceleration=.05;`                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                     |
| Friction                                            | We simplify friction by just reducing the magnitude of the speed by a small amount (smaller than acceleration or it would not move) every frame.     | `speed=speed-ship_friction;`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                     |
| Velocity                                            |  V⃗ = V⃗ + a⃗. A new velocity is calculated by adding the acceleration to the existing velocity              | `motion_add(image_angle,acceleration);`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                     |


## GameMaker Resources

On the right hand side of the game editor you have a list of all resources that can be added to the game.
GameMaker Resources. Here are the new GameMaker resources that are introduced in this second walk through.

| GameMaker Resources | Description                                                                                                                                                                                                                                                                                                                                                 |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sounds              | GameMaker Studio 2 allows for `.wav` and `.mp3` files.  It is strongly recommended to use `.mp3` files for music or any long audio sequence due to its smaller size.                                                                                                                                                                                        |
| Scripts             | Scripts are away to simplify and shorten event based scripts (like step events in a game object).  This makes the code easier to maintain and can make it more reusable.  These scripts acts like functions in other programming languages and can take parameters and return values.                                                                       |
| Fonts               | This allows you to select a font that is already available on your computer to be added to the game. Please note that for the editor the font needs to be loaded in the computer already to show up.  So you need to make sure this font is installed on all computers that are working on the game.  A build of the game on its own will include the font. |

## Built in Object Variables

GameMaker objects all share common built in variables. Here are the ones that are important to this exercise. Here are the new Built-In Variables that are introduced in this second walk through.

| Built-In Object Variables | Description                                                                                                                                                                                                                                                                                                                              | Example                                |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| alarm[n]                  | There are 12 alarms that can be set on an individual game object (alarm[0] through alarm[11]). This runs a an alarm script as a future event in game steps.  An alarm that is not set (not active) is set to `-1`.  When triggering an alarm it is important to make sure it is only triggered once, especially if it is in a step event. | `if(alarm[0]<0)<br>   alarm[0]=room_speed*2;` |
| score                     | This is a real number global variable that is accessible from any object.  There is only a single score so in a multiplayer game, you will need to create another variable. The default value is `0`.                                                                                                                                    | `score=100;`                           |
| lives                     | This is a real number global variable that is accessible from any object.  There is only a single health variable so in a multiplayer game you will need to create another variable. The default value is `0`.                                                                                                                           | `lives=5;`                             |
| image_alpha               | This is a real number that determines how opaque the sprite will be rendered.  It defaults to `1` which is completely opaque.  `.5` would be 50% transparent and 50% opaque and `0` would be 100% transparent, effectively invisible.                                                                                                    | `image_alpha=.75;`                     |
| image_index               | This is an integer that refers to which frame of a sprite the game is displaying.  The first frame in a sprite is `image_index` of `0`. Each subsequent sprite goes up by 1.                                                                                                                                                             | `image_index=0;`                       |
| sprite_index              | This refers to which sprite the game object embeds.  For a player animation you might need to change sprites for different directions of movement.  You assign the name of the sprite that you use.                                                                                                                                      | `sprite_index=spr_player_right;`       |

GameMaker Variables:
alarm[n]
score
room_speed
lives
image_alpha
image_index
sprite_index
Algorythm
Game Controller

GameMaker Events
Alarm
Room Start
Collision
Outside Room
End Step

GameMaker Functions
draw_set_font(font);
audio_is_playing
audio_stop_sound
audio_play_sound
draw_text_transformed_colour
room_goto(room)
instance_create_layer(x, y, layer, object)
instance_exists()
keyboard_check_pressed
choose(arg0, art1…)
irandom_range
repeat
clamp
instance_destroy
motion_add(direction, speed)

User Created Function (supplied)
scr_spawn_asteroid



GamdMaker Constants
vk_space

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
