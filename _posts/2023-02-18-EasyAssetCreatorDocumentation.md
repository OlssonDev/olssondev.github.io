---
layout: post
title: Easy Asset Creator Documentation
---

# Table of Contents
* [Plugin Overview](#plugin-overview)
+ [Asset Actions](#asset-actions)
    + [Create an Asset Action](#create-an-asset-action)
    + [Setting up your Asset Action](#setting-up-your-asset-action)
* [Asset Factory](#asset-factory)
    + [Create an Asset Factory](#create-an-asset-factory)



<a name="plugin-overview"></a>
## Plugin Overview 

Making editor tools for creating and placing assets is a tedious and time consuming process, and usually requires C++ to set up. Easy Asset Creator makes it easy to create tools for your assets, and all of it can be managed inside the editor with no requirements for an editor restart.

<a name="asset-action"></a>
## Asset Actions

Asset Action is the core of Easy Asset Creator and it handles how your class is gonna be exposed to the different editor menus.

You need one Asset Action for each asset you want to expose.

<a name="create-an-asset-action"></a>
## Create an Asset Action

Start by right clicking in your content browser/drawer to create an **Asset Action**.

![CreateAssetActionImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_01.png)

And just choose the Asset Action class:

![ChooseAssetAction](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_02.JPG)

Now you have your first Asset Action class ready!

{: .box-note}
**Fun fact:** The **Asset Action** and **Asset Factory** entries in the Easy Asset Creator category are exposed via custom Asset Action classes in C++.

<a name="setting-up-your-asset-action"></a>
## Setting up your Asset Action

Open up the Asset Action you just created and go to the Class Defaults menu.

It should look like this:

![ClassDefaultsMenu](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/cd3d51729157931767de4eab1452581f1afcabb8/assets/img/EasyAssetCreator/Image_03.JPG)

Choose the asset you want to expose in the **Asset Class** variable:

![ChooseAsset](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_04.JPG)

Now assign the category this asset should be exposed to in the different menus:

![ChooseCategory](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_05.JPG)

Now you are all done for the basic setup of an Asset Action!

{: .box-note}
**Note:** We will skip sub-menus for now, they'll come back later in the documentation.

<a name="asset-factory"></a>
## Asset Factory

Factories are responsible for creating the actual asset and give it its name. Due to current engine "limitations", you unfortunately need both classes to expose your assets.

<a name="create-an-asset-factory"></a>
## Create your first Asset Factory

Start by right clicking in your content browser/drawer to create an **Asset Factory**.

![CreateAssetFactoryImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_06.JPG)

Now you have your first Asset Factory class ready!


## Setting up your Asset Factory

**In progress...**