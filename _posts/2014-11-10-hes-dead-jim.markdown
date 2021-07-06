---
title: "He's Dead Jim..."
date:  2014-011-10 10:00:00 -0500
categories: [guides, news,rants,site news, tech news]
tags: [backup, data loss, drive, linux, lost, server, wamp, web server, windows]
author: chuck lindblom
sharing: true
show_author_profile: true
---

It pains me to admit that after years and years in the IT field, I was finally bit by my laziness in my own home network. My server crashed.


<figure>
	<a href="/images/explosion.jpg"><img src="/images/explosion.jpg" alt=""></a>
</figure>

# The Story

On November 5th 2014, I was at work when I needed to SSH back home to check on something. From my work machine I tried to SSH home, but I was greeted with a &#8216;Connection Refused&#8217; message in my terminal. Thinking that it was odd, I tried to RDP back to the Windows Server at my house, but again the connection would not start. Checking on the sites that I normally run from my server, I began to get nervous when none of them would load.
<!--more-->

As a last ditch effort I tried to FTP back to the server to see if there was anything I could get to, but again I was greeted by an error message that told me a connection was not going to happen.

The only thing I could actually connect to was my Wireless Camera that I use to monitor the baby at night in her crib. This was the straw that broke my back and sent me into a full panic. This meant there was an issue with the ESX host at home.

## What The Heck Happened?

So it turns out that the Plex Server I had was running, and the ESX host itself was working fine. The ESX host was a SuperMicro server that had a RAID controller that does not play nice with ESX. Now I know a normally person would never allow this to happen, or would take steps to ensure that in the event of a disaster, they had a plan. Backups you say? Ha! No need for those said I.

The server was configured as such:

Disk1: ESX Boot Drive
  
Disk2: Web Server and Windows Server
  
Disk3: Plex Server
  
Disk4: Not Used

When I finally fired up the VMWare, I found that Disk 2 had failed, and it failed hard. I pulled the drive and ran some diagnostics on it, or well I tried to at least, but as soon as I plugged the drive in, it began to click like a son of a gun. So I knew right there I was in deep.

## What I Did

In a frantic rush I tried to figure out what I had backups of, if anything. I know I just said I didn&#8217;t have them in the previous section, but I did have two of the seven websites I run, luckily I was working on them to revamp them.

I took a Gigabyte Brix box I had laying around that I was going to use for an arcade box, and I quickly threw a windows image up on it, and installed WAMP. That&#8217;s right, as of right now my webserver is running on WAMP.

## Future Plans

If possible I am going to build a new rig for the family machine in around five months. If I can do this I will be buying a PCI RAID Card for my current rig, where I will then fill it back up with drives and turn it back into an ESX Host. One can only hope that this new server will last as long as I need it to.
