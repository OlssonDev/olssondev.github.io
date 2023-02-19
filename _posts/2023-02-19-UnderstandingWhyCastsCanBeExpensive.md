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
    + [How to avoid expensive hard references](#how-to-avoid-expensive-hard-references)
* [Conclusion](#conclusion)

<a name="introduction"></a>
## Introduction 

Almost every day on Youtube, Reddit, Discord, and many more social media, I see people saying, “Casting is expensive. Use interfaces!”, well yes, but no, it's a bit more complicated. I’m going to tell you why.

But first, we have to start on another topic to understand why casting **can** be expensive.

<a name="hard-references"></a>
## Hard References

A hard reference happens when an asset depends upon another asset. Hard reference is the number one reason casts can be expensive, but they are a one-time cost.  

In the **Game Mode** class, you have assigned your **Character**, **Player Controller**, **Game State**, and more. Those are all hard references to those classes and will get loaded when **Game Mode** is loading.

For example, the **Game Mode** will get loaded when you start your game. It will also load the assigned classes I mentioned above. Whatever hard references those classes have will be kept loaded throughout the whole play session because the **Game Mode** is always loaded and holds a hard reference to those classes.

### The complications of hard references

Now you might understand why hard references can have severe complications on the project.

Large chains of hard references does not only affect the game itself, but the development cycle aswell and will slow down Blueprint compile times, editor startup time, and packaging.

{: .box-note}
**Note:** Hard reference is not directly linked to longer load times, the size map will help you to know if you have just created an expensive hard reference.

<a name="size-map"></a>
### Size Map

The size map is an excellent tool in Unreal Engine, which you can see the size of an asset and its hard references.

Just right click on any asset and click on **""Size Map"**, and you'll get this window:

![SizeMap](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_05.JPG)

Here you can see all the assets that will get loaded with this asset. I've seen in some projects where an asset size map is up to 2GB, which will increase the load times.

Let's retake the character as an example. If the **Character** class assigned in the **Game Mode** has a size map of 3GB, all those 3GB will be loaded at all times while your game is playing.

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

A variable or a node that has a hard reference to a class, has the same cost as a cast node that points to the same class.

<a name="how-to-avoid-expensive-hard-references"></a>
### How to avoid expensive hard references

You can avoid hard references in many different ways, and sometimes they are needed, and no reason to avoid them (Like a reference to the character's mesh).

I'll go over a few ways you can reduce the number of hard references.

#### Soft References

You can use soft references for any object-type variables. Soft references will not be loaded when the asset they are referenced by is loaded.

![SoftReferenceVariable](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_06.JPG)

```javascript
//How you declare them in C++

UPROPERTY(EditDefaultsOnly)
TSoftObjectPtr<UMyClass> MySoftObjectPointer;

UPROPERTY(EditDefaultsOnly)
TSoftClassPtr<UMyClass> MySoftClassPointer;
``` 

To load soft references, you have to load them yourself using these nodes:

![AsyncLoadNodes](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_07.JPG)

```javascript
//How to load soft pointers in C++

//Load using a weak lambda as callback
UAssetManager::GetStreamableManager().RequestAsyncLoad(MySoftClassPointer.ToSoftObjectPath(), FStreamableDelegate::CreateWeakLambda(this, [this]
{
    //On loaded
}));

//Load using a function as callback
UAssetManager::GetStreamableManager().RequestAsyncLoad(MySoftClassPointer.ToSoftObjectPath(), FStreamableDelegate::CreateUObject(this, &ThisClass::OnSoftPointerLoaded));
```

However, the class will unload eventually, if they're not kept as a hard reference after they've been loaded.

For example, I load my static mesh and set it on my **Static Mesh Component**, which holds a hard reference to the static mesh it displays so it won't be unloaded.

![HardReferenceUnload](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_08.JPG)

{: .box-note}
**Note:** A great use case for soft pointers is to store an equipable item's thumbnail/actor class in soft references.

##### Check class without hard reference

Soft references can also be used when you want to check if an object is of a certain class without creating a hard reference to that class:

![OverlapCheckClass](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_12.JPG)
![CheckClassFunction](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_13.JPG)

The function tries to resolve the soft reference and check it towards the other class. If it fails to resolve the class, it can't be that class because it's not loaded.

#### Casting

As we've already settled, casts create a hard reference to the class you want to cast to. 

However, if you cast to a C++ class like Character, Pawn, Actor, or your custom C++ classes, that reference has no overhead since all C++ classes are always loaded into memory.

If you need to cast to a Blueprint class, limit your casts to parent classes that should only contain variables, functions, and no references to large assets.

#### Interfaces

Interfaces enable you to communicate with other classes without creating a hard reference unless any of the interface functions have parameters that point to a UAsset.

{: .box-note}
**Note:** Interfaces **don't** replace casts!

Interfaces are great for interaction systems or getting a certain component from an Actor to use in a system (Gameplay Ability System (GAS) does this). 

Use interfaces when you want the same call to multiple classes, don't use interfaces if you need one implementation of the function, just cast it. It's easier to read and debug.

A bad use case for interfaces (Single implementations of interface functions make no sense. Cast to Game State and add the point):

![UselessInterfaceCall](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_11.JPG)

A good use case for interfaces (Multiple classes might need to be interactable, and this is where interfaces shine):

![GreatInterfaceCall](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/Casting/Image_10.JPG)

## Conclusion

Casting is pretty much a free operation; performance-wise, the only thing cast nodes **can** contribute is longer loading times (due to a large size map) when the Blueprint the cast node is in is getting loaded in runtime and the editor.
