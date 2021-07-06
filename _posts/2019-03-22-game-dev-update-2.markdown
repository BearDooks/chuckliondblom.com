---
title: "Game Dev Update #2"
date: 2019-03-22 17:00:00 -05:00
categories: [Update]
tags: [Godot, Game, Dev, Development, '3.1', 3D, looking for artist]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/godot_logo.png
---

# Test Scene Is Running

I got the test scene of the game finally running. It took some time but I was able to get the low poly car into Godot, and I was actually able to make a scene out of it. It took a bit to get used to using blender to get everything working, but I found a really good low poly model that I was able to export from blender as a .obj file. Once it was imported it was a simple drag and drop and I had my car on the screen like you can see below. I have to say I was quite proud of myself since I have never done anything like that before.

<a href="/images/trafficjam/normal_car.png"><img src="/images/trafficjam/normal_car.png" alt=""></a>

<!--more-->

From there I started the scene and I didn't see anything. Stupid of me, I forgot to put a camera in the scene, otherwise how would it know where to look or what to show. Once I got that in there, the car just fell right down. Again, stupid, I need something like a road that has no gravity and a solid body for the car to sit on. Dumb......

I fixed that up and I finally got a test scene running

<a href="/images/trafficjam/test_scene.png"><img src="/images/trafficjam/test_scene.png" alt=""></a>

## Changelog
v0.1.1:
<ul>
    <li>Switching to 2D</li>
</ul>
v0.1:
<ul>
    <li>Game created</li>
    <li>Thoughts on paper</li>
</ul>

## The 2D Switch

3D is cool, don't get me wrong, but I took a good hard look at where I was and what I was doing, and I saw that I can't deliver what I want. This project might be to big of one for me to start on not knowing how the 3D side of things works. Odds are I will make another 3D project that is much smaller, and way more simple so I don't need to deal with this currently. Also going back to 2D will allow me to work faster and get the prototype further in a shprter amount of time.

## Roadmap
Basic game working - End of July