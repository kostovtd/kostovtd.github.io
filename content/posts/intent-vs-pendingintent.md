---
author: "Todor Kostov"
title: "Intent VS PendingIntent"
date: "2017-01-08"
tags: [
    "android"
]
cover:
    image: "posts/eikbsc3sdti-sonja-langford.jpg"
---

2016 is officially over and here we are at the beginning of 2017! So let's start the year with some wisdom!

Have you ever wondered what is the difference between [Intent](https://developer.android.com/reference/android/content/Intent.html) and [PendingIntent](https://developer.android.com/reference/android/app/PendingIntent.html)? Well, although they sound similar, there is a difference between them. As you can see, the documentation about these two entities is extensive and provides lots of information. But we will try to summarize it in a shorter version.

## Intent
That's one of the major entities in the Android SDK. We all use it almost everyday alongside with [Activity](https://developer.android.com/reference/android/app/Activity.html) and [Context](https://developer.android.com/reference/android/content/Context.html).

The Intent object is an abstract representation of an intent / action (Surprise! Surprise!). In other words, by using the Intent class you can start activities within your application, or you can communication with components defined by the Android system (a.k.a. Camera, Services, Contacts, browsers, etc.). Probably the most significant use of Intents is to start new Activities within an application.

There are two different kinds of Intents:
* **Explicit** - by using an explicit Intent, we can tell the Android system which exact Activity to start, or with which exact component of the Android OS we want to communicate. We know what we want to do and we know exactly what to use. [Here](https://developer.android.com/guide/components/intents-filters.html#ExampleExplicit) you can find an example of an explicit intent.
* **Implicit** - these intents are useful when we know what we want to do, but we don't know what exactly to use. For example, we might want to open a particular URL, but that URL can be opened by a browser, or by some other application. Thus, we give the responsibility to the system to determine which is the best component for the given task. [Here](https://developer.android.com/guide/components/intents-filters.html#ExampleSend) you can find an example of an implicit event.

The usual Intent's structure consists of two parts:
* **Action** - the action to be performed. There are multiple predefined actions, which you can find in the documentation.
* **Data** - the data to operate on. The data must be provided as an [Uri](https://developer.android.com/reference/android/net/Uri.html).

## Pending Intent

The pending intents are a little bit different than the normal intents. Actually, a PendingIntent represents a reference to a token. By using a PendingIntent to communicate with a foreign application like the Camera, Contacts, etc. you are telling that foreign application to execute some predefined code at some point in the future, by using the listed permissions of your application. It's like that foreign application is acting on the behalf of your application.

Now, that sounds messy, right? And why do we need such a thing? Well, that's really useful when you want to implement a push notification functionality into your application. In this case, you have the logic for handling notifications, but you don't actually know when you will receive one. Thus, you start a service by using a PendingIntent and stating what code should be executed when the notification was clicked.

A specific feature of the PendingIntent is that it is not related to the lifecycle of your application. Even if your application was intentionally being closed, or killed by the OS, the PendingIntent will remain and the processes to which it had been attached will be able to use it.

In order to create a PendingIntent you first need to construct a normal Intent.

## Conclusion

In conclusion, the general and main difference between Intent and PendingIntent is that by using the first, you want to start / launch / execute something NOW, while by using the second entity you want to execute that something in the future.

## References

* https://developer.android.com/reference/android/content/Intent.html
* https://developer.android.com/reference/android/app/PendingIntent.html
* http://stackoverflow.com/questions/2808796/what-is-an-android-pendingintent

Feel free to share, comment & give your opinion on the topic!