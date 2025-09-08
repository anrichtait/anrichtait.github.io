---
title: Studylog - OOP and Component Systems
date: 2025-03-01 04:00:00 +/-TTTT
categories: [Studylog, C++, Game Dev]
tags: [cpp, gamedev, learning]     # TAG names should always be lowercase
description: Discussion on how "complex" object orientated programming can simplify component systems.
toc: true
comments: false
media_subpath: /assets/img/
---

## Foreword
In my previous blog post I designed and implemented the basics of a component system for my custom c++ game engine. That implementation has some serious flaws and shortcomings. In this post I pick apart the current system and look at ways to make this system more intuitive.

## Redesigning the Component System
So at the moment a `GameActor` is basically just a container for `Components`. This all works fine and well but if we look a bit deeper at the implementation we can see a few issues.

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

So as you can see a `GameActor` stores it's components in a vector of components. In my head this seemed like a good method but in practice this presents some issues.






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
