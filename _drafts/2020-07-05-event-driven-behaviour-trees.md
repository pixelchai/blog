---
layout: post
title: Event-driven Behaviour Trees
---

Okay so I actually just created this blog because of this. I found out about something cool that I just _have_ to write about, but realised I don't have a blog (lol) so I hastilly slapped up the default Jekyll blog thing, opened up a text editor and let it flow. And honestly,... I wouldn't have it any other way.

<!-- Talk abuout lack of resources/implementations here -->

{% comment %}
I think I found out about MineRL through Twitter btw -- forgot who
{% endcomment %}

Recently, I found out about the MineRL Competition, a Machine Learning competition where the aim is to teach an agent to obtain diamonds in Minecraft. As a competition seeking to motivate interest in sample-efficient reinforcmenet learning, it forbids researchers from using domain knowledge in their approaches. This got me wondering, however, about how well a domain knowledge based bot could actually perform in Minecraft -- so I decided to try my hand at making one: MineBot. There's much more left to say about this particular project, but I'll leave it for another time.
Anyway it was thinking about how I should structure the AI for MineBot that lead me down this rabbit hole.

I approached the problem how I would approach designing something like a self-driving car. I knew immediately that I wanted three things:

1. For the AI to be heirarchical -- that feels reflective of how a human would think about things, after all.
2. For it to be event-driven -- I was already in an event-driven mindset because of the way I was interacting with Minecraft anyway.
3. For behaviours to be able to be interrupted and transition to different behaviours when necessary -- for example, if the agent is cutting down some wood but is suddenly jumped by a hostile mob in the game, cutting down the tree should be interrupted and the agent should switch to dealing with the mob.

You can actually find the notes I jotted down while I was initially thinking about this in [MineBot's github repo](https://github.com/pixelzerg/MineBot/commit/cb8eb3291cefdc45cc3fac55bdc75aee40e87181). "I'm sleepy I need to think more about this later" lol. I initially had a vague idea about using finite state machines, but I later also discovered behaviour trees.

## 'Classical' Behaviour Trees
I understand that modern implementations of behaviour trees do not always run every frame: I'll address these later. For now, though, let's stick with what I'll call 'classical' behaviour trees for a bit, and what exactly is the problem with them.

When I found out about behaviour trees I definitely thought they were pretty cool but traversing the entire tree every single tick didn't sit right with me at all. Not only from a computation overhead perspective but also, what if you wanted to do a more long-running task -- something that would likely take multiple ticks?

### Long-running Tasks
One solution to this might be to simply try to avoid such long-running tasks and instead break them up into smaller tasks instead. At first glance, this doesn't seem too bad, especially if you think about it as an opaque process like some do with Machine Learning: you take a set of features -> feed them into a model -> some magic happens -> it spits out an action to do (key press, mouse movement, no-op, whatever) and you repeat this every frame. Let's say for example we want the AI to move towards a specific target location. Rather than having a task which is to `move to the target location`, this approach would suggest segmenting the task such that we are left with simpler tasks such as `take a step towards the target location` instead.

To say:
they try to address it with 'running' state -- just confusing, reactive? If you just jump straight to a state
maybe some werid thing with layered

### Computation Overhead
Why exactly are we re-computing the outputs of so many nodes every single frame when we are pretty much certain that they are going to result in the same output?? In fact, for frames close to each other (with small amounts of time elapsed between them), you could even say that we _assume_ that they are going to result in the same/similar output in structuring the AI this way: if we have done a bunch of computation, realised we want to move towards tree, then step towards it on one frame, we _proabbly_ want to step towards the tree the next frame as well and so you could say that we are implicitly assuming that .
Yes, there are some cases where you suddenly want to do something else (like if you are interrupted by a hostile mob, to take the example I gave above). And while I agree that this sort of approach would ensure that the AI is reactive (assuming the computations are quick and doesn't lag everything out, which might be assuming too much, mind you, considering how large trees can get)

but this isn't supposed to be the majority.

### How These Are Adressed




This is fine for simple movement behaviour, but what 

which I'll leave for another time, but it was ultimately during working on that project and thinking about the structure of the AI 

Recently, I decided I wanted to try my hand at creating a bot for Minecraft that