---
author: "Todor Kostov"
title: "App Shortcuts in details"
date: "2017-03-12"
tags: [
    "android"
]
---

Not long ago, the iOS users were introduced to a new feature called **3D Touch**. What this feature does is to provide a limited list of actions that you can do without entering an app. Of course, the folks from Google were ready to respond to that. Thus, the **App Shortcuts** feature was included in Android 7.1.1

## What are App shortcuts?

The main idea behind App Shortcuts is not different than the one behind the 3D Touch. With this new feature, the users can start app actions directly from their launcher, by long pressing the app icon.

![](/app-shortcuts_youtube_final-width-581.png)

There are two different types of App Shortcuts: 
* static
* dynamic

And now is the best time to list their differences:
* **Static shortcuts** - These shortcuts are predefined. They come together with your .apk. Their number and actions stay the same until you publish a new version of your app.
* **Dynamic shortcuts** - These shortcuts are constructed and included in the list with shortcuts on the fly. They can be created based on some usage statistics and can change over time. There is no need to publish a new version of your app, in order to update your dynamic shortcuts.

Now, with this combination between static and dynamic shortcuts, we can expand our creativity even further. Such a feature can be useful in many different contexts. Messaging, navigation, games, productivity apps and many others can take advantage of App Shortcuts. Thus, we (the developers) now have another tool for increasing the UX and satisfaction levels of our apps.

Currently, some of the famous apps out there are now using the App Shortcuts feature:
* Google Maps
* Google Play Music
* Google Photos
* Google Drive
* Chrome
* YouTube
* Evernote
* Twitter

There are other apps as well, so feel free to share them with us!

## How to use them?

Using Apps Shortcuts is not a rocket science! And there is no better way to prove you that than developing a simple application. In this way we can get our hands dirty again! In the ‘Resources’ section down below, you will find a link to the Git repository of the application. The app is nothing special, but it shows the very basic features of App Shortcuts. It takes advantage of both dynamic and static shortcuts. For the sake of simplicity, design pattern like MVP, MVVM, etc. are not implemented in the app. If you are a Kotlin fan, you can find a link to another Git repo in the ‘Resources’ section. It’s a great app with shortcuts about constellations, based on Kotlin.

## Static shortcuts

As said earlier, the static shortcuts are predefined and they can not be changed unless there is a new version of your app. To create a static shortcut, we must describe it with XML. Technically, we can create our XML file in **res/xml-v25/**, but a better approach is to create it in **res/xml-v22/**. The reason for that is that more and more launchers are trying to backport App Shortcuts to API level 22. Down below you can see how to define static shortcuts.

{{< gist kostovtd 411462bd6d692bc7f3827db8362c381f >}}

There are three static shortcuts in the app. For each shortcut we must provide:
* **shortcutId** - The ID of the shortcut. (Surprise! Surprise!)
* **enabled** - The current state of the shortcut. It can be either **true** or **false**. If the shortcut is disabled it won’t appear in the list with shortcuts.
* **shortcutShortLabel / shortcutLongLabel** - The labels which contain the name of the shortcut. Their length is limited. You can check the ‘Limitations’ section for more info. Usually the short one is used when the shortcut is pinned to the home screen. The long label is used for the app shortcut menu.
* **shortcutDisabledMessage** - The message, which is shown to the user when a disabled pinned shortcut was selected.

In the current version of the app, the **shortcutDisabledMessage** will never be displayed, because non of the shortcuts gets ever disabled.

As you probably noticed, we must declare the things these shortcuts will do. The **intent** tags hold the info for each task associated with each shortcut. We can even set multiple intents for each shortcut. In this way, we can easily populate the backstack of the app. The last intent will be on the top of the stack.

> Each intent must have an action! Otherwise, the app will crash!

To use these static shortcuts in our app, we must declare them in our AndroidManifest as well (see rows #20 — #22).

{{< gist kostovtd 8173e632d66396db24a28f33a97ec83f >}}

## Dynamic shortcuts

The dynamic shortcuts are constructed while the application is running. We can add, remove and update shortcuts as many times as we want. This dynamic feature gives us the possibility to be creative. We can apply some sort of algorithm to figure out which parts of our app are most suitable for having a shortcut version. The following [Activity](https://developer.android.com/reference/android/app/Activity.html) figures out which is the most used phone number by using the [SharedPreferences](https://developer.android.com/reference/android/content/SharedPreferences.html) and creates a shortcut for it.

{{< gist kostovtd 5d97afa8bf65a800726fb8b3975c0ca9 >}}

The most interesting part of this code is in the **createJackShortcut** and **createJillShortcut** methods. These two methods create different dynamic shortcuts. They use objects of type [ShortcutInfo](https://developer.android.com/reference/android/content/pm/ShortcutInfo.html). These object are something like the Java representation of the static XML shortcuts from the previous section. By using a simple [Builder](https://developer.android.com/reference/android/content/pm/ShortcutInfo.Builder.html) class we can set the same properties like the one in our XML file. To publish a list of dynamic shortcuts we must have an instance of the [ShortcutManager](https://developer.android.com/reference/android/content/pm/ShortcutManager.html) (see row #33). The [setDynamicShortcuts](https://developer.android.com/reference/android/content/pm/ShortcutManager.html#setDynamicShortcuts%28java.util.List%3Candroid.content.pm.ShortcutInfo%3E%29) method is responsible for publishing the given shortcuts (see row #93).

> Just like with the static shortcuts, each dynamic shortcut must have an intent with an action. If not, the app will crash!

In the **createDynamicShortcuts** method we simply compare the current usage of our shortcuts. The usage is saved thanks to the SharedPreferences (see the **trackShortcutUsage** and **getShortcutUsage** methods). In our **onCreate** method there is a simple check if the dynamic shortcuts are missing (see rows #34 — #37). If they are missing, then we need to create them again. This is a valid case, when the app was restored after a backup. After restoring the app from a backup, all it’s info is downloaded from the Google Cloud and we must provide the same user experience as before.

> Since Android 6.0 the backup option is enabled by default.

## Design Guidelines

Not surprisingly, there are some available guidelines about App Shortcuts in regards of their UI. This time there are not in the form of a web page, but they are distributed as a **.pdf** file. You can find a link to it in the ‘Resources’ section. Some of the advises are:
* Stick to the Material Design as much as possible.
* If using system icons, there size should be **24 x 24 (dp)**.
* Use **SVG** icons for automatic scaling.

## Limitations

Believe it or not, there are some limitations about how we can use App Shortcuts. According to the official Android documentation, the current API supports up to five different shortcuts at any given time. **BUT** it is highly recommended to use maximum four of them. Also, there are limitations to the length of the short and long description for each shortcut. Because of the limited space for the shortcut items, it is recommended to use no more than 10 characters for the short description and no more than 25 for the long one.

Another limitation is the launcher of the current device. Not all launchers support App Shortcuts yet. Thus, before releasing this new feature we must test it on as many different launchers as possible. Also, there is a limit on how often we can update our dynamic shortcuts, when our app is in the background. When the app is brought back to the foreground, that limit is reset automatically. It can be also reset manually from **Settings -> Developer Options** or with the help of a small ADB command:

```
adb shell cmd shortcut reset-throttling [ — user your-user-id ]
```

And last, but not least, only the static shortcuts can be restored after a successful backup of the device. The dynamic ones will be lost and must be recreated again, when the app starts.

## Resources

* App Shortcuts Design Guidelines - https://commondatastorage.googleapis.com/androiddevelopers/shareables/design/app-shortcuts-design-guidelines.pdf
* AppShortcuts Example App Git Repo - https://github.com/kostovtd/AppShortcuts
* Konstellations Example App Kotlin Git Repo - https://github.com/AOrobator/Konstellations

## References

* https://medium.com/@andreworobator/implementing-android-app-shortcuts-74feb524959b#.cwl4dmt5h
* http://fragmentedpodcast.com/episodes/72/
* https://www.novoda.com/blog/exploring-android-nougat-7-1-app-shortcuts/
* https://developer.android.com/guide/topics/ui/shortcuts.html

Feel free to share, comment & give your opinion on the topic!