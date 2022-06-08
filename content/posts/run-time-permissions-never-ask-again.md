---
author: "Todor Kostov"
title: "Android tricks - Runtime permissions and the 'Never ask again' option"
date: "2018-01-12"
tags: [
    "android"
]
---

With Android 6.0 (API 23) users are able to grant app permissions during run time. That new feature made our developer lives a bit more difficult, but gave huge powers to our users. And do you remember that little check box which says 'Never ask me again'?

![](/rqqyp.png)

Yep... this particular one! So, how can we know that this check box had ever been selected by the user? Actually, it's not that difficult! There is a method called [shouldShowRequestPermissionRationale](https://developer.android.com/reference/android/support/v4/app/ActivityCompat.html#shouldShowRequestPermissionRationale(android.app.Activity,java.lang.String)). This method has a boolean return type. It returns:
* **true** - if the app has requested this permission previously and the user denied it without selecting the 'Never ask me again' checkbox
* **false** - if the permission was denied together with the checkbox being checked

So, if this method returns **false**, then we can be sure that the checkbox was selected and we can show a dialog to the user and navigate him / her to the phone settings where he / she can enable that permission.

{{< gist kostovtd 753c86772f9820ee0dee4564faa142e8 >}}

Sadly, as of this date, the official Android documentation for this method does not represent the reality. Right now, this method accepts only the String parameter. The Activity parameter is currently missing.

## Resources

* https://stackoverflow.com/questions/30719047/android-m-check-runtime-permission-how-to-determine-if-the-user-checked-nev

Feel free to share, comment & give your opinion on the topic!