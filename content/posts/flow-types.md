---
author: "Todor Kostov"
title: "Flow types"
date: "2022-06-15"
tags: [
    "android"
]
cover:
    image: "/posts/pexels-aleksandr-neplokhov-1238965.jpg"
---

It's been a while since my last post! Actually, more than 4 years... The Android ecosystem has changed a lot during that time! Some new concepts were introduced, some old programming languages were left behind and we have to make the most out of this situation (as always). So, let's get down to business! 

## What is a Flow? (briefly) 
The flow is a "new" concept of doing asynchronous tasks. Flows are built on top of coroutines and I am sure you have heard about them. The difference between flows and coroutines is that, the first is meant to produce multiple values one after the other, while the second is meant to produce a single value. 

Flows are really useful when you need continuous updates of your data – e.x. live updates of a table from a database. 

## Types of flows 
Having just a single way of creating flows would have been easy, but that's not the case! Actually, there are some situations where we need a more specific functionality than the one out of the box. Thus, there are three different types of flow constructors that can come in handy: 
* **flow**  - that's the default way of creating flows. This constructor creates a cold flow. You are probably wondering what actually a cold flow is, right? Well check [this discussion](https://stackoverflow.com/questions/69297362/what-is-the-hot-flow-and-cold-flow-in-coroutines-and-the-difference-between-them). In order to "return / produce" a result we have to use the [**emit()**](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/flow.html) method, which also ensures that the current scope is still active by calling [**ensureActive**](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/ensure-active.html). 

```
fun myFunction(): Flow<MyObject> = flow { emit(MyObject()) } 
```

* **CallbackFlow** – this type of flow is useful when you want to convert a callback-based API into a flow. A good example for this is the Firebase SDK. If you want to listen to changes in a Firestore document, you have to use a callback. But what if your app's architecture is based on flows? That's right – callbackFlow is here to help! This flow is using channels under the hood. You can read about them [here](https://kotlinlang.org/docs/channels.html), because we will not get into details about them. An important thing when using this flow type is to make use of [**awaitClose**](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.channels/await-close.html). This argument is called when: 
    * The flow consumer cancels the collection 
    * The callback-based API invokes [**SendChannel.close**](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.channels/-send-channel/close.html) 

This is a great place to clean whatever it's needed before closing the flow – e.x. unregister a callback. 

{{< gist kostovtd 94414918a98f57a43dea6db018d719a8 >}}

* **ChannelFlow** – the base flow type from which the CallbackFlow inherits most of its functionality. If you dig into its implementation, you will notice that the only difference with CallbackFlow is that channelFlow doesn't throw an **IllegalStateException** in its **collectTo** method. Thus, we can conclude that its functionality is almost the same as CallbackFlow. 

## Resources 
* https://stackoverflow.com/questions/61865744/android-kotlin-coroutines-what-is-the-difference-between-flow-callbackflow-ch 
* https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/callback-flow.html
* Photo by [Aleksandr Neplokhov](https://www.pexels.com/photo/group-of-people-gathering-near-frees-standing-flow-letters-1238965/)

Feel free to share, comment & give your opinion on the topic!


