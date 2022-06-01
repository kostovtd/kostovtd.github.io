---
author: "Todor Kostov"
title: "Android tricks - How to add an icon to your Toolbar?"
date: "2016-12-14"
tags: [
    "android"
]
---

Today I had to implement something which is not so popular throughout the Android universe. I had to implement a simple [Toolbar](https://developer.android.com/reference/android/widget/Toolbar.html) with a logo on it's left side. That's not so popular these days, but from time to time there always will be someone who wants something like that. All in all, the end result had to be similar to the one down below:

![](/toolbar_icon.png)

I ended up with two different solutions based on weather you want your icon to be on the left side of the title, or on the right side.

If you want to accomplish the result from the picture above, you will need not more than 3 rows of code:

```
Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
setSupportActionBar(toolbar);
getSupportActionBar().setIcon(R.drawable.ic_icon);
```

These rows must be included in your **onCreate()** method of your [Activity](https://developer.android.com/reference/android/app/Activity.html). First, we have to find our Toolbar view and then we need to set it as the support ActionBar for the current Activity. At the end we need to provide an icon for the current ActionBar. That's all.

In case you want to add an icon on the right side of the title, then the only thing you have to do is to include an [ImaveView](https://developer.android.com/reference/android/widget/ImageView.html) into your xml file which contains the Toolbar widget in the following way:

{{< gist kostovtd a5215121dcac269da5ff05211eb70aba >}}

**Please, notice that before using the Toolbar widget you have to set your app theme to .NoActionBar.**

## Resources

* http://stackoverflow.com/questions/35913688/show-imageview-in-android-toolbar-at-top-left-corner-before-title

Feel free to share, comment & give your opinion on the topic!