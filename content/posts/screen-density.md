---
author: "Todor Kostov"
title: "Android tricks - Determine current screen density"
date: "2017-01-19"
tags: [
    "android"
]
---

Do you know the thing I hate the most about Android? It's screen fragmentation! On the one hand, having a huge variety of screen sizes is great for the end users. But it's a complete nightmare for developers! Thus, it's really hard to create a good looking UI without any problems. There will always be a device with some wired screen size on which your layout will look bad!

There are several different approaches for handling this problem. Sadly, you can't be 100% sure that there won't be any UI issues. And if you have to manipulate a [View](https://developer.android.com/reference/android/view/View.html) through your Java code, things can get really nasty!

A good practice is to determine the current screen density of the device. We can do that with the following code snippet:

```
DisplayMetrics metrics = getResources().getDisplayMetrics();
float density = metrics.density;
```

The **density** variable holds a **float** value. It represents the logical density of your device. It's a factor based on the mdpi baseline.

## How is that useful?

I did the following thing several days ago:
My task was to create translation animations for some views. I had a xhdpi phone. Thus, I implemented the UI with values which made the views look great on this particular phone. Of course, they looked terrible on other devices. But that was not a problem.

For example, I knew that I had to translate a view with 200 dp on the X axis to look OK on my current phone. I knew my phone had a xhdpi screen. Thus, to make the UI relatively good for the rest of the devices out there, I had to find the base value for mdpi screens. I used the code from above and divided these 200 dp by the value in the **density** variable. And found out that the baseline value for mdpi screens was 100 dp.

By having this value, I was able to determine with how many dp I have to translate the view for the current device density. The only thing I had to do was to multiply it with the value from the code snippet above.

## Resources

* http://stackoverflow.com/questions/27590213/android-displaymetrics-densitydpi-returns-zero-on-rooted-devices

Feel free to share, comment & give your opinion on the topic!