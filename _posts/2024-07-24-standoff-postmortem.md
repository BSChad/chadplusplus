---
layout: post
title:  "Postmortem: Standoff!"
date:   2024-07-24 13:10:00 -0500
categories: blog postmortem
banner: assets/resources/posts/standoff/StandoffFire.gif
---

Standoff! is my first foray into the world of [Tiny Mass Games](http://www.tinymassgames). It is a card game about deceit and limited information. Attack the players to your left or right while trying to co-ordinate with others to become the last person standing. Part of my concession, was that I was actually too busy to put a lot of time into this, so I was going to be doing this pretty much on my phone. (Wait, what? Yep! [On my phone.]({{site.baseurl}}{% post_url 2023-10-24-i-made-a-game-on-my-phone %}))

[You can play the game on itch.](https://binarysolo.itch.io/standoff)

This was also my first adventure in using Godot, an open source engine that some people compare to Unity. It is similar in that there's an object hierarchy and a Decorator, Composition-ish pattern. It's also, available on the Google Play Store. So with two and a half months and a phone, Standoff! was born.

## What Did I Do On My Phone
Pretty much everything! I say pretty much because the only parts I didn't do were things that just weren't possible via phone.

* I did all of the UI art via Pixel Studio Pro.
* Particles and lighting directly in-editor in Godot!
  * (I actually like how this fire came out!)
    
    ![Chunky spherical fire particles float up like little flames in a low-poly campfire.]({{ "/assets/resources/posts/standoff/FireParticles.gif" | relative_url }})
* I wrote all the code in GDScript. That includes:
  * A card-based, ability system.
  * Game logic.
  * Unique AIs per character.
  * Menus and UI!
  * Saving player data.
  * Controlling character animations.

## What I Did On a Computer
Well, turns out the FMOD GDExtension didn't work out because... Android doesn't support extensions in 4.0. (Support was added in 4.2 but, due to a bug, the FMOD extension doesn't load because the engine can't load libraries that depend on other libraries from internal memory. This was fixed in 4.3!) Unfortunately, and fortunately, I had already gotten cool dynamic music from [Garret Rose](http://www.garrettrose.com), so I ended up doing all audio related work on a laptop. This was a little tedious because I had to develop new features and merge them into an audio branch that constantly had conflicts. If I had more time, I could have just done an interface to cover this up and make it mergeable.

*Another issue:* You can't import 3D models on Android! The gltf importer didn't work as of 4.0, so all models and animations had to be imported on a laptop. The gltf importer is, I believe, an executable, so it can't run on Android. I added them to the project on my laptop and committed it. After the initial import, however, you can set them up and mess with the models via mobile. It's just the initial import that isn't mobile friendly. You can animate, tweak materials, and everything else.

*Lastly,* I generated all my builds on a computer. (Godot calls this Exporting.) The Android editor doesn't have the capability to run the Export commands. That doesn't sound unreasonable, as generating binaries requires quite a bit of platform-specific code. Save for mobile, it seems best to actually export from the desired platform.

![The characters do the whole Good, Bad, and the Ugly close-up eye shot thing.]({{ "/assets/resources/posts/standoff/CinematicIntro.gif" | relative_url }}){:class="centered"}

## What I Learned
1. ### How to use the Godot editor!
Coming into this I had literally zero knowledge of Godot. To do this on my phone, I ended up having to use GDScript. GDScript is a lot like python. I had already messed around with python for our build system at BioWare, so it wasn't too hard to pick up. I found the documentation to be pretty fantastic. Everything I did was pretty much the bare bones version, so I never ran into something that didn't have a tutorial available. Whether it was the Godot docs themselves (which are also an open source, maintained product) or a Youtube video tutorial, the info I needed I could always find. The simplest takeaways: There are lots of Node types that do what you want and whitespace matters.

2. ### How to use Mixamo for animations.
I used basic Synty models to give characters an on-screen presence. To animate them, I dug into the world of Mixamo to animate humanoids. At Full Sail they taught us about animation and I did mess around with Maya. But that knowledge level is cursory at best. For Mixamo, they make it super easy to find animations, check them with your models, and download them for use in your project. Unfortunately, Godot isn't great with fbx models. Everything had to be changed into a gltf or glb, the open source format. Luckily, I was able to figure out a pipeline to get models and animations implemented by doing a one-time import with certain args using FBXtoGLTF. I've been doing so much 2D lately, it was a much needed refresher.

## What Worked
1. ### Prototype early.
I did a really quick paper prototype at GDC using a deck of cards and immediately knew the basic idea could work. Having the deck of cards be the most basic form of gameplay gave me a huge leg up on design work. I had the numbers, the four types of cards, and an easy way to play with it and deal it out even when it was just me. Luckily, this concept translated quickly to digital as well. The base gameplay was done early and then all of the learning was figuring out how to make it work visually.

2. ### Simple Idea
The game didn't require a plethora of features in order to get working. Deal cards. Play cards. Track health. That's all you really need in this game. I could have let it creep in scope. I did slightly. But I could have went networked. (I actually spent a day seeing if it was easy enough and then decided not to do it.) I could have shown players an entire hand of cards instead of forcing them to do one at a time. I'm sure I could have made much crazier cards. But I spent some time doing polish instead.

## What Could Be Better
1. ### Legibility!
    I used UI to do a lot of the card and button work, but that bit me a little bit when I wanted to implement animations and effects to make the game clearer to understand. I ran out of time for multiple reasons, but in the end I just have cards flying to the left or right of the screen when it would have been much clearer to create a 3D instance that flies to the actual player.

    ![Player chooses whether cards are given to the player on the left or right.]({{ "/assets/resources/posts/standoff/DealCards.gif" | relative_url }}){:class="centered"}

    I was also stubborn and stuck on this over the shoulder view, so getting the camera angles good for all players took a lot of time. Time that would have been better used if I had just done a top down view to start and been willing to show the flow of the cards more easily that way. I'm happy with the cinematic quality it has, but it was slightly at the cost of clarity.

2. ### Stick To a Theme
    This one was just a mismatch between what I had in my head and what I had on my computer. When I started developing the idea I was intent on a wacky mashup of wizards, knights, guns, and others. I drew all of the card art on my phone during the intermission of Disney on Ice. I avoided guns because I thought of swords and shields when I made the deck of cards prototype.
    
    ![Players use cards to attack each other, although animations are sync'd up to the UI, it's still cowboys using cards with goofy swords on them.]({{ "/assets/resources/posts/standoff/CowboysUsingSwords.gif" | relative_url }}){:class="centered"}

    The first pack I had on my machine was an old Synty Western pack. Then I got a fun idea to use the 'The Good, The Bad, and the Ugly' shots of the eyes to start each game to sell that distrust element. From there, I felt like I really went full on Serious Western with the vibe while UI has this sketchy fun feel to it. I should have either added more over-the-top models, injected some humor, or just re-did the cards to be a gunslingin' theme instead.

3. ### The Code!
This one is less an issue in architecture and more of a learning curve. The game is kind of buggy in some respects, and that can mostly be attributed to learning a new language with different paradigms on an engine that's just starting to mature. No problem admitting there were some hacks or even just lessons learned down the road that there wasn't time to go back and fix.

## In Conclusion
It was an interesting experience making the game mostly via mobile. I think for a game developed in stolen moments it came out relatively well. Definitely leaned more game jam than small project, but such was the constraints of the time and tools.

[Again, you can play the game on itch.](https://binarysolo.itch.io/standoff)

Unless you follow the [Binary Solo itch page](https://binarysolo.itch.io/) or subscribe to the [Tiny Mass Games newsletter](http://subscribepage.io/uwNffE), you might be wondering if I would do it again. Well, I released another game called Deeper which I started on my computer and ended up putting a lot more work into via mobile when my house was flooded. So yes, I did do it again and I shall continue to do it. I'm sure it's unhealthy to think of this idle time as wasted, but it feels damn good when you are able to create and test a feature on your phone. Grab Godot on the Play Store and give it a try.
