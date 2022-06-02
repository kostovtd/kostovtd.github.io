---
author: "Todor Kostov"
title: "Geo-fencing with MVP Part 4"
date: "2016-12-26"
tags: [
    "android"
]
cover:
    image: "posts/vvgvlh1d10u-slava-bowman.jpg"
---

Here we are, at the last, fourth part of the series about Geofencing and MVP. In this last article we will talk about the actual registration and addition process of the predefined POJO geofences. Aaand we will make a short summery of the articles up till now.

In [part 3](https//kostovtd.com/posts/geo-fencing-mvp-part3/) we said that there are two different groups of entities in the **manager** package. The first group is responsible for providing the location awareness logic for our app, and the second is responsible for handling the actual geofencing functionality. This includes registration and addition of geofences and handling events based on some predefined parameters.

The entities related to the second group are **GeofenceCallback** (interface) and **GeofencingManager**.

{{< gist kostovtd 4d76bf3214c174aba56b7d913a77df70 >}}

As you can see, there is nothing complicated about the above interface. There is a single method in it, called **onGeofenceResultAvailable()** which is called once the geofence objects are registered. The GeofenceCallback interface is implemented by the MapsPresenterImpl class. This is our hub, remember? Once the method in MapsPresenterImpl is fired, our presenter layer will inform the view layer that a list of geofences was successfully registered, thus the view must update it's state.

Now, the more interesting part of the code is in the **GeofencingManager** class.

{{< gist kostovtd acd0789e991d4a2c4be604cf3ebf146d >}}

Here is a brief description of most of the methods in the class shown above:
* **addGeofences()** - the name is pretty self-explanatory. This method simply registers a bunch of predefined geofence objects in Google Services and also registers the current instance of the GeofencingManager as a listener for the result of registering the given list of geofences.
* **removeGeofences()** - this method does exactly the opposite. It unregisters the predefined geofences from the Google Services.
* **getGeofencingRequest()** - the method does exactly one thing - builds / creates a [GeofencingRequest](https://developers.google.com/android/reference/com/google/android/gms/location/GeofencingRequest) by using the [Builder Pattern](https://en.wikipedia.org/wiki/Builder_pattern). The GeofencingRequest contains the actual list of predefined geofences and the trigger for events. In this case the trigger is the user entering the geofence area.
* **getGeofencePendingIntent()** - the function creates and returns a [PendingIntent](https://developer.android.com/reference/android/app/PendingIntent.html) that will start a service. The actual implementation of the service is in **GeofenceTransitionsIntentService** and is included in the public Git repository for this project.
* **onResult()** - the last method is invoked whenever there is a result from a [GoogleApiClient](https://developers.google.com/android/reference/com/google/android/gms/common/api/GoogleApiClient) opperation and simply notifies the presenter layer for the result.

## Event triggers

As it was said before, the idea of geofencing relies a lot on some predefined events. Whenever such a predefined event occurred, you can do whatever you want, based on this event. There are three major event triggers available for us:
* [GEOFENCE_TRANSITION_DWELL](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.html#GEOFENCE_TRANSITION_DWELL) - whenever a user enters a geofence and stays in it's boundaries for some predefined time, an event will be triggered.
* [GEOFENCE_TRANSITION_ENTER](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.html#GEOFENCE_TRANSITION_ENTER) - at the moment when the user entered the predefined geofence area, an event will be triggered.
* [GEOFENCE_TRANSITION_EXIT](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence.html#GEOFENCE_TRANSITION_EXIT) - at the moment when the user exit the predefined area, an event will be triggered.

Although, there are just three event triggers, you can combine them and they are more than enough for us to put the overall UX on a whole new level.

[Here](https://github.com/kostovtd/GeofenceExample) is a link to the public Git repository with the source code of the example application, which we used across the articles. There you will notice that there is another package called **service** which contains a single class. That class is a simple [IntentService](https://developer.android.com/reference/android/app/IntentService.html) which is responsible for creating notifications for each triggered event. It was not discussed in details, because it is out of the scope of these articles.

As an improvement to the code shared above, you can add support for a proper handling mechanism of runtime permissions. You know that this great feature was introduced in Android 5.0 and requires some additional effort from us - the developers. You can check [these](https://blog.stylingandroid.com/permissions-part-1/) several articles on that topic. Mark Allison, the author of the articles, definitely knows a thing or two about Android!

## Conclusion

And finally the end of these series is here! Let's see a brief description of all of the four articles up till now:
* [Part 1](https://kostovtd.com/posts/geo-fencing-mvp-part1/) - in the first part we made a short introduction of the idea of geofencing. Also, we talked a bit about the advantages of using design patterns and presented the overall architecture of the example application used across the articles.
* [Part 2](https://kostovtd.com/posts/geo-fencing-mvp-part2/) - in the second part we went through the classes in each of the three layer of the MVP design pattern.
* [Part 3](https://kostovtd.com/posts/geo-fencing-mvp-part3/) - the third part was related to the way of implementing the location awareness functionality into your app and the different methods we can use in order to achieve that.
* Part 4 - the last fourth article was about the process of registering and adding our predefined geofences to the Google Services and the map on our app.

At the end, I want to thank you for your time and attention, for going through all of the four articles (hopefully)! Also, I will appreciate it, if you want to suggest an improvement, or point out a particular error in the code used through the series, or just to give your feedback on the good and bad parts of these articles! I'm a hard believer in the idea that there is always some room for improvements, so feel free to share your thoughts!

Feel free to share, comment & give your opinion on the topic!