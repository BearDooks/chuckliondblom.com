---
title: "Dev Diary First Run"
date: 2018-04-24 11:05:00 -05:00
categories: [dev diary]
tags: [godot, dev diary, ai app, git, github, lessons learned, trello, slack]
author: chuck lindblom
sharing: true
show_author_profile: true
---

# Dev Diary 1

Over the past few months I have been working on a new app/gaem idea with a guy from work using the Godot Engine. It has been long process and I wanted to document some of the things I have already learned and what I would change if I could go back and tell the old me about it.

# Git

Git is your friend, but it can also be your worst nightmare at the same time. Git is a super powerful tool for managing work, collaborating with someone else, and storing old versions of code so you can review if needed. Overall, I have been super happy with it, moving over from SVN, but I have also had an extremely hard time with it. 
<figure>
	<a href="/images/bitbucket_commits.jpg"><img src="/images/bitbucket_commits.jpg" alt=""></a>
</figure>
<!--more-->
One of the biggest issues we have had is when two people are working on the same file. Normally not an issue, but when there is a few changes made to a .tscn file in Godot, you don't always see the changes. These files are basically the scenes that you are working on, and you never really go into the code side of things. That is where GDScript comes in. A few times though I have had to go into these .tscn files and fix the merge issues that we have.

Finding the right tool is also a pain. Since most of the code we are working on is hosted in BitBucket, we used SourceTree since it is made by the same company. We soon saw that this is going be an issue since we didn't really know how to use the application, and it was overly complicated. In the end I had to switch to GitHub Desktop because it was simple to use. My partner picked up TortoiseGit, which is basically an SVN client converted to Git.

# Trello

Trello has become my go to for Kanban type lists. Granted I don't use it as much as I should, and we are still trying to figure out what the cards should look like, it helps organize thoughts and ideas that you don't want to lose. It also helps me see who is working on what so we don't end up working on the same thing (Which happens more than I would like). 

We took the idea of the columns and adapted it to meet our needs. We have one that is just for cards of things we need to discuss, or new ideas we might want to turn into something. Labels have also been super important to this product. I can tag things as a bug, misc, v0.1 release, or a nice to have item. It allows me to quickly see what is going on, and what I need to tackle first. This method stops me from working on things that would be nice to have, vs things that are broken.
<figure>
	<a href="/images/trello_cards.jpg"><img src="/images/trello_cards.jpg" alt=""></a>
</figure>

# Slack

Slack was first introduced to me by a development team at my day job. The first time I saw it I didn’t really care for it, I thought it was just another app that allows you to chat with people and share stupid pictures. I then started using it more myself to see what it was capable of, and how it might benefit me as I worked on projects. 

Slack is great at linking into other applications. The best example I have for this is Git. When someone on the team posts a new build into BitBucket, Slack sends a message to let me know and includes the notes. When cards are worked on or moved in Trello, Slack lets me know. It has become less of a chat application for me, and more of a high-level view into how the project is progressing and what has been done. Yes, I still use it to chat with the team, and share stupid pictures, but we can also post things like portions of code. Slack is smart enough to show the code in the correct format with colors so it is easier for the user to read.
<figure>
	<a href="/images/slack_git.jpg"><img src="/images/slack_git.jpg" alt=""></a>
</figure>
<figure>
	<a href="/images/slack_code.jpg"><img src="/images/slack_code.jpg" alt=""></a>
</figure>

# Conclusion

If I could go back in time and tell my old self anything about this project, it would be to not give up. This project is nowhere near complete, but I am already feeling let down by it. I know it can be great if I really put the effort into it, but I get frustrated when working on core mechanics when I would rather be working on the flashy side of things.

I would remind myself, that every once and a while I will have this aha moment, and come up with some really great code that will make the game open up a bit more and show me what the end product will be like. It’s important to just stick with it and stay true to the process.
