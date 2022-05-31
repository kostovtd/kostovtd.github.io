---
author: "Todor Kostov"
title: "Android tricks - ViewPager and Offscreen Tabs"
date: "2019-03-11"
tags: [
    "android"
]
---

**Originally published on 11/23/2016**

As I wrote in one of my first posts, we use Tabs a lot in our applications. They provide a great way of navigating to different screens through our app. And in order to use tabs, we have to work with something call a [ViewPager](https://developer.android.com/reference/android/support/v4/view/ViewPager.html). According to the official documentation, this is a layout manager that allows us to flip left and right through pages of data. These pages of data are usually composed of [Fragments](https://developer.android.com/guide/fragments). And in order to increase the performance and efficiency of the application, the views of each fragment / tab, which is off-screen, can be destroyed. The idea is to keep as little information in memory as possible. Sometimes this optimization can lead to problems, if the number of off-screen tabs is not set properly. User input can be lost, views' state can be reset, etc. Thus, we need to carefully choose that number of off-screen tabs.

## How can we do that?

By default, the number of off-screen tabs is set to 1. This means that there can be 1 tab to the left and 1 tab to the right of the currently visible tab, which will be kept in memory. Changing that value is fairly easy.

> mViewPager.setOffScreenPageLimit(limit)

That's all we need. The [setOffScreenPageLimit()](https://developer.android.com/reference/android/support/v4/view/ViewPager.html#setOffscreenPageLimit(int)) method will handle the rest.


## Resources

* https://developer.android.com/reference/android/support/v4/view/ViewPager.htm 


Feel free to share, comment & give your opinion on the topic!