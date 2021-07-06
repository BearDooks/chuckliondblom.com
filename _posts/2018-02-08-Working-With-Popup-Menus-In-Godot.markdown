---
title: "Working With Popup Menus In Godot"
date: 2018-02-08 11:20:00 -05:00
categories: [guide, godot]
tags: [godot, godot 3.0, godot 3, popup menu, programming, guide]
author: chuck lindblom
sharing: true
show_author_profile: true
---

# Popup Menus In Godot
Last night I started work on a test project, and I wanted to start using popup menus correctly. I had implemented them in my game 'LightsOut!' but I did not realize that I was using them incorrectly. As it turns out this Node is super helpful and pretty easy to use if you now what you are doing.

## Working With The Popup Menu Node
Please note this is a super simple popup menu with three items. Each selection calls a function via a signal that passes the ID of the selection and allows you to go from there.

<figure>
	<a href="/images/GodotPopupNodes.png"><img src="/images/GodotPopupNodes.png" alt=""></a>
</figure>
<!--more-->
{% highlight python %}
extends Node

# Internal Connections
onready var popup = self.get_node("PopupMenu")
func _ready():
	_setupPopupMenu()

func _setupPopupMenu():
	# This function will clear the popup menu and then add the items to it
	popup.clear()
	popup.add_item("Item1", 1)
	popup.add_item("Item2", 2)
	popup.add_item("Item3", 3)
	popup.set_position(Vector2(100,100))
	popup.connect("id_pressed", self, "_popupMenuChoice")
	popup.show()

func _popupMenuChoice(ID):
	# This function takes the ID of the chocie you made and runs something
	if ID == 1:
		print("You picked Item1")
	elif ID == 2:
		print("You picked Item2")
	elif ID == 3:
		print("You picked Item3")
{% endhighlight %}

This will create a menu on the screen that you can use. 

{% highlight python %}
	popup.connect("id_pressed", self, "_popupMenuChoice")
{% endhighlight %}

This is the line that connects the signal to another function when you select something. Note that this is how it works in Godot 3.0. The commands in 2.1.4 are different. While working on this last night there are a ton of cool things yuo can also add to the menu such as sub-menus, separators, and buttons.

I highly suggest checking out the official documentation and trying it out for yourself.
