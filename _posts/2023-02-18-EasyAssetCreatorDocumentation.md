---
layout: post
title: Easy Asset Creator Documentation
---

# Table of Contents
* [Plugin Overview](#plugin-overview)
+ [Asset Action](#asset-action)
    + [Create an Asset Action](#create-an-asset-action)
    + [Setting up your Asset Action](#setting-up-your-asset-action)
* [Asset Factory](#asset-factory)
    + [Create an Asset Factory](#create-an-asset-factory)
	+ [Setting up your Asset Factory](#setting-up-your-asset-factory)
* [Asset Appearance](#asset-appearance)
* [Asset Action Fragments](#asset-action-fragments)

<a name="plugin-overview"></a>
## Plugin Overview 

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

{: .box-note}
**Note:** We will skip sub-menus for now, they'll come back later in the documentation.

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

#### Asset name & tooltip

You might not want the default asset name/tooltip to be displayed when hovered, and that is an easy fix.

Go into the asset and click on Class Settings and this should show up:

![OldNameTooltipImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/8ec02df69d183ad6865bcba1cc2bc4795d4a2fc2/assets/img/EasyAssetCreator/Image_13.JPG)

Change to what you want under **Blueprint Display Name** and **Blueprint Description**, and compile and save.

Now your asset should be displayed with the new name and tooltip:

![NewNameTooltipImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_14.JPG)

#### Asset Color

To change the color of the Asset in the menu, go into your Asset Action and change the color under **Asset Color**

{: .box-note}
**Note:** This will **not** change color of the asset once its created due to engine back-end stuff.

![AssetActionChangeColor](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_18.JPG)

Now your asset will appear in a different color:

![AssetActionChangeColor](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_16.JPG)

## Asset Action Fragments

Fragments are used in Asset Actions to add different functionalities to the asset in the editor.

#### Add To Place Actors Menu

**In progress...**