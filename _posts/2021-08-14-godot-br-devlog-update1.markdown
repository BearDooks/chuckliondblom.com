---
title: "Godot Battle Royale Devlog Update #1"
date: 2021-08-14 17:00:00 -05:00
categories: [Update]
tags: [Godot, Game, Dev, Development, '3.3', 'Battle Royale']
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/godot_logo.png
---

## Finally Working On A New Game

It has been a while since I posted anything, or worked on anything at all. My real job and family life took over a large chunk of my time so I was unable to sit down and really concentrate on working on something. I had also been working with the GodotNuts on the firebase plugin. It is super cool and I highly suggest everyone checks it out. <a href="https://github.com/GodotNuts/GodotFirebase">This Plugin</a> allows you to connect a Godot game to Google Firebase using the REST APIs without the need to recompile the Godot Engine.

## A New Idea

Talking to some of the guys from GodotNuts I decided I wanted to revisit an old idea to make a solo battle royle game when you would play with the CPU players. I also have plans to possible make it a multiplayer game if I get it to a point where it works and I can pivot to that.

I have not had a lot of time to work on it, and most of it was spent reading the old code when I tried this before, but I finally have a small working example. Using simple icons and tilesets I have been able to create small world with a single building. Inside of that building is a weapon you can pickup and use.

<a href="/images/br/br-1.gif"><img src="/images/br/br-1.gif" alt=""></a>

## Changes From The First Version

One of the biggest changes from the first version is how I worked through the issue of picking up an item. In the first version I was using an Area2D to see if there was an item on the ground, but I was never able to get the item to be picked up, and the code was getting out of hand checking for impossble situations.

I have since changed this to still use an Area2D, but that is for the item that is on the ground. Coming out of the player is a RayCast2D that allows me to see if I am close enough to an item, and what that item is. The player needs to be looking at the item, and have their mouse of it to pick it up. This has been working perfectly, until I put the item in the house, and the Area2D inside the house that checks if you are inside started blocking the item from being picked up. This was a simple fix with collision layers and masks.

## Next On Deck

The next thing I need to work on it getting the building editor in a good place so I can rapidly prototype buildings that I can save and place in the world. To do this I will need to come up with a tileset that works for me, and take the time to make sure the walls have the collison setup. 

Once I have this done I can setup the Area2D that is used to check if you are in the building and deal with the roof. To make it fair I want the player to not be able to see what is in a building unless they go into it. I plan in the future to add the ability to walk up to a window and peek inside of the building, but that is for later. I am trying to focus and getting a working model, before I being to add more to it.