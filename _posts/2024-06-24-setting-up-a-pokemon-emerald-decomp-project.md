## Short guide on setting up a pokemon emerald decomp

---

### Introduction

If you didn't know already, it is possible to edit and add to the old pokemon games. I have personally started working on a pokemon emerald rom hack of my own after playing custom games for years.

This is a short guide containing all the neccessary links and resources I used to get my project up and running. This is by no means a step by step guide and you will have to do some extra research but it is a good starting point nonetheless.

### Important Links

1. [pret/emerald](https://github.com/pret/pokeemerald)

This is the original decompilation project for pokemon emerald. If you just want the base emerald experience and would rather add all the extra stuff yourself then this is the repo you want to clone and work off.

2. [rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion)

This is the decomp repo I cloned and work on. It has a whole lot of __optional__ extras like; gen 1-9 pokemon, new movesets and a updated battle engine. I would recommend this when first getting into decomp hacking.

3. [huderlem/poryscript](https://github.com/huderlem/poryscript)

This is the github repo for __poryscript__, this will be the scripting language you use when making changes to the game (like editing signs and trainer speeches). You can opt to just edit the pokemon emerald source code (in c) but to be honest I don't think it's worth the extra effort. Also check out some of the other repos on the page, there's a lot of cool stuff there, like porymap which I will discuss in the __tools__ section below.

4. [Team Aqua's Hideout Youtube](https://www.youtube.com/playlist?list=PLLNv9Lq6kDmTIYfN5NvgQRvfOHTOXl0uU)

This youtube channel should be your go to for learning about what is possible when hacking pokemon emerald. Some of the videos are a bit dated and you should still read all the documentation provided by the other links but for when you get tired of banging your head against the wall this is hands down the best.

5. [Pokecommunity Forums](https://www.pokecommunity.com)

The pokecommunity forums are a great place to get information and share ideas. You might have to do some crawling and looking under rocks to find the good stuff but I have spent hours on here browsing and ~~stealing~~.

### Extra resources

1. [huderlem/porymap](https://github.com/huderlem/porymap?tab=readme-ov-file)

Yet another tool by huderlem! This is an amazing game editing tool that basically forms the centre piece of my room hacking project tools. You should read the docs provided on porymap but basically it makes editing the map and trainer's super easy. For example if I wanted to edit what the first trainer you fight on Route102 says I can go in porymap and click on his sprite. From there I can see what script is triggered when he notices the player.

2. [doom emacs](https://github.com/doomemacs/doomemacs)

If you don't have a text editor of choice then you should definitley use vscode, but I have been using emacs for a while and do not plan on changing to vscode __ever__. That being said there is a emacs config on my github as well as my config files for linux. If you do decide to use vscode check out [huderlem's poryscript vscode extension](https://github.com/huderlem/poryscript-pls) for nice syntax highlighting and all that.

3. [team aquas asset repo](https://github.com/Pawkkie/Team-Aquas-Asset-Repo)

A whole bunch of free to use assets.

### A quick rundown of the steps you should follow to setup your project

__Keep in mind I use linux so the steps may differ on different platforms.__
Also most of the resources I mentioned above have detailed instructions. If you are having issues reach out to me via email: anrichjtait@gmail.com. I'll be happy to help.

1. Follow the instructions on the [rh-hideout/pokeemerald-expansion](https://github.com/rh-hideout/pokeemerald-expansion) repo (assuming you plan to use the expansion repo, otherwise just clone the base repo mentioned above)
2. Use make and nproc to build the .gba file and then test it with a gba emulator of your choice.

 2.1
```
nproc
```
 
 2.2
 ```
 make -j (output of nproc)
 ```
 
 2.3 Wait for the build to complete and then test the .gba file. 
 
__You will need to do this every time you make changes and want to test them.__


### Conclusion
I hope this helps a bit, like I said feel free to reach out via email if you have issues, but please read the docs as much as possible first. Also I recommend making regular backups after major changes because it's pretty easy to break your project in the beginning.

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/I2I4ZPGX8)
