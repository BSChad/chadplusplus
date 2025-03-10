---
layout: post
title:  "Postmortem: Deeper"
date:   2025-03-06 09:22:03 -0500
categories: blog postmortem
---

Deeper is my second game for [Tiny Mass Games](http://www.tinymassgames.com) as well as my second project in Godot and my second time using my phone to make a game. It is an action-esque, turn-based, extraction RPG. It is a GameBoy aesthetic party-based battle system with time bars instead of mana.

### Features

* An Extraction RPG that fits the GameBoy aesthetic and control limitations.
  * Control up to four characters at the same time, each with six different moves, using only left / right and A / B!
  * Unlock new color palettes to spice up later runs.

* Fight 9 Common Enemies and 3 Unique Bosses, each with their own unique mechanics.

* Collect 50+ pieces of procedurally generated equipment and outfit your party.
  * Be careful! If characters die, their bodies and, more importantly, their loot are lost to the dungeon.
  * (Collect unique equipment that can only be found once.)

[You can play the game on itch.](https://binarysolo.itch.io/deeper)

I originally intended for this game to be a smaller piece of a larger thing, but ended up not completing the larger thing. 

## What Did I Do On My Phone

I started this game on my computer with a plan to do certain features or types of work on my phone: Tasks without audio, easy systems that didn't require too much debugging, or better yet, creating Resources and doing basic data entry. That got thrown for a giant loop when my house was flooded and I lost said computer. (And the walls, stairs, washing machine, water heater, files, and more. Big things to lose, but away they went!)

![A basement flooded with 18 inches of standing, brown water.](/assets/resources/posts/deeper/flood.jpg) 

* This game was entirely pixel art, so again I was able to use Pixel Studio Pro to create all of the graphics. This includes:
  * 6 Hero Designs (Simple back of head only)
  * 6 Enemy Designs, 3 of which having 3 color variations.
  * VFX
  * Equipment Icons
  * UI
  * Logos

* Created all equipment resources, both code and the data files.

* Created a virtual GameBoy wrapper that is only available on an Android device. On Android the game is forced into portrait and the controls all sit just below the fold, so to speak, on a regular windowed build.


## What I Did On a Computer

I knew going into this one that I would have to make builds on desktop. I was going to aschew FMOD for this one since I knew the plugin didn't load on an Android device. My plan this time was to do all of the system code on my desktop and then use my phone to just enter gobs and gobs of data.

Luckily I had a laptop I could do builds on, but everything else was via phone.


## What I Learned

Script templates! 

## What Worked

Set myself up for success by making things that could be pure data without art. Equipment, for example, only had an icon for it's type. Moves were simple. 

Re-using the status effect system to make unique enemies. (Vampire is a status effect!)

## What Could Be Better

Needed even more content! The classes weren't fully baked.

## In Conclusion

Water sucks.

Again, you can play the game on itch.

Unless you follow the Binary Solo itch page or subscribe to the Tiny Mass Games newsletter, you might be wondering if I would do it again. Well, I released another game called Deeper which I started on my computer and ended up putting a lot more work into via mobile when my house was flooded. So yes, I did do it again and I shall continue to do it. I'm sure it's unhealthy to think of this idle time as wasted, but it feels damn good when you are able to create and test a feature on your phone. Grab Godot on the Play Store and give it a try.