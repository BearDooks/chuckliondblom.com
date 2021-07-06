---
title: "Website Revamp"
date: 2018-11-27 11:25:00 -05:00
categories: [website]
tags: [website, updates, jekyll, working on it]
author: chuck lindblom
sharing: true
show_author_profile: true
---

The site was in desperate need of an update. Every day GitHub was letting me know that there were errors and risks on the site and that Jekyll was not running the best version. I finally gave in and decided to try and get this thing working to the best of my limited ability.

# Jekyll not running correct version

This was a tough one for me since I really never had to update Jekyll before. I was able however to download Ruby and install the Jekyll Gem on my machine. I also cloned my repo locally so I could work on it. From the limited research I did I found all I should have to do is run the following command. ‘bundle update’
Seemed simple enough, but it did not work. Jekyll stayed at the version is was running on and I was lost. It took a while but more research helped me uncover the fact that in my gemfile I was telling github-pages to run on version 139. This was an issue since it would lock Jekyll into an older version.

# The Fix

The fix was a simple one. Start over. I know to some people this sounds a bit crazy but hear me out. I never really understood how all of this worked before (Really I still don’t get it 100% but I am getting there). The best way to learn is to start back at square one and try again. I was able to get the latest version of Jekyll running, and served on my local machine. I did have some issues getting it running on the GitHub-Pages side of things, but that is another write up for another day. I was able to clean up the file and then get a new theme running. It did however force me to go back into all the posts and make some edits, since I had hacked them up before to get things like pictures working.

# The Result

The result is this new and improved site. It looks better than it did before, and it seems easier to update in the future. I just need to be better at writing for it and making sure to give it the care it needs.
