---
author: "Todor Kostov"
title: "DiffUtil in details"
date: "2017-01-15"
tags: [
    "android"
]
cover:
    image: "posts/6ur2fvtdcxu-steinar-engeland.jpg"
---

The chances of developing a medium to large size Android application without using RecyclerView are relatively low. The scrollable list, as UI and UX pattern, is really powerful. It gives us the possibility to group similar items or entities into lists. They are easy to grab and to understand.

But there are some difficulties related to this pattern as well. We often have to update those lists with some newly entered, or server-fetched information. Doing that as fast as possible and using as little resources as possible is really important. The good news is that there is a handy class called [DiffUtil](https://developer.android.com/reference/android/support/v7/util/DiffUtil.html), included in the [Support Library](https://developer.android.com/topic/libraries/support-library/index.html). It was officially added in release **24.2.0**.

## The purpose of DiffUtil

Here's what the official Android documentation has to say about DiffUtil:

> DiffUtil is a utility class that can calculate the difference between two lists and output a list of update operations that converts the first list into the second one.

That sounds really useful! And if we read further:

> It can be used to calculate updates for a RecyclerView Adapter.


So, enough with the tedious and sometimes complex logic of handling data updates for our RecyclerViews.

## DiffUtil vs notifyDataSetChanged()

Some will say that there are other ways to update the information of a RecyclerView. And they will be right! The two most common approaches I have seen till now are:
* **Using [notifyDataSetChanged()](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyDataSetChanged())** - by using this method, there is no way for the RecyclerView to know what the actual changes in the data set are. Thus, it is assumed that all current items and data are invalid. That is why all visible views will be recreated again. This sounds like an expensive operation.
* **New instance of your adapter** - it requires even more resources and time than the previous one. It is easier for the developer just to assign a new instance of his / her adapter to the RecyclerView. Although, the price payed in performance is huge.

Now, the DiffUtil class has some great advantages. It is based on an algorithm by [Eugene W. Myers](https://en.wikipedia.org/wiki/Eugene_Myers). Of course, lots of math is involved here. There is a link to the official paper of the algorithm in the 'References' section. The paper describes the main idea behind the algorithm and it's variations.

As stated in the documentation, the algorithm is optimized for space. It requires **O(N)** space to find out the number of operations for transforming the old list into the new one. It's expected performance is **O(N + D^2)**. N is the sum of the lengths of the two lists and D is the length of the edit script. The edit script is the smallest set of deletions and insertions to transform the first list into the second. If you feel uncomfortable with these O(bla bla), you can check the 'References' section. There is a great article, which explains the basics of this concept. It's written for developers by a developer.

## Interesting things about DiffUtil

The implementation of the DiffUtil class is not based on recursion. By using recursion we can solve some relatively complex problems. Although, this approach can be useful, there is a drawback - possible stack overflow exceptions. Thus, the guys from the Android team decided not to use it.

Another interesting fact is that the maximum length of the list is 2^26. Now, that's a big number - **67 108 864**. It's more than enough. Although, having a list with that many items is a sign that you are doing something wrong! This limitation is set due to implementation constraints. Sadly, I was not able to figure out what is the reason behind this limitation. So, if you know it, feel free to share it!

DiffUtil uses these methods to notify the RecyclerView for any changes in the data set:
* [notifyItemMoved](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemMoved(int,int))
* [notifyItemRangeChanged](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeChanged(int,int))
* [notifyItemRangeInserted](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeInserted(int,int))
* [notifyItemRangeRemoved](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.Adapter.html#notifyItemRangeRemoved(int,int))

Their names explain their purpose pretty well. According to the official documentation, they are significantly more efficient than the famous **notifyDataSetChanged()**.

## DiffUtil and performance

Down bellow you will find the results from a test performed with **Nexus 5X** running on **Android M**.

![](/screenshot-from-2017-01-15-21-29-26.png)

The conclusion is that moving items around can decrease the performance of the algorithm. Based on the average values, there is a decrease of between **23%** to almost **50%** in performance. It's because, Myers' algorithm does not handle moved items. Thus, a second pass of the DiffUtil's algorithm is needed. That adds another O(N^2) time to the result, where N is the number of added and removed items.

In the "References' section, there are some actual examples of how to use the DiffUtil class. Both articles contain enough code, so that you can become familiar with the use of DiffUtil.

## References

* Eugene Myers' algorithm - http://www.xmailserver.org/diff2.pdf
* Big-O notation - https://justin.abrah.ms/computer-science/big-o-notation-explained.html
* DiffUtil is a must! - https://medium.com/@nullthemall/diffutil-is-a-must-797502bc1149#.h81kkeftj
* Using DiffUtil in Android RecyclerView - https://medium.com/@iammert/using-diffutil-in-android-recyclerview-bdca8e4fbb00#.4vlcxvrp7

Feel free to share, comment & give your opinion on the topic!