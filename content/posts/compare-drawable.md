---
author: "Todor Kostov"
title: "Android tricks - How to compare two drawables?"
date: "2017-02-15"
tags: [
    "android"
]
---

Drawables are widely used throughout the developing process of Android applications. Because of one reason, or another we can be interested in comparing two drawable objects. At first, that sounds like an easy task, but actually it can be a bit tricky.

## The '==' operator

Of course, if you have two different instances of the same drawable resource, the '==' operator is useless. It's gonna compare if the left and the right side are actually the same instance. Thus, this operator is out of the game.

## The getConstantState() method

Now, there is a second option. Each drawable object has something called 'Constant state'. We can try to make use of it by calling the **getConstantState()** method of the two instances we already have. Then we can actually use the famous **equals()** method. Check the codes sniped down below.

{{< gist kostovtd ec773c70102ada8fb430579c4a756883 >}}

That method actually returns an instance of the abstract class [ConstantState](https://developer.android.com/reference/android/graphics/drawable/Drawable.ConstantState.html). It is used to store a shared constant state and data between Drawables. For example, two Drawables which reference the same resource, will share a unique Bitmap. This Bitmap is stored in the ConstantState class.

Now that can be useful, but it's not a complete, 100% accurate solution. It can produce a false negative result. The two drawables can reference the same resource, but comparing their ConstantStates can state otherwise. Thus, we have to find another solution.

## A custom solution

The following code provides a custom made solution, which should always work. Sadly, it requires more resources, but if used wisely, it won't be a big performance burden.

{{< gist kostovtd 8eb46fed1be6dfb096cb977a65987279 >}}

The general idea is that if we ended up in a possible false negative case, then we try to use a method called **sameAs()**. This method is in the [Bitmap](https://developer.android.com/reference/android/graphics/Bitmap.html) class. It extensively compares two bitmaps based on dimensions, pixel data, etc.

Now, to use the method mentioned above, we need to get or generate a Bitmap from the two Drawable object we have. For that purpose, we can use our **getBitmap(drawable)** method. With such naming, it's pretty obvious what it does. Now let's see how it does it.

If the given Drawable object is an instance of the [BitmapDrawable](https://developer.android.com/reference/android/graphics/drawable/BitmapDrawable.html) we can extract the Bitmap from it. If it's not, then we have some more things to do. We must create an empty Bitmap with the same dimensions like the given Drawable. Then we need a [Canvas](https://developer.android.com/reference/android/graphics/Canvas.html) on which we can actually draw our Drawable. And that's it! We now have a Bitmap which contains the same info like the given Drawable. Thus, we are now ready to compare it with the sameAs() method.

## References

* http://stackoverflow.com/questions/9125229/comparing-two-drawables-in-android

Feel free to share, comment & give your opinion on the topic!