---
author: "Todor Kostov"
title: "Parcelable vs Serializable"
date: "2017-05-17"
tags: [
    "android"
]
---

Often, when we develop applications, we have to transfer data from one [Activity](https://developer.android.com/reference/android/app/Activity.html) to another. Of course, we can not do that directly. The data we want to transfer must be included into a corresponding [Intent](https://developer.android.com/reference/android/content/Intent.html) object. And if we want to move a complex POJO (e.x. Person, Car, Employee, etc.) we also need to perform some additional actions to make that object suitable for a transfer. To do that, our object must be either Serializable or Parcelable.

## What is Serializable?

[Serializable](https://docs.oracle.com/javase/7/docs/api/java/io/Serializable.html) is a standard Java interface. It is not a part of the Android SDK. It’s simplicity is it’s beauty. Just by implementing this interface your POJO will be ready to jump from one Activity to another. In the following code snippet you can see how simple it is to use this interface.

{{< gist kostovtd deb0d6c709efd482d2065f9ba75db9a4 >}}

Because Serializable is a marker interface, we don’t have to implement tons of extra methods. When we ‘mark’ our POJO with it, Java will try it’s best to serialize it.
Of course, this simple approach has it’s price. Reflection is used during the process and lots of additional objects are created along the way. This can cause lot’s of garbage collection. The result is poor performance and battery drain.

## What is Parcelable?

[Parcelable](https://developer.android.com/reference/android/os/Parcelable.html) is another interface. Despite it’s rival (Serializable in case you forgot), it is a part of the Android SDK. Now, Parcelable was specifically designed in such a way that there is no reflection when using it. That is because, we are being really explicit for the serialization process. In the code snippet down below you can see a sample usage of the Parcelable interface:

{{< gist kostovtd d76e5f36abfd36d407a1f99d424a7cb3 >}}

Of course, there is a price we have to pay when using Parcelable as well! Because of the boilerplate code, it is much harder to maintain and understand the POJO from above.

## Parcelable VS Serializable

![](/14861-1dsk7z8y9rniepcxru5ntwg.png)

If you search through the web for info on this topic, you will most probably come to the conclusion that there won’t be an absolute winner for this comparison. There are people and articles out there, which support either the one, or the other approach. Thus, I will present you both sides and leave you to decide for yourself!
The first ‘team’ stands behind the idea that Parcelable is way faster and better than Serializable. Of course, there is data behind this statement.

![](/78b26-1d4iacvhmfirbgr4c0yqcvw.png)

The results from the tests conducted by Philippe Breault show that Parcelable is more than 10x faster than Serializable. Some other Google engineers stand behind this statement as well.You can find a link to Philippe’s article in the ‘References’ section down below.

Now, the second ‘team’ claims that we are all doing it wrong! And their arguments sound reasonable enough!
According to them, the default Serializable approach is slower than Parcelable. And here we have an agreement between the two parties! BUT, it is unfair to compare these two at all! Because with Parcelable we are actually writing custom code. Code specifically created for that one POJO. Thus, no garbage is created and the results are better. But with the default Serializable approach, we rely on the automatic serialization process of Java. The process is apparently not custom at all and creates lots of garbage! Thus, the worse results. 

Now, there is another approach. The whole automatic process behind Serializable can be replaced by custom code which uses **writeObject()** & **readObject()** methods. These methods are specific. If we want to rely on the Serializable approach in combination with custom serialization behavior, then we **must** include these two methods with the same **exact signature** as the one below:

{{< gist kostovtd 0e6b7d455a20802a581dc3dfe51a6069 >}}

Strange! Weird! Unusual! But that’s how it works! Now, in these two methods we can include our custom logic. If done correctly, the garbage associated with the default Serializable approach will not be a factor anymore!
And now a comparison between Parcelable and **custom** Serializable seems fair! The results may be surprising! The custom Serializable approach is more than 3x faster for writes and 1.6x faster for reads than Parcelable. You can find a BitBucket project with test data in the ‘Resources’ section to play with.

In my opinion, the differences in speed between the two approaches will be almost insignificant in **most of the cases**. Thus, at the end of the day, it is rather more important to get the job done and to have happy users, than to have an app running with 0.000042 milliseconds faster.

## References

* http://www.developerphil.com/parcelable-vs-serializable/
* http://nemanjakovacevic.net/blog/english/2015/03/24/yet-another-post-on-serializable-vs-parcelable/
* https://bitbucket.org/afrishman/androidserializationtest/verview

Feel free to share, comment & give your opinion on the topic!