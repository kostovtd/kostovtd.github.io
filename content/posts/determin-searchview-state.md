---
author: "Todor Kostov"
title: "Android tricks - How to determine the current state of your SearchView?"
date: "2017-02-10"
tags: [
    "android"
]
---

The [SearchView](https://developer.android.com/reference/android/widget/SearchView.html) provides a way for the user to enter a search query and submit it to a search provider. It's a widely used UI pattern in the Android system. Though, a simple task like figuring out if the search box is currently visible can be a bit tricky.

On the image below, you can see the two possible states for a SearchView. On the left one, the view is closed. On the right one the view is opened and holds the current focus.

![](/android-search-view.jpg)

One possible way to determine the current state of the view is to try to get a reference to the [EditText](https://developer.android.com/reference/android/widget/EditText.html) from the right image above. Then you can check if this view is visible or not. Based on that, you can determine the current state of the SearchView. But that sounds like a lot of work, right? Although, the code will be around 3-5 rows long it's still a lot. We are developers! And we are lazy!

Fortunately, there is a build-in method which can help us. It's called [isIconified()](https://developer.android.com/reference/android/widget/SearchView.html#isIconified()). Here's what the official Android documentation has to say about the result of that method:

> true if the SearchView is currently iconified, false if the search field is fully visible.

Feel free to share, comment & give your opinion on the topic!