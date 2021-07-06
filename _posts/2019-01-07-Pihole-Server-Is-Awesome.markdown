---
title: "Pi-hole Server is Awesome!"
date: 2019-01-07 11:20:00 -05:00
categories: [review]
tags: [review, docker, linux, pihole, DNS]
author: chuck lindblom
sharing: true
show_author_profile: true
---

A friend recently asked me if I knew of a good way to block ads on his home network. At the time I didn't, but I started to dig into it more, since this is something I have also been curious about. Ads have become more and more annoying and intrusive to our lives. The people that use them for the right reasons get a bad rap, by the people who hijack browsers with it. I needed to find something, enter Pi-hole.

<a href="https://pi-hole.net/">Pi-hole's Website</a>

<figure>
	<a href="/images/pihole_logo.png"><img src="/images/pihole_logo.png" alt=""></a>
</figure>
<!--more-->

## My Pi-hole Setup
I have a small linux server running in my basement. Nothing special, just a Gigabyte Brix box, 120GB SSD, 4GB RAM, and a small Intel CPU. It is enough for me to test what I need to in the house before I either move it to a VPS or find a service to run it for me. The server is currently running <a href="https://www.docker.com/">Docker</a> so I can run containers of apps I want to test. To manage these containers I have <a href="https://www.portainer.io/">Portainer</a> installed so I have a nice GUI of everything. I am the first to admit I am not the best at these things.

From there I followed <a href="https://github.com/pi-hole/docker-pi-hole">this guide</a> on how to get Pi-hole running inside of docker. I have to admit it was very easy to get it going, for lack of a better phrase, it just works. I did have a small issue I needed to fix with the admin password. Docker creates a random on for you, and they tell you if you want to change it run the following command. 

{% highlight bash %}
pihole -a -p
{% endhighlight %}

When I run this command, it would return an error that the server didn't understand pihole. I figured this was an issue since it was running inside of docker in it's own little world. Doing a little looking around I finally found someone online with the same issue as me, and instead of making me feel dumb, they just elain how to fix it.

{% highlight bash %}
docker exec -it pihole /bin/bash
# create an password protection for your pihole web interface
pihole -a -p somepasswordhere
# You can also remove the password by not passing an argument.
pihole -a -p
{% endhighlight %}

Credit to Nico Maas <a href="https://www.nico-maas.de/?p=1525">Nico's Link</a>

## Stats
To start I have only changed one of the machines in my network to use Pi-hole, because I want to see how it works before I go all in. Its not that I have a lot of devices in my house, by with Smart TVs, Phones, Tablets, Etc I don't want to break anything and have to explain to the family what I did. My 5 year old daughter will be pissed if she can't watch her shows on her iPad. (Don't judge me). After running the server for a bit and doing some gaming and web browsing, I found that Pi-hole just works. While my wife was using my rig, I had their admin panel up on my phone, and I could see in real time what it was doing.
<a href="/images/pihole_stats.png"><img src="/images/pihole_stats.png" alt=""></a>

## Final Report
I think this is 100% something I am going to be looking into and running in my house. It might take some tweaking to get everything just right, but from what I have seen so far it is good. Nothing really broke, and my wife had no idea it was even running. I plan to do a follow-up after I have this fully integrated into my network so I can post some better stats.
