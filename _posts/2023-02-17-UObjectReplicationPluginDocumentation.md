---
layout: post
title: UObject Replication Plugin Documentation
toc: true
---

[Marketplace Page](https://www.unrealengine.com/marketplace/en-US/product/34834b25f9b94125a015342fb3fae218)

[Support](https://discord.gg/NenE6EptdD)

Supported Unreal Engine Versions: 4.27 - 5.1

# Table of Contents
1. [Plugin Overview](#Plugin-Overview)
2. [Create a Replicated UObject](#Create-a-Replicated-UObject)

## Plugin Overview <a name="plugin overview"></a>

In Unreal Engine, two main classes are used for replication, Actors and Actor Components. With just a simple checkbox away, you’re up and running with replicating those classes.

But that is not the case with UObjects. They require C++ to set up replication, which this plugin will help you with.

{: .box-note}
**Note:** The documentation will not cover how multiplayer in Unreal Engine works, just how UObject replication works at a high level. The documentation expects you to have some knowledge about replication already. If you’re new to networking, here is an excellent resource about multiplayer in Unreal Engine: [UE Network Compendium](https://cedric-neukirchen.net/Downloads/Compendium/UE4_Network_Compendium_by_Cedric_eXi_Neukirchen.pdf).


## Create a Replicated UObject

Setting up a new custom Replicated UObject is very easy and intuitive.

![CreateAReplicatedUObject](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/CreateAReplicatedUObject.png)

Right-click anywhere in your content browser, find the **“UObject Replication”** category and click on **“Replicated UObject”** to create your new Replicated UObject class.

## Setup your custom Replicated UObject

The new Replicated UObject is already replicated by default.

![SetToReplicated](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/SetToReplicated.png)

You can turn off replication for the UObject by simply choosing **“Do Not Replicate”** in the enum instead of **“Replicates.”**

![SetToNotReplicate](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/SetToNotReplicate.png)

That’s it for the Replicated UObject. Your Replicated UObject now supports any multiplayer features as any Actor/Actor Component would do, like sending RPCs and replicating variables. 

Now we just need to register it to a **UObject Replication Manager** in an Actor.

## UObject Replication Manager

There is one caveat with replicating UObjects. You need to replicate them through an Actor and their **Actor Channel**. At a high-level Actor, Channels are used to send replicated data over the network, like RPCs and variables. 

We will replicate our UObjects the same way that Actor Components are replicated. 

And that’s where our **UObject Replication Manager** comes in. You can put it on any Actor, and it’ll replicate the registered UObjects through the owning Actor’s Actor Channel.

## Add a UObject Replication Manager

To add a UObject Replication Manager to your Actor. Simply add it to your Actor as any other component in Unreal Engine, and you’re set.

![AddReplicationManager](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/AddReplicationManager.png)

## Register UObjects for replication

With your actor's **UObject Replication Manager** setup, you can now register your first UObject for replication.

![RegisterReplicatedUObjectNode](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/RegisterReplicatedUObjectNode.png)

The node seen above registers **Replicated UObjects** for replication. Very important to note that only **Replicated UObjects** will work to register, not regular UObjects.

![ConstructAndRegisterUObject](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/ConstructAndRegisterUObject.png)

This is the most common way to create Replicated UObjects with the plugin.

![ConstructReplicatedUObject](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/ConstructReplicatedUObject.png)

To register a Replicated UObject you need first to construct one. Right-click in the graph, search for **Construct Object From Class** and then choose the class of the Replicated UObject you created earlier.

Right-click on **Return Value** and promote it to a variable like in the image above, and set the newly created variable to Replicated or RepNotify (depending on your replication needs).

![RegisterReplicatedUObject](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/RegisterReplicatedUObject.png)

And simply connect the variable to the Register Replicated Object node from the Object Replication Manager you added earlier to the Actor. And that’s it. Your UObject will now be replicating.

{: .box-note}
**Note:** Make sure you construct and register the Replicated UObject on the server only. The Replicated UObject will get created on the clients automatically. Check that the Actor that the UObject Replication Manager is on, is replicating. 

## Replicating Arrays

![ReplicateArrayOfUObjects](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/ReplicatingArray.png)

Replicating an array of Replicated UObjects is the same procedure, but you add the Replicated UObject to the replicated array and register it. Execution order doesn’t matter.

## Unregister UObjects from replication

![UnregisterReplicatedUObject](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/UnregisterReplicatedUObject.png)

Suppose you want to stop replicating your Replicated UObject. Add an **Unregister Replicated Object** node from the Object Replication Manager, and plug your replicated variable of the Replicated UObject into it. 

If you want to destroy the **Replicated UObject** as you’re unregistering it, tick the Destroy Replicated UObject, and it will get marked as garbage. It will eventually get picked up by the garbage collector.

![DestroyReplicatedUObject](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/DestroyReplicatedUObject.png)

You can manually destroy the Replicated UObject by using **Destroy Replicated UObject** and it should only be called from the server. This will also unregister the Replicated UObject from being replicated.

## Custom Object Replication Managers

Custom Object Replication Managers is where this plugin shines. You can create modular systems using Replicated UObjects as the system's foundation. 

In [Lyra](https://dev.epicgames.com/community/learning/paths/Z4/lyra-starter-game), each gun in an inventory slot is a replicated UObject. When the player picks up a gun in Lyra, the gun they see in their inventory is a replicated UObject, and it’s responsible for managing the players’ ammunition, abilities, static mesh to spawn, inventory appearance (weapon icon et.c.), and much more!

Usually, ability systems make great use of replicated UObjects for their abilities. One of the ability systems that replicate abilities with UObjects is Unreal Engine's own [Gameplay Ability System](https://docs.unrealengine.com/5.0/en-US/gameplay-ability-system-for-unreal-engine/), which they use for Fortnite.

## Make Custom Object Replication Managers

![MakeReplicationManager](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/MakeCustomReplicationManager.png)

To make a custom Object Replication Manager is as easy as creating Replicated UObjects. Right-click anywhere in your content browser, find the  **“UObject Replication”** category and click on **“UObject Replication Manager”** to create your new UObject Replication Manager class.

## Setup your new UObject Replication Manager

No more setup is required. The UObject Replication Manager is replicated by default.

![ReplicationManagerNodes](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/ReplicationManagerNodes.png)

The functions from earlier are now callable in your custom UObject Replication Manager class. You can now start making modular systems like inventories, to add on any replicated Actor.

## Common Issues

#### My Replicated UObjects are not replicating

Make sure that the Actor you’re replicating from is set to **Replicates**, the UObject Replication Manager component is set to **Component Replicates**, and your variable/array is set to **Replicate/RepNotify**, and that you create/destroy Replicated UObjects on the **server**.

#### My Replicated UObjects don’t get destroyed

Make sure you ONLY destroy Replicated UObjects on the server.

#### I can’t see the UObject Replication category in the content browser

Make sure the plugin is installed on the correct engine version, and the plugin is set to be enabled.

#### My replicated UObjects are replicating slowly

Check the Actor with the UObject Replication Manager that the **Net Update Frequency** is reasonable. The default for Actors is 100.



