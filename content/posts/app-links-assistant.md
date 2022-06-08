---
author: "Todor Kostov"
title: "How to use App Links Assistant in Android Studio 2.3"
date: "2017-04-02"
tags: [
    "android"
]
---

With each and every new version of Android, more and more features are included into the OS. The apps become more flexible and user-friendly. Both users and developers can experiment and try new features and configurations. Of course, these boundaries can not be pushed without improving the actual tools used for developing the applications. Thus, our beloved Android Studio is evolving as well! Many bugs were fixed and new features were introduced with version 2.3 of Android Studio. One of these new features is the so called App Links Assistant.

## What is an App Link?

Before diving deeply into the actual usage of the App Links Assistant, let’s try to clarify what actually App Links are!
The app links are nothing more than simple URLs which can directly launch a specific screen of your app. No dialog will be shown to the user. Your app will just launch. Now, this can significantly decrease the user’s confusion and can increase the overall UX level.
Of course, your app will start only if a specific URL was selected. It will not start on each and every clicked URL.

## App Links Assistant
According to the official Android documentation you must complete three steps to add App Links support to your application:
* Create intent filters in your manifest.
* Add code to your app’s activities to handle incoming links.
* Associate your app and your website with Digital Asset Links.

The App Links Assistant included in Android Studio 2.3 simplifies that process. It also provides a way to test the result of following through the steps.
To start the assistant go to **Tools -> App Links Assistant**. This will open a panel with description and four distinct steps, which you must follow.


![](/81262-17gblgjemewtv3bibx_4cpw.png)

#### Step 1: Add URL intent filters

On the first step of the process you must specify the structure of the URL(s), which will be used by your app.

![](/75a9b-1jymvfcbqy8g6wvfjf9p3cq.png)

By selecting the **green cross** button, on the left side of your screen, you can add a new URL to your list.

![](/bc585-14horx52hyw6-fmd6q2i06a.png)

The window used for adding new URLs consists of three sections:
1. **Host** - The domain name of the new URL (e.x. https://kostovtd.github.io)
2. **Path** - Most probably you will have different sections of your website (e.x. Products, About Us, News). Thus, each of these sections should start a different part of your app. The path parameter helps you to differentiate between them. You can choose between three different paths — **path / pathPrefix / pathPattern**. See the ‘Resources’ section for a detailed explanation of each one.
3. **Activity** - This is a drop down list. You must select one of your activities, which will start after selecting an URL.

The result of following through this step will be some automatically generated code. It will be included into your AndroidManifest file. The assistant actually adds some [Intent Filters](https://developer.android.com/guide/components/intents-filters.html) to the selected Activity. You can preview the newly inserted code at the bottom of the window.
You can also test if the mapping actually works, by entering an URL into the input field just below the list with your URLs.

#### Step 2: Add logic to handle the intent

This step is even simpler than the previous one. Here you have to select the same Activity, which you used in Step 1. After completing this step, some code will be automatically included into your Activity class. Now, this code needs to be changed in most of the cases, because it won’t probably satisfy your current use-case.

![](/d1650-1ms7a59738urfwxxmngcmbq.png)

#### Step 3: Associate Website

This step is probably the most tricky one. Here you must generate a JSON file. It’s called a Digital Asset Links file. This file contains information about your application like **package name, SHA256 fingerprint, namespace, etc**. Most of the information needed to generate this file will be automatically populated for you.

![](/8c2c9-1uxn-ywzj0qmypho6agcc6g.png)

After generating the Digital Asset Links file, you must include it into your website. The App Links Assistant gives you the **exact** place for it.

![](/e2246-1huhdesfzmjozbaef4xs9lw.png)

If you want to make everything work, you must not rename or change the location of this file on your webpage.
Again, after completing this step, you can verify if everything is OK for now. At the bottom of the window for step 3, there is a **Link and Verify** button.

#### Step 4: Test on device or emulator

The final step is just a test to verify that you have properly integrated the whole feature.

![](/ec5a0-10u2vo-wbe3spx9nxqrgcgq.png)

By entering an URL you can run your app on an emulator and see the result.
I have created a small example on GitHub, which uses a local database ([Realm](https://realm.io/)) with some dummy data. Please note, that there are no design patterns like MVP, MVVM, etc. included in the app. This is just an example application. Thus, it’s kept as simple as possible. You can find a link to the GitHub repository in the ‘Resources’ section.
Also, if you run your application on an Android Virtual Device (AVD) you can test everything done up till now, by sending SMSs to your device. Just do the following:
1. Start your preferred AVD.
2. Expand the **Extended Controls** window (click the three horizontal dots on your AVD control panel).
3. Go to **Phone**.
4. Type **Number & Message**.
5. Click **Send Message**

## Resources

* Example application — GitHub repo - https://github.com/kostovtd/AppLinksAssistant
* (Step 2) Path parameters explained - https://developer.android.com/guide/topics/manifest/data-element.html#path

## References

* Android App Links - https://developer.android.com/studio/write/app-link-indexing.html

Feel free to share, comment & give your opinion on the topic!