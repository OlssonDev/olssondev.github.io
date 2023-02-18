---
layout: post
title: Easy Asset Creator Documentation
---

# Table of Contents
* [Plugin Overview](#plugin-overview)
* [Asset Actions](#asset-actions)
* [Get Started](#get-started)
* [Setting up your Asset Action](#setting-up-your-asset-action)

<a name="plugin-overview"></a>
## Plugin Overview 

Making editor tools for creating and placing assets is a tedious and time consuming process, and usually requires C++ to set up. Easy Asset Creator makes it easy to create tools for your assets, and all of it can be managed inside the editor with no requirements for an editor restart.

<a name="asset-action"></a>
## Asset Actions

Asset Action is the core of Easy Asset Creator and it handles how your class is gonna be exposed to the different editor menus.

You need one Asset Action for each asset you want to expose.

<a name="get-started"></a>
## Get Started

Start by right clicking in your content browser/drawer to create your first **Asset Action**.

![CreateAssetActionImage](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_01.png)

And just choose the Asset Action class:

![ChooseAssetAction](https://raw.githubusercontent.com/OlssonDev/olssondev.github.io/master/assets/img/EasyAssetCreator/Image_02.JPG)

Now you have your first Asset Action class ready!

{: .box-note}
**Fun fact:** The **Asset Action** and **Asset Factory** entries in the Easy Asset Creator category are exposed via custom Asset Action classes in C++.

<a name="setting-up-your-asset-action"></a>
## Setting up your Asset Action

**In progress...**