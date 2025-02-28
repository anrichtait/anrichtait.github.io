---
title: Studylog - Implementing Component System
date: 2025-02-26 04:00:00 +/-TTTT
categories: [Studylog, C++, Game Dev]
tags: [cpp, gamedev, learning]     # TAG names should always be lowercase
description: An article following my attempt at creating a component system for my custom C++ game engine.
toc: true
comments: false
media_subpath: /assets/img/
---

## Introduction
In my last article I implemented the game loop for my custom C++ game engine. I also mentioned that I wanted to implement a texture manager next and that is what this article started out as. But I ended up scratching the original idea and instead implemented a component system for my game actors.

## Features
- **Currently Implementing:**
  - Component System (for player and enemies)

- **Implemented:**
  - Game Loop: Variable and fixed time step loops to handle all the processes a game might need.

- **Planned:** *This list of features is in the order I plan to implement them so it is subject to change.*
  - Texture Manager
  - Input System
  - Game State Machine
  - GUI

---

## Component System Design Considerations
When deciding how to represent game objects in my engine I considered two options. The first was a traditional component system and the other was an Entity Component System (ECS) system.

I ended up choosing to go with a more traditional component system. There were two big reasons I chose this over a ECS system. First off is the complexity, I used the [Bevy](https://bevyengine.org/) ECS before and that was amazing but the reasons for that are Rust specific in my opinion. This is due to how Rust manages memory and concurrency, the main reason to use [bevy_ecs](https://docs.rs/bevy_ecs/latest/bevy_ecs/) is the easy multithreading it facilitates. Now that is all good an well but I am not using Rust and I definetly don't know enough about ECS or C++ to implement a system that could rival the one Bevy uses. 

The second reason I chose a component system is because there is a really nice chapter on the [Component Pattern](https://gameprogrammingpatterns.com/component.html) in Robert Nystroms book, Game Programming Patterns. Like I have said in previous articles one of the reasons I'm working on this engine is so I can learn OOP programming and how to implement different patterns. 

![hand drawn picture](comp_dia.png)

As the above picture hopefully demonstrates I plan to represent entities - or GameActors in my case - as a class that acts as a container for component classes. Such as the input, texture and position components. I chose `GameActors` as the name to represent my entities purely because I like how it sounds. I don't really plan on making the distinction between GameActors and GameObjects because I think components can do the same thing without the extra complexity/boilerplate.

---

## Implementing the Component System
My implementation of the component system went through a couple different iterations and at one point I even considered just using an already established ECS solution. But I pushed through and now we have this janky, *but functional*, component system that I will now present and explain.  

**Project Layout:**  


![Project Layout](folder_str.png)   


To start with, I have now organized the project so it's not all just sitting in the project root. I then implemented the `component` class which will be the base class all components are built from.  

*Component.hpp*
``` c++
class GameActor;

class Component {
	public:
		Component(GameActor* owner) : owner(owner) {}

		void Update() {
			// implementation of Component
		}

		void FixedUpdate() {
			// implementation of Component
		}

	private:
		GameActor* owner;
};
```
> Note: We forward declare the GameActor class so we don't create circle #includes

This is pretty straight forward and there is still a lot I need to think about before I would say it's bullet proof, but for now it works. I will explain the `Update()` and `FixedUpdate()` members in a moment. Let's first look at the `GameActor` class for some more context.

*GameActor.hpp*

``` c++
class GameActor {
	public:
		void AddComponent(Component* component) {
			components.push_back(component);
		}

		void Update() {
			for (Component* component : components) {
				component->Update();
			}
		}

		void FixedUpdate() {
			for (Component* component : components) {
				component->FixedUpdate();
			}
		}

	private:
		std::vector<Component*> components;
};
```
Okay, so here is a little more going on.  
First, notice that a `GameActor` is made up of a vector (list) of `Components`. This way components can be added or removed as needed and all the GameActor class really does is store a list of the components it has and provides a way to update them. But components are still responsible for their implementation.

Now that I had the `Component` and `GameActor` classes I needed a way to trigger all of their updates at the right time. I'm not gonna lie, when I was still planning the whole component system this part blew my brain up a bit. I know in my head what I needed to achieve but I just couldn't think of any way to do it in code. I ended up with the solution below but, man oh man. This part of the implementation, tying all of these abstract ideas together... Now that was difficult.

*World.hpp*

``` c++ 
class World {
	public:
		void PushActor(GameActor* actor) {
			actors.push_back(actor);
		}

		void PopActor(GameActor* actor) {
			// remove actor from world
		}

		void Update() {
			for (GameActor* actor : actors) {
				actor -> Update();
			}
		}

		void FixedUpdate() {
			for (GameActor* actor : actors) {
				actor -> FixedUpdate();
			}
		}

	private:
		std::vector<GameActor*> actors;
};
```

This world class is very similar to the GameActor class. It doesn't store anything except a vector list of game actors for us to iterate through. The real utility provided by the `World` class is that now we have a way to store and reference all the actors in a scene. This also changes how our game loop works a bit. 

*main.cpp*
``` c++
	GameEngine game;
	World world;

	game.Initialize();

	while (game.Running()) {
	  game.Input();
	  world.Update();
	  world.FixedUpdate();
	  game.Render(alpha);
	  game.Clean();
}
```
> This is a vastly over-simplified version of the engine's game loop. If you want a better look at the actual code read my previous article on designing a game loop or have a look at [this commit](https://github.com/anrichtait/low-light-engine/commit/036924d806924d6a89d1c119cf9e2092758f1f76).

For those that have been following along or read my other article on game loops you will notice that now instead of all the loops being owned my a `GameEngine` instance `Update` and `FixedUpdate` are now owned by an instance of `World`. We can now call the update members of all of the game actors (and their components) in a unified way.

---

## Conclusion
I am atleast 50% aware of all the shortcomings of my current approach but I planned on implementing a texture manager and got sidetracked. This component solution I have works and for now that's good enough. *I seem to be thinking that a lot recently...*

But seriously, from what I have seen so far a lot of the code I write is going to be rewrittin in the future. So right now I want to focus on getting stuff done, I can worry about efficiency and smaller edge cases later.

## Sources and References:
Below are the resources I used while researching this article.

### Books:
- Game Programming Patterns - Robert Nystrom
- Programming Principles and Practice Using C++ - Bjarne Stroustrup

### Articles:
Nothing today folks.

### Videos:
Nothing today folks.

### Other:
- [Raylib docs](https://www.raylib.com/)
- [SDL3 docs](https://wiki.libsdl.org/SDL3/FrontPage)

