## Short Guide on Setting Up a Pokémon Emerald Decomp

---

### Introduction

If you didn't know already, it's possible to edit and expand upon the old Pokémon games. I recently started working on my own Pokémon Emerald ROM hack after enjoying custom games for years.

This guide provides essential links and resources to kickstart your project. It's not a step-by-step tutorial, so expect to do some additional research, but it's a solid starting point.

### Important Links

1. [pret/pokeemerald](https://github.com/pret/pokeemerald)

  This is the original decompilation project for Pokémon Emerald. If you want the base Emerald experience and prefer to add extras yourself, this is the repository to clone.

2. [rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion)

   I recommend this decomp repository. It includes optional extras like Gen 1-9 Pokémon, new movesets, and an updated battle engine. Ideal for newcomers to decomp hacking.

3. [huderlem/poryscript](https://github.com/huderlem/poryscript)

   This is the GitHub repository for Poryscript, the scripting language for making changes to the game (e.g., editing signs and trainer speeches). Editing the Pokémon Emerald source code directly in C is possible but more complex. Also, explore other tools like Porymap mentioned in the tools section below.

4. [Team Aqua's Hideout YouTube](https://www.youtube.com/playlist?list=PLLNv9Lq6kDmTIYfN5NvgQRvfOHTOXl0uU)

   This YouTube channel is invaluable for learning about Pokémon Emerald hacking possibilities. While some videos are dated, they complement the documentation from the other links.

5. [Pokecommunity Forums](https://www.pokecommunity.com)

   These forums are excellent for information and idea sharing. There's a wealth of knowledge here, though you might need to dig a bit to find exactly what you're looking for.

### Extra Resources

1. [huderlem/porymap](https://github.com/huderlem/porymap)

   Another tool by Huderlem! Porymap is a powerful game editing tool and a cornerstone of my ROM hacking toolkit. It simplifies editing maps and trainers. For instance, you can edit the first trainer's dialog on Route 102 by clicking on their sprite in Porymap.

2. [Doom Emacs](https://github.com/huderlem/poryscript-pls)

   If you're undecided on a text editor, consider VSCode. I've been using Emacs and have configs available on my GitHub. If you choose VSCode, check out Huderlem's Poryscript VSCode extension for syntax highlighting and more.

3. [Team Aqua's Asset Repo](https://github.com/Pawkkie/Team-Aquas-Asset-Repo)

   A collection of freely usable assets.

### Quick Setup Steps

__Note: These steps assume Linux; they may differ on other platforms.__

Most linked resources provide detailed instructions. If you encounter issues, reach out via email: anrichjtait@gmail.com. I'm happy to help.

1. Follow instructions on [rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion) (if using the expansion repo) or clone the base repo mentioned above.
2. Build the `.gba` file using `make` and `nproc`, then test it with a GBA emulator of your choice.

   2.1 Check the number of changes:
   
   ```
   nproc
   ```
   
2.2 Build the ROM:

```
make -j [number from nproc output]
```

2.3 Wait for the build to complete and test the `.gba` file.

__Repeat this process whenever making changes to test them.__

### Conclusion

I hope this guide helps you get started. Feel free to reach out via email if you encounter issues, but please read the documentation as much as possible first. Also, remember to make regular backups, especially after major changes, as early mistakes can be easy to make.

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/I2I4ZPGX8)
