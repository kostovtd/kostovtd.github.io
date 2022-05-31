---
author: "Todor Kostov"
title: "Android tricks - Gradle and license agreements"
date: "2019-03-11"
tags: [
    "android"
]
---

**Originally published on 11/16/2016**

Working with [Gradle](https://gradle.org/) through Android Studio is fairly easy and pleasant thing. But sometimes, you will need to build your projects on a machine without Android Studio. Gradle can be really helpful during that process and can automatically download any missing SDK packages as long as the accepted license agreement for them is in place. If it is missing, then you will have a problem.

## How to find the license agreement?

Finding the agreement is fairly easy:
1. Switch to the machine which has the Android Studio installed.
2. Go to Tools > Android > SDK Manager.
3. Copy the Android SDK Location path.
4. Go to the directory from step 3.
5. Copy licenses/ directory to the machine you want to build your project on.

## What is in licenses/ ?

There is just a single file, usually called android-sdk-license. If you open it with any text editor, you will see a relatively long kind of a key. That folder is automatically generated when you accept any license agreement through the SDK Manager.

## When will we need that?

The most obvious case for me is when you are trying to integrate your project into any kind of a Continuous Integration system like Bamboo, Jenkins, etc. and that integration is being done one a different machine.

## Resources

* https://developer.android.com/studio/intro/update.html#download-with-gradle

Feel free to share, comment & give your opinion on the topic!