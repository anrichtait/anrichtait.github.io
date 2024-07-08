## Short Guide on Setting Up a Pokémon Emerald Decomp

---

### Introduction

If you didn't know already, it's possible to edit and expand upon the old Pokémon games. I recently started working on my own Pokémon Emerald ROM hack after enjoying custom games for years.

This guide provides essential links and resources to kickstart your project. It's not a step-by-step tutorial, so expect to do some additional research, but it's a solid starting point.

### Important Links

1. **[pret/pokeemerald](https://github.com/pret/pokeemerald)**
   
   This is the original decompilation project for Pokémon Emerald. If you want the base Emerald experience and prefer to add extras yourself, this is the repository to clone.

2. **[rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion)**

   I recommend this decomp repository. It includes optional extras like Gen 1-9 Pokémon, new movesets, and an updated battle engine. Ideal for newcomers to decomp hacking.

3. **[huderlem/poryscript](https://github.com/huderlem/poryscript)**

   This is the GitHub repository for Poryscript, the scripting language for making changes to the game (e.g., editing signs and trainer speeches). Editing the Pokémon Emerald source code directly in C is possible but more complex. Also, explore other tools like Porymap mentioned in the tools section below.

4. **[Team Aqua's Hideout YouTube](https://www.youtube.com/playlist?list=PLLNv9Lq6kDmTIYfN5NvgQRvfOHTOXl0uU)**

   This YouTube channel is invaluable for learning about Pokémon Emerald hacking possibilities. While some videos are dated, they complement the documentation from the other links.

5. **[Pokecommunity Forums](https://www.pokecommunity.com)**

   These forums are excellent for information and idea sharing. There's a wealth of knowledge here, though you might need to dig a bit to find exactly what you're looking for.

### Extra Resources

1. **[huderlem/porymap](https://github.com/huderlem/porymap)**

   Another tool by Huderlem! Porymap is a map editor for Pokémon games, making it easier to create and edit maps visually rather than dealing with raw code.

2. **[porygon](https://github.com/huderlem/porygon)**

   Porygon is a suite of tools for managing graphics in Pokémon games. It's particularly useful for handling tilesets and sprites.

### Tools and Prerequisites

Before starting your project, ensure you have the following tools installed:

- **DevKitARM**: Required for compiling the project.
- **Python**: Needed for various scripts and tools.
- **GNU Make**: The build system used for compiling the project.
- **Git**: Version control system for managing your codebase.

You can install these tools on a Linux system using the following commands:

```sh
sudo apt-get update
sudo apt-get install build-essential devkitpro pacman
```

### Setting Up the Project

Follow these steps to set up your Pokémon Emerald decomp project:

#### Step One: Clone the Repository

Choose the repository you want to work with and clone it:

```sh
git clone https://github.com/rh-hideout/pokeemerald-expansion.git
cd pokeemerald-expansion
```

#### Step Two: Install Dependencies

Install the required dependencies using `make`:

```sh
make setup
```

#### Step Three: Build the Project

Build the project to create the initial ROM file:

```sh
make -j$(nproc)
```

This command uses all available processing units to speed up the build process.

#### Step Four: Configure Tools

Set up Poryscript and other tools by following the instructions in their respective repositories. Typically, you will need to copy some configuration files and make necessary adjustments.

### Common GitHub CLI Commands

When working on your project, you'll frequently interact with GitHub. Here are some common GitHub CLI commands you might need:

1. **Initialize a Repository**:

   ```sh
   git init
   ```

2. **Clone a Repository**:

   ```sh
   git clone https://github.com/username/repository.git
   ```

3. **Check Repository Status**:

   ```sh
   git status
   ```

4. **Add Changes to Staging**:

   ```sh
   git add .
   ```

5. **Commit Changes**:

   ```sh
   git commit -m "Your commit message"
   ```

6. **Push Changes to GitHub**:

   ```sh
   git push origin main
   ```

7. **Pull Changes from GitHub**:

   ```sh
   git pull origin main
   ```

8. **Create a New Branch**:

   ```sh
   git checkout -b new-branch-name
   ```

9. **Switch Between Branches**:

   ```sh
   git checkout branch-name
   ```

10. **Merge Branches**:

   ```sh
   git merge branch-name
   ```

11. **View Commit History**:

   ```sh
   git log
   ```

12. **Create and Manage Pull Requests**:

   ```sh
   gh pr create
   gh pr list
   gh pr view <pr-number>
   ```

### Conclusion

I hope this guide helps you get started. Feel free to reach out via Discord if you encounter issues, but please read the documentation as much as possible first. Also, remember to make regular backups, especially after major changes, as early mistakes can be easy to make.

Most linked resources provide detailed instructions. If you encounter issues, reach out on my Discord channel: https://discord.gg/8a7SXdHy

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/I2I4ZPGX8)
