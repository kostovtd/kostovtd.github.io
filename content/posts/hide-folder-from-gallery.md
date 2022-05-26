+++
author = "Todor Kostov"
title = "Android tricks - Hide a folder from the Gallery app"
date = "2019-03-11"
tags = [
    "android"
]
categories = [
    "android"
]
+++

**Originally published on 11/10/2016**

Here is a small trick for preventing a folder from appearing in the Gallery application:

{{< gist kostovtd 49834eb6b37777e88a94e834ec80b899 >}}

## Code description:

The general idea is really simple. We just have to create an empty file with the name **.nomedia**. That's all! And that's exactly what we want to do with the code snippet above. When the media scanner detects the .nomedia file, the folder is just being skipped by the OS and thus it wont be visible from the Gallery application.

## Why do we need it?!

The main reason for hiding a folder from the Gallery application is... well... because you just want that particular folder to remain hidden! Sometimes you have to cache images or any other media files and you usually store them in a folder. But the Gallery application is very good in finding directories which contain media files and so your folder appears in the Gallery app. And you will agree with me that it's not a good idea to show the user all your dirty and nasty hacks, transformations and changes you had made to the media files used by your application. Thus, hiding such folders suddenly seems beneficial.

Feel free to share, comment & give your opinion on the topic!