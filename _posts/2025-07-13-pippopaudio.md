---
layout: post
author: Cameron McBurney
tags: [pippopaudio]
---

# PipPop (3D FPS Shooter) 
## Game Audio Implementation 

As part of my own demo learning project, I was looking for efficient ways to link my existing C++ code with Metasounds and Blueprint audio implementation.

I considered trying to use event dispatchers initially but found that it seemed it was more efficient to declare it as a delegate that could be referenced quickly in memory when needed.

Given that all players would be firing guns multiple times throughout the game, it seemed using delegates was the more efficient route.

A benefit too is the functionality to call multicast delegates to declare the sound needed to be played across multiple player instances.

```
DECLARE_DYNAMIC_MULTICAST_DELEGATE(FUpdateAmmoDelegate);

UPROPERTY(BlueprintAssignable)
	FUpdateAmmoDelegate UpdateAmmoDelegate;
```

I found the method Broadcast within the delegates class to communicate the event when bound.

The broadcast was called each time the gun was successfully fired to communicate the need for sound and visual effects.

```
void ABaseGun::FireGun_Implementation()
{   
	// ...
	Ammo--;
	UpdateAmmoDelegate.Broadcast();
}
```

The logic within the UI display then checks if a referenced to a player's gun with the binding exists and if not binds it as a listener.

```
// ...
PlayerGun->UpdateAmmoDelegate.AddDynamic(this, &UUIAmmo::UpdateAmmoDisplay);
CurrentBoundGun = PlayerGun;

// ...
if (BoundGun)
{
	BoundGun->UpdateAmmoDelegate.RemoveDynamic(this, &UUIAmmo::UpdateAmmoDisplay);
}
```

This event was also bound in blueprints to a customer event calling an audio component.

On the broadcast of the event the audio component is called containing the following metasound: 

<iframe src="https://blueprintue.com/render/5m2i-cph/" scrolling="no" allowfullscreen></iframe>

A random gun fire sound is selected from an array and is given 3 random parameter adjustments (start time, pitch and volume) to create some variation in the sound.

The metasound and content are assigned to a class 'GunSounds' in which the apply ambient volums bool is checked.

When played in the world there are audio gameplay volumes set with various reverb components attached to reflect the environment the firing sound is played in.  












