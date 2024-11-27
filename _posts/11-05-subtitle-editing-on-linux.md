---
title: Subtitle Editing On Linux and some of the ways to make it suck less
date: 2024-11-05 13:30:00 +/-TTTT
categories: [Work/Life, Subtitle Editing]
tags: [linux, archlinux, subtitle editing, blogging]     # TAG names should always be lowercase
description: A general look at subtitle editing as a freelance job and some of the ways to make it suck less.
toc: true
comments: false
media_subpath: /assets/img/
---

## Introduction
I first started with subtitle editing in 2021. Back then every episode I worked through felt like an uphill climb that would never end. Almost exactly like my new game + playthrough of God of War. Except it's not fun and you defintely don't feel like the god of anything, that's for sure.

Since then I have managed to make that struggle a lot less. Don't get me wrong, subtitle editing is defintely not a fun job, but a job it is nonetheless. And since you are reading this it probably means you are in one of three stages and thinking something along the lines of:
1. **Beginner:** _"I'm so grateful for a job, and hey how bad could it be anyway?"_
2. **Seasoned:** "_My eyes hurt but even when I close them I see subtitles..._"
3. **Veteran:** _"When did I start speaking Spanish?"_

Haha, very funny, I know. So let's take a more serious look at the pros and cons of the job before getting into the things I learnt along the way.

---

## What Subtitle Editing Involves
For those that are new to subtitle editing, it's pretty simple. 

Subtitle files are saved as .srt or plain text formats, which contain lines of dialogue with corresponding time codes.
``` 
00:04:33,013 --> 00:04:34,013
Smash the pots,

2
00:04:34,077 --> 00:04:34,703
Burn the paintings.

3
00:04:34,710 --> 00:04:36,043
The art isn't the art,

4
00:04:36,070 --> 00:04:37,336
The art is never the art.
```

These time codes correspond to a range of time in the video that the subtitle file was synced with. How exactly to edit timecodes is out of the scope of this article but I do have some general tips in the Essentials section. 

But first! Let's look at the pro's and con's of doing subtitle editing as a freelancer.

### Pros:
So far this post has painted subtitle editing in a very negative light,
- Once you are in the industry there is a lot of high paying work
- Flexible working hours
- Lot's of free software
- Automateable (to a certain extent)
- Remote
- Opportunity to practice and learn a new language

### Cons:
I do not really include any industry wide issues, like strict deadlines and the overall industrie's tendence towards workaholism. And my perspective on a job at this point in my life is that I do it to make money, not for passion. I have hobbies for passion, work is just there to support my expenses. That being said here are some things to consider:
- You will be working in the TV industry which is notorious for not giving a fuck about your personal life or how busy you are.
- Often the subtitles you will be working on will have video in another language and a really bad script or none at all. 

---

## Essentials to excel at subtitle editing
These essentials are mix bag of beginner and advanced skills that you should aim to hone when doing subtitle editing. This list does not cover everything you need to know or focus on but includes the things that I think are the most important.

- __Lip-Syncing:__   
  Okay so this one is job specific, if you are doing subtitles for a TV show or actually any video where there is a lot of focus on converstation and the speakers' faces are shown it is critical that you focus on trying to match your words to the way the speaker's mouth moves in the video. This is difficult and I still struggle with this at times, especially when the video is in another language. But if you focus on this and hone the skill not only will it make your subtitles stand out (because most people don't actually do this, just look at Netflix and Anime) but it will also force you to get involved in actual script editing and writing, because let's face it a google translated script is never going to be 100% accurate and sometimes things don't translate well and then you will need to use your imagination. I have gotten translated scripts that make no sense and basically forced me to guess what the characters were saying and rewrite a large part of the script.

- __Micro Expressions:__   
  When I say Micro Expressions I am refering to sighs of exasperation, gasps and the like. Since most of my experience has been in the TV side of subtitle work this comes up pretty often. Micro expressions are shown in subtitles as capital letters in brackets `(OUT), (IN), (CRY)`.  

  For example let's look at the following example script:

  ```
  00:00:15,000 --> 00:00:17,000 # First Speaker
  I'm really sorry for shouting at you earlier.

  00:00:18,000 --> 00:00:20,000 # First Speaker
  Please don't sigh like that,

  00:00:20.000,000 --> 00:00:22,000 # First Speaker
  I didn't mean it.
  ```
  Now looking at this example there is no immediate problem, let's unpack this example and see where the issues are. First we need to consider who we are doing subititles for at the end of the day. Who uses subtitles? Of the top of my head I can think of 3 distinct groups:
  1. People who are hearing impaired 
  2. People who don't understand the language spoken in the source video.
  3. Dubbing artists.

  The only group here that doesn't strictly need the micro expressions is the second. But for people who are hearing impaired micro expressions can be super important, like in the above example there is no indication that the second speaker did anything or that there is even a second speaker. And this can defintely be an issue of the viewer can't see the speakers face. The second group that needs these micro expressions are the dubbing artists. 

  I am very fortunate that my wife is a dubbing artist so she has helped me a lot to understand what goes into dubbing and how important micro transactions are. Imagine a TV show or movie that is dubbed but none of the sighs or laughs or anything were dubbed. It would look empty, wrong and most likely ruin the viewing experience.

  This is so important that I would go so far as to say that if you can't read your subtitles without the video for context then they are probably not ready to be submitted. This is part of the reason that I do my final checks in a text editor not the subtitle editing software.

  Below is an example with the second speakers micro expression included.

  ```
  00:00:15,000 --> 00:00:17,000 # First Speaker
  I'm really sorry for shouting at you earlier.

  00:00:17,000 --> 00:00:18,000 # Second Speaker
  (OUT)

  00:00:18,000 --> 00:00:20,000 # First Speaker
  Please don't sigh like that,

  00:00:20.000,000 --> 00:00:22,000 # First Speaker
  I didn't mean it.
  ```
  Just by adding the reaction by the second speaker we can drastically improve our subtitle quality and encounter less fix requests after we have submitted the work.

---

## Software and Workflow

---

## Using whisper to do the heavy lifting

---

## Brain Made
This post was [Brain Made](https://brainmade.org/index.html#about). 

<img src="https://brainmade.org/black-logo.png" alt="This blog post was Brain Made" width="20%" height="auto">

