---
author: "Todor Kostov"
title: "Android tricks - How to find view's dimensions before displaying the view?"
date: "2016-12-21"
tags: [
    "android"
]
---

Two days ago I had to work with some views (Surprise! Surprise!). At some point I had to get the actual views' width and height, before actually displaying the views. Of course, they were included in my XML layout. Thus this made the task a little bit easier. After spending several minutes on Google (ALWAYS do that, when you are in trouble), I found a solution.

{{< gist kostovtd 4eff0a1381cf31b3d465e5dbc72c3c2f >}}

## Code Description:

You can see that we can actually obtain the view's dimensions thanks to the [Display](https://developer.android.com/reference/android/view/Display.html) class. By using it we can get information about the size and density of the current logical display. Now, a logical display **DOES NOT** necessary represents an actual physical display. There can be a difference between these two.

After obtaining an instance of the Display class and finding the view we need, we must call the [measure()](https://developer.android.com/reference/android/view/View.html#measure(int,int)) method of that view. The actual implementation of it is not relatively simple, but the overall idea is that it calculates how big the view should be.

The only thing left is to call [getMeasuredWidth()](https://developer.android.com/reference/android/view/View.html#getMeasuredWidth()) & [getMeasuredHeight()](https://developer.android.com/reference/android/view/View.html#getMeasuredHeight()). These two methods return the raw width and height sizes of our view.

## References
* http://stackoverflow.com/a/8201072/4675457

Feel free to share, comment & give your opinion on the topic!