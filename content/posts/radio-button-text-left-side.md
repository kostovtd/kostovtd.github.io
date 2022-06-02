---
author: "Todor Kostov"
title: "Android tricks - How to make the text of a RadioButton appear on it's left side?"
date: "2017-01-24"
tags: [
    "android"
]
---

Let's start 2017 with a quick and useful 'How to' article!

Have you ever tried to make the text of a [RadioButton](https://developer.android.com/reference/android/widget/RadioButton.html) appear on it's left side? It's tricky! You can check to source code down below:

{{< gist kostovtd b765edccc2eb5802013dd0095a4e8a56 >}}

## Code description

By default, for the usual left-to-right layout, the text appears on the right side of the RadioButton. As you can see from the snipped above, we actually use a particular property to change the direction of the current view:

```
android:layoutDirection="rtl";
```
In this way, we kind of try to trick the OS. How? By telling Android that this view is supposed to be read / used by a person who reads from right to left. That's not true, but it works for us!

After that little lie, you can align and change the gravity of the text according to your particular case.

And as [Irshu](http://stackoverflow.com/users/1155282/irshu) said in the Stackoverflow discussion from the References section - don't forget to set the **supportsRtl** property to **true** of your **application** tag in the Manifest file.

There are some other methods / tricks, which can be used, but there are some side effects as well. You can check the discussion mentioned above, if you want to make use of some of the methods.

## References

* http://stackoverflow.com/questions/18914792/how-to-put-the-text-on-the-left-of-a-radio-button-in-android

Feel free to share, comment & give your opinion on the topic!