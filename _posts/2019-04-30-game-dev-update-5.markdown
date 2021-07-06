---
title: "Game Dev Update #5"
date: 2019-04-30 17:00:00 -05:00
categories: [Update]
tags: [Godot, Game, Dev, Development, '3.1', 3D, looking for artist]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/godot_logo.png
---

# I Am Slacking

I am hitting a point where the game is taking great shape, but there are bugs or features that I don't want to work on because to me they don't seem as much fun. I am still trying to power through it all, and I have a basic roadmap on Trello for what the current needs are. I just need to really stick to it. I am still looking for an artist to help me out, that hasn't changed...

<!--more-->

# New Options Menu

<a href="/images/trafficjam/options.png"><img src="/images/trafficjam/options.png" alt=""></a>

Its not much but I have a volume slider and a mute button to control the music. It took me a while ot really figure out what was going on, until I leanred there is a built in function to convert linear to db in Godot and vice versa. 

# Vehicle Spawning Code Refactor

While you can't really see it, I took around 100 lines of code out of the test level script and replaced it with a simple function. It does the work for all the spawners, and all they need to do is pass along their postion, their timer, the direction, and if the vehicle needs to be scored or not. As you can see I am really not sticking to my plan of don't refactor until the end because I really don't want to add more things. 

# Bug Sqishing

While I do have issues working on this project and adding new things, I am still working out the bugs that I have introduced. I fixed an issue where the win/crash menu was not being drawn correctly over everything else in the level. I also added a small wait timer to a crash so the player can see the chaos that is a failure.

I have also updated the code to look morer appealing visually, makign sure each vehicle and level have the same functions, and in the same order in the script. Since everything has its own script to make them unique I needed to make sure I had the code on lock so I wouldn't be searching all the time for something.

# v0.1.3.1 Commit

<a href="/images/trafficjam/v0131edit.png"><img src="/images/trafficjam/v0131edit.png" alt=""></a>

Thats some changes right there....

## Changelog
v0.1.3.1:
<ul>
    <li>Added music volume slider</li>
    <li>Refactored vehicle spawn</li>
</ul>
v0.1.3:
<ul>
    <li>Fixed Crash/Win Menu from not being in front of everything</li>
    <li>Refactored a lot of code to clean it and make it more uniform</li>
    <li>Fixed the restart level button to reload the scene</li>
    <li>Added const to each level to give it a number</li>
    <li>Updated Trello with new cards</li>
</ul>
v0.1.2:
<ul>
    <li>Added new font to game</li>
    <li>Add title screen and level select</li>
    <li>Added new vehicles including Cop Car</li>
    <li>Added Crash and Win Screen</li>
    <li>Added Level 1 to game for testing</li>
    <li>Updated artwork for roads and added new tiles to tilemap</li>
    <li>BUG: Crash/Win Screen rendered in wrong layer</li>
</ul>
v0.1.1:
<ul>
    <li>Switching to 2D</li>
</ul>
v0.1:
<ul>
    <li>Game created</li>
    <li>Thoughts on paper</li>
</ul>

## Roadmap
Basic game working - End of July?
