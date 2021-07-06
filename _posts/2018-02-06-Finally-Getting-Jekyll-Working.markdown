---
title: "Finally Getting Jekyll Working"
date: 2018-02-06 15:20:00 -05:00
categories: [website, jekyll]
tags: [jekyll, updates, git, code, source tree, hostgator, web hosting, aws]
author: chuck lindblom
sharing: true
show_author_profile: true
---

It took me years to see that paying over $100 for web hosting for a few Wordpress sites and some personal junk was not really working for me anymore. I don't really make any money off of the small ads I have on my site (Thanks for not blocking them if you see them), and I never really asked people for money when I made them a website. I used HostGator for a few years, and to be honest I am glad I am moving away from them. The price was way to high for personal use, and the support was lacking.

I can remember a time when my sites where being turned off for no reason. I got an email from a third party called SiteLock, that told me my sites had been scanned and there was malware and bad files. The worst part was they could never really tell me what files, how they got there, or who was accessing my account. It is very hard for a person who works in IT to trust a company that doesn't provide logs of access to you. There were other times when the site was be shut down for no reason at all, and by the time I finally got through to support, the site was back, and they claimed it had been working the entire time. The screenshots that I had taken must have been fake right? Yeah.
<!--more-->
Amazon Web Services was the first answer that I needed. I converted what sites I could into static sites, no more need for Wordpress. Once I had that done it was easy enough to spin those sites up on some Cloudfront services with a S3 backend, and move DNS over to Route53. The best part is since the sites are so small and generate next to no traffic, I only pay 51 cents per site, per month. Comes out to a bank account breaking $1.02 a month currently. 

<figure>
	<a href="/images/jekyll.png"><img src="/images/jekyll.png" alt=""></a>
</figure>

The bigger nut to break was my personal site. I had been running it in Wordpress for years. I had hosted my own servers, I had lost all my data, and I had built it all back up again. Wordpress to me was a safe place, easy to use, and allowed me to write without issue. It took care of the hard parts for me, I didn't have to code everything by hand. Jekyll was the answer to that. At first I had to get used to the fact there is no real 'Admin Panel' that I can log into and easily write, but once you learn some git, or use an application like SourceTree you will be fine. What really helped was a plug-in I could install on Wordpress to help convert what I had over into a Jekyll format. It only took a few minor edits for each post to make them all uniform and turn it all into this site that I am currently running. Jekyll takes these flat markdown files and turns them into pages and posts for me, so it makes life easy when I can type everything in notepad, or on my phone and upload it later.

It took some time but the site is really up and running now. I have small ads at the bottom of the posts to try and earn a little bit of cash (Currently as of today I have made $3.23 in my lifetime of runnings ads) and I am figuring the rest out. I make sure I have good backups so when I break things, or add a service that rewrites all my markdown files for me and breaks the site, I can restore back to a good time.

So here is to 2018. Lets hope this year I commit to really adding posts and content to this thing.
