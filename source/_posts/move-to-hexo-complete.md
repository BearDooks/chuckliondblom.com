---
title: Move to Hexo Complete
date: 2024-04-19 22:49:10
categories: [Site News]
tags: [hexo, website, code]
---

## The move to Hexo is now complete

It took a little longer than I would have liked, but there was a lot of changes that needed to be made to get the posts to work from Jekyll. Most of it revolved around how Hexo handles images. I also had to clean up a lot of the tags and the categories on posts since they did not line up with what I wanted. Lastly I removed some old posts, and removed some links to things that don't work anymore, mainly my X (The Old Twitter) account.

<!-- more -->

## Hexo and Images

Hexo has a really cool way of handling images for posts. In the `_config.yml` file there is a line `post_asset_folder: false`. Once you set this to true, anytime you make a new post with the `hexo new` command, it also creates a folder with the same name as the post itself. All you need to do now is store any images for that post in said folder, and then reference them in the post using the following syntax `{% asset_img <ImageName> <AltText> %}`

As you can guess, when you have a lot of posts from an old website, moving all the images into these new folders, and then trying to edit all the markdown to reference the new syntax can take a while.

## Google Analytics

Google Analytics was probably the most annoying thing to move over from jekyll. To be honest, there was not an easy way that made sense. There are plenty of guides, and most of them work for other people, but I think those people are not using Github pages like I am and using Github actions to deploy the site. Normally if I ran the command `hexo generate` I could see all the Google Analytics code in my site, but when I deployed it via Github actions, no such luck. To fix this I had to place the following line in my `_config.yml` under the theme. (I have obviously changed my Google number so no one steals it)

{% codeblock %}
theme_config:
  google_analytics: G-XXXXXXXXXX
{% endcodeblock %}

## Where to next?

I want to start writing on here more. I find it easy and a little more user friendly than Jekyll was. The problem is I forgot to do it, or I have nothing important or good to write about. The other thing I want to add back in are ads. I know that is a hot button topic for a lot of people. I hate going to a site and being drowned in ad after ad that take up the entire screen. I always tried to keep the ads to a miniumum, and to be honest I have never really made any money that has been sent to me buy the ads. If I do get them working I am sure I could make that a post.

Until then, stay safe, have fun.