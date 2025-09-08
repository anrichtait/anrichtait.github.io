---
title: Guide - Setting Up a Pokémon Emerald Decomp
date: 2024-06-24 18:00:00 +/-TTTT
categories: [Guides, Pokémon]
tags: [pokemon]     # TAG names should always be lowercase
description: Quick start guide on getting a pokemon emerald decomp project setup.
toc: true
comments: false
media_subpath: /assets/img/
---

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

__These steps assume Linux; they may differ on other platforms.__

__Also this assumes that you are either using the [pret pokemerald](https://github.com/pret/pokeemerald) repo or the [rh hidout expansion](https://github.com/rh-hideout/pokeemerald-expansion) repo as a base for your project.__

__These steps are for reference only, if you are completley new I would highly recommend following the in depth guides for forking, building etc. on the respective repostories!__

#### Step One:
Fork the repo you want to base your project on and name it whatever you want.

#### Step Two:
Clone your personal repository to a directory on your system.

``` bash
git clone https://github.com/user_name/repo-name.git
```
You will now have your pokemon emerald project on your sysem for editing! I recommend uploading your changes to Github every time you make a big edition (or even a small one), this will allow you to revert changes if you break something and also track your progress through the very helpful github commit history.

#### Step Three:
Next go to the [Poryscript](https://github.com/huderlem/poryscript) github page and download a release version to your system.

#### Step Four:
Once the download is complete create a new directory `poryscript` in the `tools/` directory of your project repo.


#### Step Five:
Copy the files `poryscript` command line tool and the `font_config.json` files from the release folder into the `poryscript/` directory you just made.

#### Step Six:
__6.1__ You can now create a script called `convert_inc.sh` that will be used to convert all the .inc files to .pory files. You can then make script changes using the poryscript syntax.

Here is the script:
```bash
#!/bin/bash

for directory in data/maps/* ; do
	pory_exists=$(find $directory -name $"scripts.pory" | wc -l)
	if [[ $pory_exists -eq 0 ]]; 
	then
		inc_exists=$(find $directory -name $"scripts.inc" | wc -l)
		if [[ $inc_exists -ne 0 ]]; 
		then
			echo "Converting: $directory/scripts.inc"
			touch "$directory/scripts.pory"
			echo 'raw `' >> "$directory/scripts.pory"
			cat "$directory/scripts.inc" >> "$directory/scripts.pory"
			echo '`' >> "$directory/scripts.pory"
		fi
	fi 	
done
```
__6.2__ Make the script executable with `chmod +x conver_inc.sh`.

__6.3__ Run the script using `./convert_inc.sh`


#### Step Seven:
Build the `.gba` file using `make` and `nproc`, then test it with a GBA emulator of your choice.

   2.1 Check the number processing units available.
   
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

I hope this guide helps you get started. Feel free to reach out via discord if you encounter issues, but please read the documentation as much as possible first. Also, remember to make regular backups, especially after major changes, as early mistakes can be easy to make.

Most linked resources provide detailed instructions. If you encounter issues, reach out on my discord channel: https://discord.gg/8a7SXdHy

