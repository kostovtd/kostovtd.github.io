---
author: "Todor Kostov"
title: "Geo-fencing with MVP Part 1"
date: "2016-12-04"
tags: [
    "android"
]
cover:
    image: "posts/d2k1uzr4vxk-sylwia-bartyzel.jpg"
---

Several weeks ago, I had to implement a geo-fencing functionality in one of the projects on which I was currently working on. Due to the fact that I had never done that before, I had to do a 'small' research on the topic. Of course, tools like Google, Stackoverflow, the Android Documentation, etc. were there to help me. Happily, I managed to inform myself on the topic, but there was a small detail. I failed to find a good example of how to implement all the logic by using the MVP design pattern. So, that is how my journey began and step by step it led me to write these several articles.

In this article we will talk about what is the idea behind geo-fencing, why is it so useful and why choosing MVP as a design pattern for the example application which I managed to write. So, lets begin!

## What is geo-fencing?

According to Wikipedia a geo-fence is:
> a virtual perimeter for a real-world geographic area.

Thus, the use of geo-fences is called geo-fencing. There are two different types of geo-fences. The first one is based on a radius around a particular location and the second one is an actual set of boundaries like the boundaries of a city, building, neighborhood, etc. By having these boundaries on a map, we can take advantage of the different system events that can be fired if certain conditions have been met. Such events are fired when entering or exiting a particular geo-fence, or when predefined time was spend in the boundaries of such a geo-fence. The source code presented through out this set of articles will be based on the first type of geo-fencing.

## Why bothering with geo-fencing?

Although the implementation of such a functionality is not an easy one, it provides many possibilities for customer or user engagements. Making your application location aware, can have a huge positive impact on the overall user satisfaction. Just imagine how many different things you can do based on your application's context! If you are running a store and you have an application especially developed for your business, you can notify your users, when they are near your shop about great deals. Or you can send reminders to your users regarding things they have to do, when they are near a particular location. There are many many cases in which the geo-fencing functionality can have a huge business value and can increase the levels of satisfaction of your customers. Thus, spending some time on it is definitely worth it!

## Why MVP?

I won't go deep into the topic of design patterns, because there are tons of articles and books regarding their advantages and disadvantages. Long story short, if you spend that additional time and effort on designing your code base by using patterns like MVC / MVP / MVVM etc. you will most probably end up with a solid source base which has a perfect separation of concerns, high cohesion and lowcoupling. You can easily find some useful articles on the topic.
Down below you will find a classical diagram which represents the three major parts of the MVP design pattern.

![](/mvp_2-en.png)

## Resources

* https://en.wikipedia.org/wiki/Geo-fence
* http://www.tinmegali.com/en/model-view-presenter-android-part-1/

Feel free to share, comment & give your opinion on the topic!