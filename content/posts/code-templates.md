---
author: "Todor Kostov"
title: "Code templates"
date: "2019-03-11"
tags: [
    "android"
]
cover:
    image: "posts/photo-1426927308491-6380b6a9936f.jpg"
---

**Originally published on 10/30/2016**

After thinking about launching a blog for Android for near a month, finally I decided to do it! So here is the first and hopefully not the last post on the vast field of Android Development!


As developers, we sometimes have the awesome privilege to work on something really interesting for us like geofencing, another cool and good looking animation, face recognition or something else. But that's not always the case. During our everyday work we have to make a bunch of Activity classes with almost always the same lifecycle methods in them or RecyclerView adapters which implement the same ViewHolder pattern and that gets really tedious and boring (ooh and not to forget the fragments). And all that source code usually follows some kind of a pattern. Thus, having some predefined templates for these tasks sounds like a good idea.

There are several advantages of having such predefined templates:

Time saving - always spending 2 or 3 minutes just to override the basic lifecycle methods of an Activity or a Fragment can add up really fast when you have to do that multiple times a day. And doing that for a RecyclerView adapter takes even longer. At the end of the day, time is money, right?

Enforcing coding conventions - we all know the benefits of following coding conventions during the development process. Although, it is a small thing, at least the overall structure of your Activities, Fragments and other components will look the same, no matter who is their author.

Flexibility - the templates are really flexible and it's only up to you the modify them in the way most suitable for your current team or project.

## How to create a template?
Creating a template is actually really simple:

##### Step 1: Go to Settings
![](/settings.png)

##### Step 2: Find Editor -> File and Code Templates
![](/file_and_code.png)

##### Step 3: Create the actual templat

In order to be able to choose a template each time you create a new class, enum, interface etc. add the template you want under the Files tab in the main section of the pop-up window from Step 2. Adding a new entry under this tab is easy - just click the green plus sign above Files.


Down bellow you will find two examples of the templates, which I am currently using. They are written to meet my personal preferences, thus I am not completely sure that they will suit you, but at least you can have an idea of how to make them. (honestly, it's not rocket science)

{{< gist kostovtd 0a8b978e24b0114a38f6e6dcbdafe2a8 >}}

[Here](https://gist.github.com/kostovtd/31a793e2fb7518b750cb2f03382f871d) you can find a link to the rest of the templates that I am currently using.


Feel free to share, comment & give your opinion on the topic!