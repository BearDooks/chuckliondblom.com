---
title: "Installing RetroArch and Emulation Station Ubuntu 16.04"
date: 2017-03-20 10:08:42 -0500
categories: [guide]
tags: ["16.04", emulation, emulation station, emulationstation, nes, psx, retroarch, snes, ubuntu]
author: chuck lindblom
sharing: true
show_author_profile: true
---

Edit:
  
I wrote this and then I found this method is no good. There is so much that does not work. Adding to this seems impossible. If you really want to run this on ubuntu, then go to the official site and follow their directions.

<figure>
	<a href="/images/Retropie_Splash.png"><img src="images/Retropie_Splash.png" alt=""></a>
</figure>

sudo add-apt-repository ppa:emulationstation/ppa
  
sudo add-apt-repository ppa:libretro/stable
  
sudo apt update
  
sudo apt install emulationstation emulationstation-theme-simple
  
sudo apt install libretro-nestopia libretro-snes9x-next libretro-mupen64plus libretro-mednafen-psx
