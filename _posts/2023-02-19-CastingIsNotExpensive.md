---
layout: post
title: Understanding why casts can be expensive
---

# Table of Contents
* [Introduction](#introduction)
+ [Hard References](#hard-references)
    + [The complications of hard references](#the-complications-of-hard-references)
    + [Size Map](#size-map)
    + [Creating hard references](#creating-hard-references)
    + [Hard reference cost conclusion](#hard-reference-cost-conclusion)



<a name="introduction"></a>
## Introduction 

Almost every day on Youtube, Reddit, Discord, and many more social media, I see people spitting out the infamous words “Casting is expensive”, well yes, but no, and I’m gonna tell you why.

But first we have to start on another topic to understand why casting **can** be expensive.

<a name="hard-references"></a>
## Hard References

Hard reference is the number one reason why casts can be expensive, but they are a one time cost.

A hard reference happens when an asset depends upon another asset. For example, in the Game Mode class you have assigned your Character/PlayerController/PlayerState, those are all hard references to those classes and will get loaded when Game Mode is laoding.

For example, when you start your game, the game mode will get loaded. It will also load the assigned Character/PlayerController/PlayerState and whatever hard references those classes have, then keep them loaded throughout the whole play session because the Game Mode is always active and holds a hard reference to those classes.

### The complications of hard references

Now you might understand why hard references can have severe complications on the project.

Large chains of hard references does not only affect the game itself, but the development cycle aswell and will slow down Blueprint compile times, editor startup time, and packaging.

{: .box-note}
**Warning:** Hard reference is not directly linked to slower loading, the size map will help you know if you have just created an expensive hard reference.

<a name="size-map"></a>
### Size Map

The size map is an excellent tool in Unreal Engine, which you can see the size of an asset and its hard references.

Just right click on any asset and click on **""Size Map"**, and you'll get this window:

![SizeMap](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_05.JPG)

Here you can see all the assets that will get loaded along with the loading of this asset. I've seen in some projects where an asset size map is up to 2gb, which will slow down the loading times.

Let's take the character again as an example. If the character class that is assigned in the Game Mode has a size map of 3GB, all those 3GB will be loaded at all times while your game is playing.

<a name="creating-hard-references"></a>
### Creating hard references

#### Hard references for variables

When you make a class variable, you'll create a hard reference to that class, and when you assign a value to it, you'll also create a hard reference to that assigned class.

![HardReferenceVariable](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_01.JPG)

For example, if you have a generic Actor class variable and assign your custom actor class **"BP_IronOre"**, you'll create a hard reference to **"BP_IronOre"**.

#### Hard references on function nodes

The same goes for nodes. When you assign a class to a node, you'll also create a hard reference to that class.

![HardReferenceNode](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_03.JPG)

Also the moment you create a cast node, you create a hard reference to the class you want to cast to.

![HardReferenceCast](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_04.JPG)

<a name="hard-reference-cost-conclusion"></a>
### Hard reference cost conclusion

A variable that has a hard reference to a class, has the same cost as a cast that points to the same class.

## Avoid hard reference

**In progress..**
