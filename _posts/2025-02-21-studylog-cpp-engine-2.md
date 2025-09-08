---
title: Studylog - Game Loop Design
date: 2025-02-21 04:00:00 +/-TTTT
categories: [Studylog, C++, Game Dev]
tags: [cpp, gamedev, learning]     # TAG names should always be lowercase
description: An article where I do a deep dive into game loop design and the solution I chose to implement in my custom engine.
toc: true
comments: false
media_subpath: /assets/img/
---

## Introduction
I recently started work on my custom game engine and so far have been testing the waters and trying out a couple things to get a better idea on how designing an engine actually works. I have been switching between raylib and SDL. After messing around a bit I've set my sights on building a 2D engine to start out with. Right now I don't have a full design spec but I think that's actually a good thing right now because it's hard to plan a project so large when I'm learning in the process. With the game loop alone my plans have drastically changed. 

In this article I talk about the research I did on game loops and the things I considered when thinking about implementations for my game engine. I also discuss the implementation I ended up going with and some of the challenges I faced while implenting the game loop.

---

## Planned Features
Part of my goals with this project is to learn about object orientated programming, because like it or not a huge amount of the systems we use are built with OOP. My key resources for learning OOP at the moment are *Game Programming Patterns by Robert Nystrom* and *Programming Principles and Practice using C++ by Bjarne Stroustrup*. With that in mind I will try to use specific patterns for each feature I implement. Like this game loop was designed after reading the chapter on game loops in Robert Nystrom's book.

So to begin with, while I still learn how to design a project of this scale I have broken the early stages into smaller "features" that I can focus on and knockout one by one. Lets take a quick look at some of the planned features before I get into the topic of this article, Game Loops.

_This list of features is in the order I plan to implement them. This section of my blog posts will sort of be a way to keep track of this for myself as well. So it's subject to change._
- Game Loop (obviously)
- Game State System to handle transitions between menu, playing, paused, etc.
- System to handle player, enemies, and other objects in the game. (This might be a component system)
- Input handeling system for the player that will allow remapping.
- First GUI implementations.

---

## Game Loop Design Considerations
Of all the game engines and frameworks I've used Unity, in my opinion, has the best game loop. It clearly seperates concerns and provides a fixed update and variable update loop. After I started looking into frameworks instead of engines I used Monogame for a bit. In Monogame the loop is basically structured as follows:
``` c#
Initialize();   // called once when the game starts
LoadContent();  // called once after initialize (used to load game assets)
Update();       // called repeatedly (used to update game logic)
Draw();         // called repeatedly (used to render graphics/textures)
```

This sort of game loop presents a problem though. It appears to have a fixed timestep update loop, like the one seen in Unity, but it doesn't, neither `Update()` nor `Draw()` have any checks to impose a fixed time interval on the game loop. This has some serious reprecussions for the overall game performance.

---

### Impact of Fixed vs. Variable Updates on Simulation and Performance
Without a fixed update, physics simulations can seriously bug out. Objects can fly through one another due to the inconsistent time steps affecting the physics and collision detection simulations. This also has an affect on AI and other time-dependent game logic.
If simulation updates depend on the frame rate, the game can behave very differently on different systems. High-end systems will run the simulation too quickly, and lower-end systems too slowly. This has some obvious reprecussions, especially for multiplayer games. 


A fixed update interval ensures that all simulation calculations occur at a consistent rate. This not only simplifies the logic for physics and AI but also helps maintain a stable game environment. If the rendering falls behind, the engine might need to process multiple fixed updates in one frame, potentially introducing slight delays but it's still better than no fixed time step at all.

---

## Implementing the Game Loop
My goals for the game loop are to separate the fixed update and normal update loops. This will stabilize the physics and other simulation-related code and also allow me to later possibly add multiplayer support to the game engine. While implementing the game loop, I did my best to follow the best practices discussed in the book *Game Programming Patterns*. Let's take a closer look at the full implementation.

### GameEngine Class
The foundation of the game loop is the `GameEngine` class. This class contains the building blocks for the game loop.
```cpp
class GameEngine {
    public:
        GameEngine() : ge_Running(true) {}
        ~GameEngine() {}

        void Initialize();        // Called once at program start
        void Input();             // Variable update for user input
        void Update();            // Variable update for non-simulation logic
        void FixedUpdate();       // Fixed update for simulation (AI, Physics, Collision, etc.)
        void Render(double alpha); // Camera and rendering updates; alpha compensates for frame lag
        void Clean();             // Called before program end to clean up resources

        bool Running() { return ge_Running; }

    private:
        bool ge_Running;
};
```

I'm not going to go into the code for each member function right now, but here's a quick summary and some interesting notes:
- **`void Initialize()`**: Called once when the game starts; ideal for initial asset and data loading.
- **`void Input()`**: Called once per frame and used for user input. Since user input dictates the majority of what is happening in a game, we check for that before running through the rest of the game loop.
- **`void Update()`**: Called once per frame and used for everything that does not fall into the rendering or simulation-related categories. This includes updating variables and checking conditionals.
- **`void FixedUpdate()`**: Called at a fixed rate and used for all simulation-related code (AI, physics, collision, etc.).
- **`void Render(double alpha)`**: Called once per frame. The alpha value can be used to compensate for frame lag.
- **`void Clean()`**: Called at the end of the program to clean up and unload any data needed before the program can end.
- **`bool Running()`**: Provides the condition to keep the engine running.

---

### main.cpp FINALLY THE LOOP
Considering that the game loop is such an important part of the engine—and everything else builds off of it—I decided to implement it in the `main()` function. From here, all the other features can be branched out into their own files and headers.

> The below code block is condensed, to see the full implementation look at the **main.cpp** in [this repo](https://github.com/anrichtait/low-light-engine).

``` c++

int main(void) {
	GameEngine game;
	game.Initialize();

	auto previous = std::chrono::high_resolution_clock::now();
	double lag = 0.0;
	const double FIXED_UPDATE_INTERVAL = 1.0 / 60.0;
	const double MAX_LAG = 0.25;

	while (game.Running()) {
		auto current = std::chrono::high_resolution_clock::now();
		double deltaTime = std::chrono::duration<double>(current - previous).count();
		previous = current;

		if (deltaTime > MAX_LAG) {
			deltaTime = MAX_LAG;
		}
		lag += deltaTime;

		game.Input();
		game.Update();

		int fixedUpdateCount = 0;
		while (lag >= FIXED_UPDATE_INTERVAL) {
			game.FixedUpdate();
			lag -= FIXED_UPDATE_INTERVAL;
			fixedUpdateCount++;

			if (fixedUpdateCount > 5) {
				break;
			}
		}
		double alpha = lag / FIXED_UPDATE_INTERVAL;
		game.Render(alpha);
	}

	game.Clean();
	return 0;
}
```

---

### Talking about the loop
> As I mentioned earlier, this game loop closely follows the best practices outlined in *Game Programming Patterns* by Robert Nystrom. For a deeper look at exactly how game loops work and some of the other technicalities I didn't cover I highly recommend checking out the sources at the end of this article. Without using all of them I wouldn't have been able to implement this loop.

Here’s my take on the loop and some of the decisions I made while I implemented it.

We start by initializing the game. The `Initialize()` method is called before the loop begins, and several important variables are set up here. To give you a brief overview of the key variables:

- **`previous`**: Holds the timestamp of the previous frame, which is used to calculate `deltaTime`.
- **`lag`**: Accumulates the extra time between frames
- **`FIXED_UPDATE_INTERVAL`**: The fixed update time interval. In my case, it’s 1/60th of a second.
- **`MAX_LAG`**: A cap on how much lag can be accumulated to prevent excessive frame skips.
- **`current`**: The timestamp of the current frame.
- **`deltaTime`**: The time between frames.

Once the initialization is done, we enter the main loop, which will keep running until the game/program ends. A few checks are made here to keep things consistent. First, we check and clamp `deltaTime` to avoid situations where it becomes too large. If `deltaTime` gets too high, it could cause a massive spike in lag, which leads to longer frames and erratic performance. By capping `deltaTime` we ensure the game remains stable.

After checking for input in the `game.Input()` call and running the variable update (`game.Update()`) loop, we check if enough lag has accumulated to trigger the fixed updates. This is done with:

``` c++
while (lag >= FIXED_UPDATE_INTERVAL)
```

If the accumulated lag is higher than or equal to the fixed update interval, we run the simulation-related code (e.g., physics, AI, etc.) within `game.FixedUpdate()`. This guarantees that the simulation updates occur at a consistent rate, independent of the frame rate.

There’s a safety check in place to prevent the fixed update loop from running too many times in a single frame, which could happen if there’s a large amount of lag. If `fixedUpdateCount` is higher than 5, we break out of the loop, this prioritizes simulation consistency over drawing frames. This ensures that the simulation doesn't get stuck in an infinite loop, and the rendering process keeps running smoothly.

Lastly, we get the `alpha` value, which is used for interpolation in the renderer.
> Note: I still do not 100% how alpha will be used so I'm not going to say much more on it now. 

---

## Conclusion
Implementing this game loop turned out to be more challenging and time-consuming than I initially anticipated, but it was a great step in building the foundations of my engine. Now that the game loop is in place and functioning, I can move forward.

Originally, I planned to get into implementing the Game State System next, but I’ve decided to shift gears for now. I want something more tangible to test the game loop and identify any potential bugs or issues before I move onto other features. Plus, I’d like to see some visual progress to keep me motivated. 

So, next up is a texture manager system and a simpler state machine for the player character. These will allow me to start testing and rendering actual game objects, which will help me test the game loop’s performance.

---

## Sources and References:
Below are the resources I used while researching this article.

### Books:
- Game Programming Patterns - Robert Nystrom
- Programming Principles and Practice Using C++ - Bjarne Stroustrup

### Articles:
- [Fix Your Timestep! - Gaffer on Games](https://gafferongames.com/post/fix_your_timestep/)
- [Mastering the Unity Game Loop](https://bleedingedge.studio/blog/master-game-loop-startvsupdate-function/)

### Videos:
- [Video on deltaTime](https://youtu.be/yGhfUcPjXuE?si=sz4cprsYYvSd88Wl)

### Other:
- [Raylib docs](https://www.raylib.com/)
- [SDL3 docs](https://wiki.libsdl.org/SDL3/FrontPage)
