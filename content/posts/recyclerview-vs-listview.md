---
author: "Todor Kostov"
title: "RecyclerView & ListView basic comparison"
date: "2017-02-05"
tags: [
    "android"
]
cover:
    image: "posts/9zule-8q7im-rosan-harmens.jpg"
---

Do you remember the good old [ListView](https://developer.android.com/reference/android/widget/ListView.html)? Back then it was the only option for showing items in scrolling lists. Then, at some point, a new player entered the field - the [RecyclerView](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html). For some period of time I was definitely confused about which one should I use. But day by day the RecyclerView took the whole stage and there was almost nothing left for the old ListView. Nowadays, if you need a listing functionality, the RecyclerView is the place to go. But what was the reason behind the success of the RecyclerView? Let's try to find out!

## RecyclerView info

The RecyclerView was introduced with Android 5.0 (Lollipop). Of course, it is included in the [Support Library](https://developer.android.com/topic/libraries/support-library/index.html). Thus, it is compatible even with Android API Level 7.

Similarly to the ListView, the RecyclerView's main idea is to provide listing functionality. But as you know, this is done in a performance friendly manner. The 'Recycler' part of this view's name is not there by coincidence. The RecyclerView can actually recycle the items with which it's currently working. Surprise! Surprise! The recycling process is done thanks to a pattern called [View Holder](https://developer.android.com/training/improving-layouts/smooth-scrolling.html). By using it, there is no need to call **findViewById()** each time we go through the **getView()** method of our adapter. The references to all views for each list row are kept in-memory. This significantly increases the performance. Of course, you can use this pattern together with a ListView, but it is optional. If you want to use a RecyclerView, you have no other option, but to implement the View Holder pattern. It is mandatory.

Also, the RecyclerView does less things than the ListView. It's always better to do less, but do it right. That sounds like the RecyclerView has less features than the ListView. But this is not true. It's actually more flexible and more feature rich. Just all these options are distributed into different entities like the [LayoutManager](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.LayoutManager.html) and [ItemAnimator](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ItemAnimator.html). Have you ever heard something about 'Separation of concerns'? If not, check the Wiki page in the 'See also' section.

Another great thing about the RecyclerView is the way it interacts with LayoutManager and ItemAnimator. These two provide some useful functionalities.Thanks to the LayoutManager we can create lists with vertical and horizontal scrolling ([LinearLayoutManager](https://developer.android.com/reference/android/support/v7/widget/LinearLayoutManager.html)) and uniform and staggered grids ([GridLayoutManager](https://developer.android.com/reference/android/support/v7/widget/GridLayoutManager.html), [StaggeredLayoutManager](https://developer.android.com/reference/android/support/v7/widget/StaggeredGridLayoutManager.html)). Or we can create our own manager with extra bit of customization. Thanks to the ItemAnimator we can make use of different animations. There are animations for adding, updating and removing items from the RecyclerView.

And let's not forget the great integration with the [DiffUtil](https://developer.android.com/reference/android/support/v7/util/DiffUtil.html) class. Long story short, this class helps us to calculate the difference between two lists of data. It's a must when using the RecyclerView! You can check the article about the DiffUtil class in the 'See also' section.

Of course, there are some drawbacks when using the RecyclerView. The distribution of responsibilities to the LayoutManager and the ItemAnimator, adds extra complexity. And if we include the mandatory usage of the ViewHolder pattern, the learning curve becomes not so smooth. Our brains are not capable of working with many different components at the same time. Thus it can be harder to get used to the way of using the RecyclerView.

Another inconvenient thing is the lack of a listener like the [OnItemClickListener](https://developer.android.com/reference/android/widget/AdapterView.OnItemClickListener.html). Of course, we can easily overcome that by using simple interfaces, but it's still worth mentioning.

## Pros & Cons of RecyclerView

**Pros:**
* integrated animations for adding, updating and removing items
* enforces the recycling of views by using the ViewHolder pattern
* supports both grids and lists
* supports vertical and horizontal scrolling
* can be used together with DiffUtil

**Cons:**
* adds complexity
* no OnItemClickListener

## ListView info

The ListView has been around since the very beginning of Android. It was available even in API Level 1 and it has the same purpose like the RecyclerView.

The usage of the ListView is actually really simple. In this aspect, it's not like its successor. The learning curve is smoother than the one for the RecyclerView. Thus, it is easier to grasp. We don't have to deal with things like the LayoutManager, ItemAnimator or DiffUtil.

If we want to keep things simple, we can even use default adapters. They can be used to show a simple text as a content for our items. There is no need of extending other classes or implementing interfaces. Of course, there is no problem to make our row elements more complicated, if we want to. Then we will have to construct our own custom adapters.

What about the OnItemClickListener? Well, it is one of these small, cool things in the life of the developer. It's really simple to use and doesn't increase complexity at all. The thing it does is self-explanatory. And I prefer working with such a listener, rather then creating my own interfaces for handling the same events in the RecyclerView. But that's life! :)

We should also mention the [ExpandableListView](https://developer.android.com/reference/android/widget/ExpandableListView.html) which is heavily based on the ListView. Actually, it extends the functionality of the ListView. It provides a two-level list, consisting of parent and child items. Each parent item is associated with many child items. That allows the usage of expanding and collapsing functionality for the child items. To use the ExpandableListView, we must construct our own custom adapter.

If we want to optimize the performance of our ListView, we can use the idea of the ViewHolder pattern here as well. The thing is, that the usage of this pattern is not mandatory. Thus, folks who are not familiar with it, can construct their ListView without a ViewHolder. That can decrease the performance.

## Pros & Cons of ListView

**Pros:**
* simple usage
* default adapters
* available OnItemClickListener
* it's the foundation of the ExpandableListView

**Cons:**
* doesn't embrace the usage of the ViewHolder pattern

## See also

* [Separation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns)
* [DiffUtil in details](https://kostovtd.com/posts/diffutils-details/)

## References

* https://www.raywenderlich.com/126528/android-recyclerview-tutorial
* http://stackoverflow.com/questions/26728651/recyclerview-vs-listview
* http://stackoverflow.com/questions/28392554/should-we-use-recyclerview-to-replace-listview
* https://www.bignerdranch.com/blog/recyclerview-part-1-fundamentals-for-listview-experts/
* http://stackoverflow.com/questions/28525112/android-recyclerview-vs-listview-with-viewholder

Feel free to share, comment & give your opinion on the topic!