---
author: "Todor Kostov"
title: "DirectBoot in details"
date: "2017-03-05"
tags: [
    "android"
]
---

Android 7.0 (Nougat) brought plenty of new features to both average users and developers. Alongside features like Multi-window view, Notification Direct Reply and File-based Encryption something called Direct Boot was included as well. Although, it doesn't sound like a game changer, it still can have a huge impact on the user satisfaction. Using this new feature with creativity and responsibility can result in better applications. But what exactly is the idea behind Direct Boot? Let's try to find out!

## What is Direct Boot?

If you see your lock screen just after rebooting your phone, or turning it on, you are in a very interesting state. At this point, you are still not authenticated. Thus the system does nothing in relation to consuming notifications or launching services. All user's data is encrypted and unavailable until you authenticate yourself (a.k.a. enter a pin, pattern, password, etc.). And that 'weird' state occurs only the first time after rebooting, or turning on your device.

I hope you can see what issues that no-man's state can cause! Let's take the main stream example. You went to bed, set your alarm for 7:00 A.M. and took off for Narnia, Mordor, Hogwarts, Azeroth or any other magical place. Then you wake up, feeling fresh and happy, just to realize that it's 9:30 A.M. and you missed your interview for the dream job you have ever wanted. What did happen?! For one reason, or another, your phone has rebooted and it ended up in that particular state mentioned above. Thus, your alarm didn't have the chance to wake you up.

To prevent such problems, the folks from Google included Direct Boot into Android Nougat. If your clock / alarm app. was developed with Direct Boot in mind, then your alarm for 7:00 A.M. would be able to do it's job.

Direct Boot is something like a compromise between security and convenience. Applications which were developed with Direct Boot in mind, are able to execute a limited number of tasks while you still have not authenticated yourself. How is that possible? By introducing a second data storage called 'Device Storage', where you can store anything important for your app to run in Direct Boot Mode. But let's see what are the differences between the new 'Device Storage' and the relatively old 'Credential Storage'!

## Credential VS Device Storage

* **Credential Storage** - This is the default storage for the Android OS. Anything stored in it can not be access until some authorization is provided. Thus, it has a higher level of security, but a lower level of user convenience.
* **Device Storage** - This storage mechanism was introduced with Android 7.0. It is less secured than the previous one, but it provides higher level of user convenience. The data stored in it can be accessed from everywhere without requiring authorization. 

![](/1-ivkgyl3l-4anqsbtfzg44a.png)

## How to use it?

Before taking advantage of the Direct Boot Mode, you first have to enable it. For now this mode will be enabled by default on devices which come with pre-installed Android API 24 and above. Such devices are: Nexus 5X, Nexus 6P or Pixel C. My advice is to try this feature on an emulator, if you can, **because enabling it will cause the loss of all your data** (a.k.a. factory reset).

If you want to enable it on your own device go to **Settings -> Developer Options -> Convert to file encryption**. But yet again - all your data will be erased!

Now, the situation with emulating that mode on a virtual device is kind of tricky. I was not able to run that mode on a Genymotion emulator. But that was not the case with the AVDs which come with Android Studio. Configuring an emulation of Nexus 6P with Android 7.0 is enough for you to try the Direct Boot mode.

Also, I made a small app to be easier for us to get our hands dirty. For the sake of simplicity, there is no usage of any mainstream design patterns like MVP. It's just a simple app to show the basics of this feature. You can find the GitHub repository in the 'Resources' section down below.

The app does a single thing. It fires a notification when your device enters that no-man's state. If you try the app one a device which runs on an older Android version you will not see the notification at all.

The most interesting part of the app is the Manifest file. In it, we must do exactly three things to enable Direct Boot:
* Add the **RECEIVE_BOOT_COMPLETE** permission.
* Enable the Direct Boot feature for a specific app's component by setting the **directBootAware** property to **true**.
* Add the **LOCKED_BOOT_COMPLETED** intent filter to the boot-aware component.

{{< gist kostovtd 10b82d48aa1a04bc81d4485cb5680855 >}}

If you want to try the new storage mechanism you must obtain a specific Context reference first. Also, there are methods which can help you transfer any SharedPrefernces or Database info from the Credential to the Device Storage. I haven't used them yet. Thus, if you have, please share your impressions with us!

{{< gist kostovtd 1b11cd79609d074eaf64b3aea50db8d2 >}}

## Note

Be careful not to abuse the Direct Boot Mode. The folks from Google will spend extra time to shut down applications, which are spamming their users with unimportant notifications. Use this feature wisely and only take advantage of it, when there is a real reason for doing that!

## Resources

* https://github.com/kostovtd/DirectBoot

## References

* http://www.androidcentral.com/android-70-what-direct-boot
* http://www.androidauthority.com/direct-boot-711668-711668
* https://blog.stylingandroid.com/nougat-direct-boot

Feel free to share, comment & give your opinion on the topic!