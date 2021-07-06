---
title: "Game Dev Update #8"
date: 2019-05-30 17:00:00 -05:00
categories: [Update]
tags: [Godot, Game, Dev, Development, '3.1', 3D, looking for artist]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/godot_logo.png
---

## Medium At Work

I made a few small changes to the game the other day, and I cleaned up a lot of the code. I had been looking up some other systems that I wanted to include as well which I will outline below.

## Saving and Loading

The game now has a basic save and load function that runs in the background without the need for player interaction. When a player completes a level the system will check if this level is the highest completed, open the new level and save the game.

When they load the game again it will read the save file before anything else, and the dynamic level select screen will open the right levels before the user even notices anything.

## Level Select

The whole menu has an overhaul now, and shows the correct levels and numbers. I am still working on button sizes, but the test level is no longer listed.

## Changelog
v0.1.3.2:
<ul>
    <li>Save and Load added</li>
    <li>Level Select Menu Updated</li>
</ul>
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