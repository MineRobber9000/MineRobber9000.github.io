---
layout: post
title: OpenComputers Tutorial: Custom OS
---

This tutorial was written by me, MineRobber9000, during my attempts at a custom OS for OpenComputers.

## Part 1: Research

First, I looked to the wiki. [This page](http://ocdoc.cil.li/tutorial:custom_oses) talks about the limitations of custom OS init files.

Sadly, it doesn't say much on the topic of actually creating one, other than how to get it set up. (init.lua on a filesystem)

Reaching out to the lovely members of the OC channel on Esper, the only person to respond to me told me quite curtly to look up examples on the forum.

And sadly, I didn't find any. That's why this tutorial exists.

## Part 2: Testing

The first test is an attempt to make sure that the machine can load off our storage medium.

```lua
local gpu = component.proxy(component.list("gpu")())
gpu.set(1,1,"It works!")
while true do
	computer.pullSignal()
end
```

Let's break this down:

The first line defines `gpu` as the first GPU. See the linked wiki page above for why that works.

The second line writes "It works!" at position 1,1.

When the init.lua returns, the computer shuts off. This is where all OSes need a main loop to prevent it from prematurely returning.
Our main loop is rediculously compact. That's because it does literally nothing. It waits for a signal and doesn't act on it.

When you try running it, (assuming you made no mistake) it should display "It works!" in the top left corner of the screen.

## Part 3: Doing something!

Now let's make our OS do something. It doesn't need to really be anything, it just has to do something, anything.

How about display the name of the latest signal?

Let's modify our code from earlier:

```lua
local gpu = component.proxy(component.list("gpu")())
gpu.set(1,1,"It works!")
while true do
	local sig = {computer.pullSignal()}
	gpu.set(1,2,"                                             ")
	gpu.set(1,2,sig[1])
end
```

The only thing we've changed is our main loop. The first line pulls a signal, the second line clears the 2nd line on-screen, and the third
line puts the name of the signal on-screen.

## Part 4: Doing something productive!

(TBD I need sleep)
