---
layout: post
author: Cameron McBurney
tags: [phantasmagoria]
---

## PHANTASMAGORIA
# 3D Turn Based RPG 

![image](./images/COVER_Phantasmagoria.png)

*Phantasmagoria is a solo project and a narrative driven RPG inspired by English folklore.*

Features:  
Turn Based Interactive Combat - Classic turn based combat giving you time to plan your next strike, follow button sequences to deal extra damage or defend and stack multipliers.

Deep dialogue systems - Think careful about how you respond to NPCs, it could be your only chance to obtain unique items.




**Riddle puzzle system**

As part of the overworld gameplay loop, I wanted to incoperate puzzles to gain access to areas or additional loot. 
I wanted a puzzle which would challenge the player to think but didn't require complex timed input sequence, a player inputted answer was the perfect fit.

{% raw %}
<iframe src="https://www.youtube.com/embed/6UFsydybUDI" width="100%" height="600" scrolling="no" allowfullscreen></iframe>
{% endraw %}

The riddle puzzle uses a widget overlay with an invisible text box to dynamically take player keyboard input and pass it to the puzzle actor.
The puzzle actor has 5 invisible cubes which can be altered based on the last inputted letter in the text box.
If the player tries to input text past the maximum amount, an error sound plays and no change is taken.

{% raw %}
<iframe src="https://blueprintue.com/render/ma4ilg6m/" width="100%" height="600" scrolling="no" allowfullscreen></iframe>
{% endraw %}

The actor takes the last inputted letter each time the text is updated, finds the paired textures using a map and sets this to the invisible block in sequence.
Each letter is added to a queue which determines whether a letter has been added or removed then fades in or out the letter in sequence on a looping timer.
If the queue is empty, the timer stops looping and resets.
If the wrong answer is inputted, the riddle clears itself in reverse and the player exits the focused camera from the widget/actor.
If the correct answer is inputted, the lights in the scene will turn on.

{% raw %}
<iframe src="https://blueprintue.com/render/57nom2rn/" width="100%" height="600" scrolling="no" allowfullscreen></iframe>
{% endraw %}

***Future planned features***

On screen keyboard for controller players and to reflect player keyboard inputs
Parameterised final string length for reuse.
Add a resuable function for creating and setting the dynamic material instances.

