---
title: Studylog - Making a Game Engine
date: 2025-02-21 04:00:00 +/-TTTT
categories: [Studylog, C++, Game Dev]
tags: [cpp, game dev, learning]     # TAG names should always be lowercase
description: A new studylog discussing the things I'm learning at the moment and a brief summary of the game engine I'm working on.
toc: true
comments: false
media_subpath: /assets/img/
---

So this post may come off as more of a "dev log" than a study log, but I refer to it as one for a few reasons. Namely, these posts are mainly going to be centered around what I'm learning at the moment. Currently, I'm studying for the [Network+ exam](https://www.comptia.org/certifications/network) scheduled for later this year while also diving deep into C++ and game development as a hobby.

I have been doing game dev on and off as a hobby for about a year now and have tried almost all the major game engines out there. That list includes full-fledged game engines like [Unreal Engine](https://www.unrealengine.com/), [Unity](https://unity.com/), and [Godot](https://godotengine.org/), as well as barebones frameworks like MonoGame and [Macroquad](https://macroquad.rs/). After exploring the different engines and ways to make games, I have finally settled on a project that I can see myself continuing as a hobby for the foreseeable future.

Now, one of the things many people say is that writing your own engine is the worst way to learn game development—and to learn C++ on top of that! But here's the thing: I am studying to work in cybersecurity and don't really plan on making a career out of making games. This is purely a passion project that may teach me some useful skills along the way.

But enough about me—let's look at the engine.

## C++
While spending time in different game engines, I got crash courses in a few of the major languages used in game programming. My programming language learning arc basically went like this:  
`C -> Python -> C# -> C++ -> Rust -> C++`

So, in my opinion, I definitely prefer the lower-level systems-programming languages. I fell in love with Rust, and learning Rust actually filled in the gaps in my understanding about memory I had from learning C (which was the first language I learned). I still really like Rust and hope that someday it is more widely used. However, I am already taking on a pretty tough learning task, and I don't think Rust lends itself to the pace of development I am currently at (which is learning by making a lot of different prototypes and implementations).

So I decided to bite the bullet and just learn enough C++ to get me going with the language, and from there learn the advanced stuff. I can say that I am very happy with my choice. Obviously, this means that C++ will become my main programming language going forward.

## SDL3
I am building the engine on top of the newly updated [SDL3 framework](https://www.libsdl.org/). The choice of framework is an interesting one. At the end of the day, I just don't like learning how to use an editor to make games—I wanted something much less bulky and more flexible. My interests align much more with system design than game design.

I chose SDL3 in particular because it is low-level enough for me to build most of the systems myself, yet it still provides a lot of convenient features that abstract away some of the less fun parts of engine design. _I'm looking at you, [OpenGL](https://www.opengl.org/) and [Vulkan](https://www.khronos.org/vulkan/)._ I will eventually look into OpenGL and Vulkan, but for now I just want to practice designing larger software and an engine of my own.

## Engine Planned Features
I am not going to plan a whole bunch of features and give myself an overwhelming amount of work to consider. So I'm going to start with some core systems and then see where I want to go from there. This is going to be a very opinionated engine and will focus on providing the features I think will be useful exactly the way I want them. I will eventually use the engine for some of my personal game projects—or even games I make for my kids—and as such, the type of game the engine will be best suited for will likely end up being quite specific.

**Currently Planned Features:**  
- **Game Loop:** The core game loop is the first thing I plan to implement. I am going to release a blog post about my considerations going into this design soon.  
- **State System:** I am still researching different methods of handling game states but plan to have this built into the engine like the game loop.

## Conclusion
This post marks the start of my journey into building a custom game engine from the ground up. In my next article, I'll dive into the technical details behind designing a robust game loop—exploring the options, trade-offs, and decisions that will form the heart of my engine. Stay tuned!

