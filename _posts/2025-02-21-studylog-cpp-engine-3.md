---
title: Studylog - Implementing a Texture Manager and Component System
date: 2025-02-26 04:00:00 +/-TTTT
categories: [Studylog, C++, Game Dev]
tags: [cpp, gamedev, learning]     # TAG names should always be lowercase
description: An article following my attempt at creating a framework agnostic texture manager.
toc: true
comments: false
media_subpath: /assets/img/
---

## Introduction
In my [last article](link to article) I implemented a game loop in my custom C++ game engine. I also said at the end of that article that I was going to remove all the raylib specific code from the game loop. So far I have managed to exclude a lot of framework specific code and want to continue doing that as much as possible. However, I will need to decide on a framework because while I enjoy building systems myself I am fully aware of my skills and in some cases, the lack there of. One of the biggest cases is graphics programming. And one of the things frameworks remove (atleast at first) is the need for graphics programming.

> I might cover this in a future article but for those interested I'm currently considering the following options for the frameworks I build my engine on top of.
  - The Forge SDK
  - SDL3
  - MOAI SDK

In the process of writing this article I realized that to design a well thought out texture management system I would need to have my component system sorted outfirst. In this article I will be discussing how I designed and implemented my framework agnostic texture management system and the component system I ended up going with.

## Features
- **Currently Implementing:**
  - Component System (for player and enemies)
  - Texture Manager

- **Implemented:**
  - Game Loop: Variable and fixed time step loops to handle all the processes a game might need.

- **Planned:** *This list of features is in the order I plan to implement them so it is subject to change.*
  - Input System
  - Game State Machine
  - GUI

---

## Component System
### Component System Design Considerations
When deciding how to represent game objects in my engine I considered two options. The first was a traditional component system and the other was an Entity Component System (ECS) system.

> Before I tell you about the component system I envision lets see what Robert Nystrom has to say about the pattern:  
  *"For a large codebase, this complexity may be worth it for the decoupling and code reuse it enables, but take care to ensure you aren’t over-engineering a “solution” to a non-existent problem before applying this pattern."*

I ended up choosing to go with a more traditional component system. There were two big reasons I chose this over a ECS system. First off is the complexity, I used the [Bevy](link.com) ECS before and that was amazing but the reasons for that are Rust specific in my opinion. This is due to how Rust manages memory and concurrency, the main reason to use [bevy_ecs](link to bevy ecs crate) is the easy multithreading it facilitates. Now that is all good an well but I am not using Rust and I definetly don't know enough about ECS or C++ to implement a system that could rival the one Bevy uses. 

The second reason I chose a component system is because there is a really nice chapter on the [Component Pattern](wikipedia link) in Robert Nystroms book, Game Programming Patterns. Like I have said in previous articles one of the reasons I'm working on this engine is so I can learn OOP programming and how to implement different patterns. 

![hand drawn picture](comp_dia.png)

As the above picture hopefully demonstrates I plan to represent entities - or GameActors in my case - as a class that acts as a container for component classes. Such as the input, texture and position components. I chose `GameActors` as the name to represent my entities purely because I like how it sounds. I don't really plan on making the distinction between GameActors and GameObjects because I think components can do the same thing without the extra complexity/boilerplate.

### Implementing the Component System


---

## Texture Manager
### Texture Manager Design Considerations
### Implementing the Texture Management System














## Sources and References:
Below are the resources I used while researching this article.

### Books:
- Game Programming Patterns - Robert Nystrom
- Programming Principles and Practice Using C++ - Bjarne Stroustrup

### Articles:

### Videos:

### Other:
- [Raylib docs](link.com)
- [SDL3 docs](link.com)

