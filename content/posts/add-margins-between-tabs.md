---
author: "Todor Kostov"
title: "How to add margins between tabs in TabLayout"
date: "2016-11-02"
tags: [
    "android"
]
---

Tabs... Almost each and every application has at least one screen with tabs. Using that UI pattern gives us the desired high level organization of the content we have in our app.

Several months ago I had to implement a [TabLayout](https://developer.android.com/reference/com/google/android/material/tabs/TabLayout) with margins between the tabs, which at the begging seemed like a regular task. Sadly, I was wrong. I expected to be fairly easy, but there was not a straight forward way to do that. Thus, I had to spend several hours in order to figure out how to do it.

But first, let me show you the main idea!

On the picture down below you can see just a regular TabLayout. The whole width of the layout is separated equally between the three tabs and there is no margin at all between them.

![](/components_tabs_usage_mobile3.png)

On the second picture you can see the desired result. The margins between the tabs are present.

![](/tabs_margin.png)

At the end, I came up with the following solution:

{{< gist kostovtd 32f85333fa92e72a00fa3495190d58aa >}}

## Code description
In general, the main idea of the code snippet above is to get each tab as a View and to add margin to it. The tricky part is how to actually get the tabs one by one. If we go through the source code of the TabLayout class, we will notice that each and every time we add a new tab to the TabLayout, that tab is being included in a SlidingTabStrip. Thus, the strip is the container of all the tabs we have. The good news is that it's pretty easy to reach the SlidingTabStip, because it's the first child of the TabLayout. And after that we can easily add margins to the tab views in the usual way.

Feel free to share, comment & give your opinion on the topic!