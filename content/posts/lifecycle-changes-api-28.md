---
author: "Todor Kostov"
title: "Lifecycle changes after API 28"
date: "2022-08-27"
tags: [
    "android"
]
---

Some time ago, I was going through the documentation about the infamous Activity class. All was good and even uneventful until I came across an interesting paragraph stating the following: 

![](/SmartSelect_20220706-094224_Brave.jpg)


A question popped up in my head- but why the change in the order? 

My first idea was to search for any articles on the topic. Sadly, with no result.

Then, I decided to go through the source code of the Activity class. There was also nothing that could provide some insight on the topic.

My last resort was to search for some discussions on Stack Overflow. To my surprise, there was a useful reference to the Android documentation.

![](/Screenshot_20220811-204902_Brave_2.jpg)

Although the last paragraph throws some light on the topic, I was still not satisfied with it.

After initiating a discussion on Stack Overflow, I can conclude the following - First of all, it's hard to come up with a precise answer to this question without actually involving some engineers from Google. For sure, they will be able to give enough information on the topic. Thus, the following statement is just speculation. The one possible reason behind this change is **consistency**. Before API 28, we couldn't be 100% sure that the code in on Save Instance State will be executed at all. That can lead to losing important data and the inability to properly recreate the state. With the changes introduced in API 28, we can now be sure that our data will be saved.

Thanks to [Martin Marconcini](https://stackoverflow.com/users/2684/martin-marconcini) for giving his 5 cents on the topic. 

Feel free to share, comment & give your opinion on the topic!


