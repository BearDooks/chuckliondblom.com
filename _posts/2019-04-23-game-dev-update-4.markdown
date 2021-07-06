---
title: "Game Dev Update #4"
date: 2019-04-23 17:00:00 -05:00
categories: [Update]
tags: [Godot, Game, Dev, Development, '3.1', 3D, looking for artist]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /assets/images/godot_logo.png
---

# The Game Is Taking Shape

So I did manage to get some time to work on the game while I was out in California. I have been hard at work fixing a few bugs that I had found in the game and working to make it mildly playable. 

The only issues I have run into I will discuss below, but things are finally shaping up nicely.

<!--more-->

# New Title Screen

I wanted to get a new title screen into the game so that it looked a little more polished. I also didn't feel like working through some of the bugs in the game.

<a href="/images/trafficjam/title.png"><img src="/images/trafficjam/title.png" alt=""></a>

I am pretty happy with how it is currently. There is a gif below of the Title Screen in action, as I have cars and such moving through it.

# Gameplay Is Coming Along

I have been hard at work trying to make this game better, and make it fun to play. That is always the issue I have, I don't think the game is fun, but others do. I have also added some new vehicles, and changed how they spawn, and how they act in the world.

<a href="/images/trafficjam/tj5.gif"><img src="/images/trafficjam/tj5.gif" alt=""></a>

From this small gif you can see the title screen in action, and also the new level select screen. The level buttons are generated on the fly which is nice, I am still working out some finer details with them. Since that gif, and this post I have also updated the font on a lot of buttons so it doesn't look as generic.

# Annoying Bug Of The Week

While it is not a game breaking on, it is still super annoying. There is a bug when you win, or you crash the vehicles and the menu appears. The cars and the smoke are rendered in front of it for some off reason.

<a href="/images/trafficjam/crash_bug.png"><img src="/images/trafficjam/crash_bug.png" alt=""></a>

I am still working through that and hope to have it fixed soon. It is probably some stupid issue with the layers in the game.

## Changelog
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
Basic game working - End of July