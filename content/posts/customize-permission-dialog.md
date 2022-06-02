---
author: "Todor Kostov"
title: "Android tricks - Is there a way to customize the permissions dialog?"
date: "2017-02-01"
tags: [
    "android"
]
---

With Android 6.0 Marshmallow a really important feature was introduced to the Android users. Yes! I'm talking about the run-time permissions. The "all or nothing" approach related to the app's permissions was wiped out. If running on Marshmallow or a later version, the users can enable and disable permissions whenever they want. And that's how the nightmare for all of us, the developers, began!

![](/screenshot-from-2017-02-01-23-52-54.png)

When going through this nightmare, have you asked yourself, if it is possible to change the UI of the dialog? I have! And the answer is **NO!**

Sadly, this is a default system dialog, thus we are not allowed to change it at all. Down below you will find what the official Android documentation has to say about that.

> **Note:** When your app calls requestPermissions(), the system shows a standard dialog box to the user. Your app cannot configure or alter that dialog box. If you need to provide any information or explanation to the user, you should do that before you call requestPermissions(), as described in Explain why the app needs permissions.

Sorry mates! I know that we are developers and that we can make miracles, but this is not the case! For now at least!

## Resources

* https://developer.android.com/training/permissions/requesting.html

Feel free to share, comment & give your opinion on the topic!
