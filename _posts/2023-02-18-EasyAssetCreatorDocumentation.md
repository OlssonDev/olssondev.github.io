---
layout: post
title: Easy Asset Creator Documentation
---

# Table of Contents
* [Plugin overview](#plugin-overview)
+ [Asset Action](#asset-action)
    + [Create an Asset Action](#create-an-asset-action)
    + [Setting up your Asset Action](#setting-up-your-asset-action)
        + [Sub-category](#sub-category)
* [Asset Factory](#asset-factory)
    + [Create an Asset Factory](#create-an-asset-factory)
	+ [Setting up your Asset Factory](#setting-up-your-asset-factory)
* [Asset appearance](#asset-appearance)
    + [Asset name & tooltip](#asset-name-tooltip)
	+ [Asset color](#asset-color)
+ [Asset Action Fragments](#asset-action-fragments)
    + [Add to Place Actors menu](#add-to-place-actors-menu)
    + [Add Content Browser drag drop support](#add-content-browser-drag-drop-support)
* [Deleting assets](#deleting-assets)
+ [Common issues](#common-issues)
    + [My class won't update its name in the menus](#my-class-wont-update-its-name-in-the-menus)
    + [My class doesn't show up in the create asset menu](#my-class-doesnt-show-up-in-create-asset-menu)


<a name="plugin-overview"></a>
## Plugin overview 

Making editor tools for creating and placing assets is a tedious and time consuming process, and usually requires C++ to set up. Easy Asset Creator makes it easy to create tools for your assets, and all of it can be managed inside the editor with no requirements for an editor restart.

<a name="asset-action"></a>
## Asset Action

Asset Action is the core of Easy Asset Creator and it handles how your class is gonna be exposed to the different editor menus.

You need one Asset Action for each asset you want to expose.

<a name="create-an-asset-action"></a>
### Create an Asset Action

Start by right clicking in your content browser/drawer to create an **Asset Action**.

![CreateAssetActionImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_01.png)

And just choose the Asset Action class:

![ChooseAssetAction](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_02.JPG)

Now you have your first Asset Action class ready!

{: .box-note}
**Fun fact:** The **Asset Action** and **Asset Factory** entries in the Easy Asset Creator category are exposed via custom Asset Action classes in C++.

<a name="setting-up-your-asset-action"></a>
### Setting up your Asset Action

Open the Asset Action and go to the Class Defaults menu:

![ClassDefaultsMenu](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/cd3d51729157931767de4eab1452581f1afcabb8/assets/img/EasyAssetCreator/Image_03.JPG)

Choose the asset you want to expose in the **Asset Class** variable:

![ChooseAsset](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_19.JPG)

Now assign the category this asset should be exposed to in the different menus:

![ChooseCategory](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_20.JPG)

Now you are all done for the basic setup of an Asset Action!

<a name="sub-category"></a>
#### Sub-category

You can only add a sub-category if two or more classes are in the same category. Then assign a sub-category name to one of them, and you will get this:

![Sub-menus](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_27.JPG)

<a name="asset-factory"></a>
## Asset Factory

Factories are responsible for creating the actual asset and give it its name. Due to current engine "limitations", you unfortunately need both classes to expose your assets.

<a name="create-an-asset-factory"></a>
### Create  Asset Factory

Start by right clicking in your content browser/drawer to create an **Asset Factory**.

![CreateAssetFactoryImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_06.JPG)

Now you have your first Asset Factory class ready!

<a name="setting-up-your-asset-factory"></a>
### Setting up your Asset Factory

Open the Asset Factory and go to the Class Defaults menu:

![AssetFactoeyClassDefaultsMenu](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_17.JPG)

Now assign the same asset in the factory as in the Asset Action:

![AssignClassFactory](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_08.JPG)

Now you should be able to see your class in the **"Create Advanced Asset"** menu:

![CreateAdvancedMenu](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_11.JPG)

#### Default Asset Name

If you want to give the asset a custom default name once its created, assign it here:

![DefaultAssetName](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_10.JPG)

#### Use Class Picker

If true, summons a class picker when you click to create a new class in the category menu:

![UseClassPicker](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_12.JPG)

<a name="asset-appearance"></a>
## Asset appearance

<a name="asset-name-tooltip"></a>
### Asset name & tooltip

You might not want the default asset name/tooltip to be displayed when hovered, and that is an easy fix.

Go into the class you have exposed with the **Asset Action** and click on Class Settings, and this should show up:

![OldNameTooltipImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/8ec02df69d183ad6865bcba1cc2bc4795d4a2fc2/assets/img/EasyAssetCreator/Image_13.JPG)

Change to what you want under **Blueprint Display Name** and **Blueprint Description**, and compile and save.

Now your asset should be displayed with the new name and tooltip:

![NewNameTooltipImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_14.JPG)

<a name="asset-color"></a>
### Asset color

To change the color of the class in the menu, go into your **Asset Action** and change the color under **Asset Color**

{: .box-note}
**Note:** This will **not** change color of the asset once its created due to engine back-end stuff.

![AssetActionChangeColor](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_18.JPG)

Now your asset will appear in a different color:

![AssetActionChangeColor](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_16.JPG)

<a name="asset-action-fragments"></a>
## Asset Action Fragments

Fragments are used in Asset Actions to add different functionalities to the asset in the editor.

<a name="add-to-place-actors-menu"></a>
### Add to Place Actors Menu

![PlaceActorsMenu](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_22.JPG)

To add a Actor to the **"Place Actors"** menu. All you need to do is add this fragment to your **Asset Action**:

![PlaceActorsMenuFragment](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_24.JPG)

Now your Actor should be registered to the menu in its category! 

{: .box-note}
**Note:** You don't need a factory to add this functionality to an asset. Just need an **Asset Action** with a valid asset class assigned, category, and this fragment.

<a name="add-content-browser-drag-drop-support"></a>
### Add Content Browser drag drop support

Drag any of your assets into the viewport from the content browser. Works with any assets that derive from UObject.

Add the drag drop support fragment to the Asset Action:

![DragDropSupportFragment](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_25.JPG)

Add custom functionality to what will happen when the asset has been dragged into the viewport. Just override the function **PostSpawnActor** in the Asset Action.

In the example below, we drag a quest into the viewport, the Asset Action spawns the quest trigger we assigned, and then assign the quest class to that quest trigger.

![DragDropSupportFragment](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/EasyAssetCreator_04.JPG)

Now the asset should behave like this:

![DragDropGif](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/DragDropGif.gif)

<a name="deleting-assets"></a>
## Deleting assets

You can delete any Asset Action or Asset Factories without any dangerous impact. It might say it still has memory references left and you have to force delete the asset, but the plugin handles that.

![DeleteAssetPic](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_26.JPG)

<a name="common-issues"></a>
## Common issues

<a name="my-class-wont-update-its-name-in-the-menus"></a>
#### My class won't update its name in the menus

Try to save and compile the class.

<a name="my-class-doesnt-show-up-in-create-asset-menu"></a>
#### My class doesn't show up in the create asset menu

Make sure you have an Asset Action with a category and class assigned, as well as an Asset Factory with the same class assigned to **Parent Class** as in the Asset Action.
