---
title: "Looking At Old Code"
date: 2019-07-16 13:20:00 -05:00
categories: []
tags: [LightsOut, OldCode, Code, Godot, Android]
author: chuck lindblom
sharing: true
show_author_profile: true
cover: /images/lightsout/lightsout_update.png
---

## Thanks Google

This all started when I got the following email from Google Play

![Image](/images/lightsout/lightsout_update.png){:.shadow.rounded}

<!-- more -->

After a quick check I found there was not current way to export an Android app from Godot 2.1.X to make a 64bit version of it. That was going to be a problem. Luckily for me Godot released a RC for version 2.1.6. This update, among other things, was going to allow the export to a 64bit app. I had figures since it was an RC I would wait. The release timing for most of these versions had seemed to be a little over a week. Cut to weeks later and there was still no production release.

I thought the best course at that point would be to use the RC and get the app up there. So I downloaded the RC, put the export templates in there, configured the engine and uploaded my APK. Cut to V1.2 release.

![Image](/images/lightsout/v1_2.png){:.shadow.rounded}

Wouldn't you know it that a mere day, nay, hours after my update went live, Godot releases the Stable Client for 2.1.6. After some fighting with myself I downloaded that, compiled it all again, and uploaded 1.2.1 of LightsOut! This time I was able to target API 28 for Android which is another new requirement.

I am happy to report that v1.2.1 is live and will continue to be in the play store for a while, I hope. I am not sure how much longer Godot will support the 2.1.X branch of the engine, so maybe I need to look into moving the code to version 3.1.X

## LightsOut! Was A Dumpster Fire

While this whole process was going down, I decided to investigate the code and see how much I have learned since I started this whole process of using Godot. I want to preface this with the reminder that I am 100% a rookie when it comes to writing code, and half the time I don’t know what I am doing.

The code for LightsOut! Is a dumpster fire. There is no doubt in my mind that it is fundamentally broken, and I am honestly surprised it works at all. A lot of the calls in the code are worthless or don’t need to be made. I didn’t store objects correctly so I could stop the number of times Godot had to look for a node. The logic in the game is a hack job and a half.

This is 100% something I would love to go back to, but re-write from the ground up, since trying to fix the code from 2.1.6 seems worthless. Maybe I will open it up for others to help me and get some ideas on how to make it better in the future.

I would love to get some high score things working, even if it is a simple site that stores the data and calls for the data. I have ideas on how to get it working, just need to find time to build it all.
