---
author: "Todor Kostov"
title: "Logging in Android"
date: "2018-01-17"
tags: [
    "android"
]
cover:
    image: "/posts/1_6ayoaqu0q9ivgvfey9mirq.jpeg"
---

I am sure that each developer out there have heard the phrase ‘Check the logs’ at least once during his or here career! And checking the logs have saved my ass several times this month. But what exactly a log message is and what are the advantages and disadvantages of logging? Let’s try to find out!

## What is logging?

Logging — the cutting, skidding, on-site processing and loading of trees onto trucks. (taken from Wikipedia) OK just kidding… but what about logging in software development? This is the process of printing or saving information about what exactly your code is doing and what is the current data it works with.

Most, if not all, programming languages support the idea of logging in one way or another. Although, the syntax is probably different, the general idea is always the same.

## Pros & Cons of Logging

If used properly, logging can be a life-saving mechanism for discovering bugs, performance issues and other problems. It can also provide valuable information about the usage of your software.
But if done poorly, it can make your life miserable… We all know that feeling of going through thousands and thousands of lines of log messages without any useful info at all.

**Pros:**
* A cheap way of building a stacktrace or a mechanism for monitoring the order of methods execution
* A way to follow different logic flows throughout your source code
* A way for monitoring the actual data your code works with

**Cons (if done poorly):**
* Can generate tons of useless info
* Can significantly decrease the readability of your source code

## Logging options in Android

The Android framework has it own set of logging options. There is a special [Log](https://developer.android.com/reference/android/util/Log.html) class which provides the needed functionality for printing a log message. There are also several different types of log messages, which can be used in different situations:
* [Log.e](https://developer.android.com/reference/android/util/Log#ERROR) - used for logging messages of type ERROR. This type is usually used inside of catch statements. It notifies us that something bad happened.
* [Log.w](https://developer.android.com/reference/android/util/Log#WARN) - used for logging messages of type WARN (warning). A common use-case for this type is when something strange happened, but it is not necessarily an error.
* [Log.i](https://developer.android.com/reference/android/util/Log#INFO) - used for logging messages of type INFO. It’s perfect when we want to log some useful info like connecting to a server, successfully finishing a process, successfully receiving info from another universe, etc.
* [Log.d](https://developer.android.com/reference/android/util/Log#DEBUG) - for these cases when you need to be sure that a + b = c or when you want to check if that problematic if statement is actually working. Thus, **d** stands for DEBUG. Some of you may think that, if this log message is used for debugging, then ALL Log.d messages will be stripped automatically during runtime. And if you refer to the official Android documentation, you will be right! But… in reality that’s not the case. You will have to make some additional steps in order to achieve that.
* [Log.v](https://developer.android.com/reference/android/util/Log#VERBOSE) - V for Vendetta… nope… ‘v’ stands for VERBOSE. This is more like a general type of a log message. You should use it whenever you want to print some very detailed info about the event that occurred.
* [Log.wtf](https://developer.android.com/reference/android/util/Log#wtf(java.lang.String,%20java.lang.String)) - I know what you are thinking, but ‘wtf’ stands for ‘What a Terrible Failure’. It looks like Log.e, but it’s way more sever. It’s to be used in these strange cases, which should never happen but… they do from time to time…

## Resources

* https://developer.android.com/reference/android/util/Log.html
* https://stackoverflow.com/questions/7959263/android-log-v-log-d-log-i-log-w-log-e-when-to-use-each-one
* http://vasir.net/blog/development/how-logging-made-me-a-better-developer

Feel free to share, comment & give your opinion on the topic!