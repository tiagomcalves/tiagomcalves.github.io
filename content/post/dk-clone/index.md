---
date: '2026-11-05T17:55:12Z'
draft: false
portfolio: true
portfolioWeight: 1
title: 'DK Clone'
description: 2D arcade platformer written in Java
tags: ["java", "game", "university"]
cover:
  image: "dk-clone-thumbnail-small.png"
  # can also paste direct link from external site
  # ex. https://i.ibb.co/K0HVPBd/paper-mod-profilemode.png
  alt: "dk-clone-thumbnail"
  caption: "The hero of the game, JumpMan, facing two DKs"
  relative: false # To use relative path for cover image, used in hugo Page-bundles
---

## Overview

The final project co-authored by me and a classmate as part of our university course of Object-Oriented Programming.
It is a 2D Arcade Platformer game written in Java, with a focus on OOP concepts, flexible implementation and reusability.


## The basics of the gameplay

The player controls our hero, JumpMan, whom they have to guide through each level and save the princess waiting on the final level.  
To accomplish that, you need to avoid DKs constant banana attacks and level traps, and reach the door DK keeps guarding.  
You can defeat DK by moving against it, which qualifies as an attack.
Each level has pickups, one of which is the Key that opens the door to the next level.  
Some pickups give you advantages such as higher damage output or healing, while others can hurt you.  
You start with 3 lives, and you restart on the current level upon dying. Depleting all lives results in a game over.


## Technical stuff

### The fundamentals
The project fundamental requirements were the usage of Java OOP concepts taught during the course, such as
- Heritage, Abstract classes, Interface implementations, Singleton classes, Factory methods, adequate usage of data structures (such as Lists, Arrays, Hashsets, Hashmaps, etc), file writing and reading, exception throwing and handling, lambda expressions, anonymous classes, Comparables, and a few more. 

We were instructed to use the provided Graphical Interface (ImageGUI class and ImageTile interface) that handled the tile drawing and a base for the GameEngine class.
The GameEngine class would be the central class of the architecture, responsible for initializing and updating the entities, while keeping tabs with 
the Tile Interface which provided a Ticking mechanism which our Engine class would be aware of and handle game events accordingly.

According to the project assignment, the game elements had to take maximum advantage of an heritage and polymorphism hierarchy, using more than one level of heritage if necessary. On the other hand, we had to take into account how could we model the game elements using Interfaces.

Later on this article will be the class diagram showing how we modeled the classes.

### The level architecture
Each level was built off of Image Tiles, which are identified by a uniquely chosen char.
We could then write each level into a text file using single characters. 
Upon loading each level, we could read and correspond each char to a Factory method to retrieve the appropriate Tile Object.

Depending on the tile type, the tile object instance would be either stored once in memory and referenced by various 2D Points of the Tile Grid.
For example, there is no point in storing and entire row of Wall Tile objects if they all behave the same, which is blocking any entity from moving further against it.
Any static tile that belonged to the environment, we would instanciate it once and, every Grid Point2D that was identified with either "Wall", "Ladder" or other of said type, would just reference that one object.
That was one of our simple ideas to save memory.

At the top of each level text file, the first line marked with '#' identifies the level exit (0 or 1) and what the next level text file is.
Every level would be loaded into memory on game launch, so there would be no file IO between level transitions.  
```txt
#0;room1.txt
0 G
WWWWWWWSWW
       S M
tWSWWWWWWW
  S     K
WWWWSWWWWW
    S  s  
WWWWWSWWWW
     S H
WWWWWWWWWW
```  
{{<sup>}}(the text file of the first level, "room0.txt". First line points to the next level "room1.txt"){{</sup>}}

### Course challenges
The codebase had to be modular enough and leverage class relationships, avoid code duplication and have enough flexibility for last-minute implementations.
This last point was quite important since each week we could be prompted to add a new gameplay element in a small window of time.
And we were prompted as such.
In a small time frame, my teammate and I were instructed, in different points in time, to implement specific ideas:
- A ticking time bomb, ala Bomberman, that the player could place anywhere on the map, and it would explode destroying objects on a 1 tile radius;
- A fireball projectile that would go upwards;
- An enemy Bat that would randomly go left or right, would climb down a ladder every time it encountered one and, if it touched/was touched by JumpMan, dealt damage and disappeared;
- A steak item, which we reskinned to a pill, that would heal the player but had a small expiration period and would go bad, and took health instead of giving if so;
- JumpMan 3 lives system (explained in "The basics of gameplay");
- A "3 types of failure" mechanism on level file reading.


## The "art"
Most of the tile image files provided to every class student by the professors came from the game [Pixel Dungeon](http://pixeldungeon.watabou.ru/) and can be found in [pixeldungeon.wikia.com](http://pixeldungeon.wikia.com/).

At the beginning of the development we quickly found out that _GIFs_ would retain their animation, so we quickly tried to spice it up a bit by taking the provided "Banana.png" still image into [GIMP](https://www.gimp.org/) and turning it into a rotating "banana.gif" by hand.
The second change we made was duplicating each character to make a "facing left" and "facing right" variant and change the code accordingly to the last movement direction.
Only JumpMan, DK and the Bat take advantage of such work but it looked much better anyway. We also sped up the Bat GIF frame rate so it would flap its wings faster.

When we added a star powerup ala Super Mario, we knew it would have to reflect on JumpMan's appearance. So a yellow fade in/out was quickly put in place.

More at the end of the project deadline, I noticed that the items were a bit stale. The healing potion was changed to a RGB-esque colour change and the Key would float up and down slightly.

We are no pixel artists (not even artists for that matter) but these slight changes made our little game much more appealing.


## Retrospective
Looking back at it, it was pretty fun to see the game take shape, the code pieces coming together and, considering how busy a university course can become, I figure my teammate and I were able to conquer the course objectives, which was writing a codebase that could accommodate unknown future elements.
This means that anyone could get a new idea for the game and implement it pretty quickly.

I remember trying this little game on my weak laptop and also trying it on an old university PC was a bit sluggish on the frame rate, although it did not impact the game ticking logic and, since it was time constrained course project with emphasis on Object-Oriented programming (literally the course title) with a delivery date, it was obviously not a priority.

Today I am almost two years older in my programming journey since this project was delivered (December 15th, 2024).
New concepts in OOP were learned but so were new paradigms and problem-solving concepts! 
Functional programming languages, Concurrent and distributed code, High-performance Computing, and so on! 
So in a way, this codebase can also stand as a testament of my growth as a developer.  

In the current days, I am looking into more data-oriented programming paradigm concepts, which are quite important for performance-critical problems, such as graphics and game-engines.


## Source code

[GitHub](https://github.com/tiagomcalves/OOP-final-2024)


## Media
|{{< figure
  class="fig-w-40"
  src="images/dk-clone-room0.png"
  alt="level 1"
  caption="First level (room 0), after grabbing the sword (note the notifications label on top)">}}|{{< figure
  class="fig-w-40"
  src="images/dk-clone-lvl3.png"
  alt="level 3"
  caption="Level 3 (room 2)">}}|
|:-----------:|:-----------:|
|{{<figure
  class="fig-w-40"
  src="images/dk-clone-total-chaos.png"
  alt="level 3"
  caption="Extra level (room 777), the pill has gone bad">}}|{{< figure
  src="images/dk-clone-victory-scoreboard.png"
  alt="victory scoreboard"
  caption="Final scoreboard">}}|

---
Some gameplay  
{{< video src="dk-clone-gameplay.webm" width="60%" >}}

{{< figure
  src="images/Banana.gif"
  alt="banana spin"
  caption="An absolute must-share">}}
