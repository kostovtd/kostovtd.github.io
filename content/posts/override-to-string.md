---
author: "Todor Kostov"
title: "Android tricks - Overriding toString() in POJOs"
date: "2016-11-30"
tags: [
    "android"
]
---

Although, this small trick is not specifically related to the Android SDK, it is still a useful one. The ROI (Return On Investment and by investment I mean time) of overriding the **toString()** method of your POJOs (Plain Old Java Objects) is relatively high. At the end of the day, this small thing can make your developer life just a little bit better.

## How to override the **toString()** method?
There are two different ways for overriding this method (and any other method as well) - manually or automatically. The second one is more interesting. You can use the **Ctrl + O** (for Windows) combination in Android Studio. It will automatically open a pop-up screen with methods which can be overridden. Just find the **toString()** method and press **Enter**. You can see the pop-up down below.

![](/override.png)

## What to include into **toString()** & Why do we need that?
That's absolutely up to you! Usually, you should provide some general info regarding the instance of the current POJO.

Let's say you have a class called **Person**. In this class you have attributes like **first name / last name / age / gender / etc.** And constructing a String, into your toString() method, which contains a nicely formated info regarding that particular person is a great idea. In this way, whoever calls the toString() method to a particular instance of the Person POJO will get some useful information. On the other hand, if not overriding this method and still calling it, you will see some strange things like Person@asd21nfa or something similar. Sadly, that means nothing to us.

This approach is useful mainly during the development process, a.k.a. during debugging or simple logging. **DO NOT USE THIS FOR PURPOSES DIFFERENT THAN DEBUGGING AND LOGGING!**

## Resources:
* http://fragmentedpodcast.com/episodes/44/

Feel free to share, comment & give your opinion on the topic!
