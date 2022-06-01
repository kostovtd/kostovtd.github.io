---
author: "Todor Kostov"
title: "Geo-fencing with MVP Part 3"
date: "2016-12-18"
tags: [
    "android"
]
cover:
    image: "posts/a6mfmjcfkii-ruthie.jpg"
---

With the previous two posts, we went through the basic concepts behind the idea of geofencing, why using design patterns and we dived deeper in the main components used in the construction of the example application for these series. Now in the third part, we will go through the classes which are responsible for the core geofencing functionality. I hope you still remember the overall MVP design diagram from the previous post! The one down below seems similar to the previous one, but some additional components are included as well:

![](/overall_packages.png)

## Manager Layer

As you can see from the diagram above, the whole package consists of four different components:
* LocationCallback (interface)
* GoogleLocationApiManager
* GeofenceCallback (interface)
* GeofencingManager

Obviously, they can be separated into two groups. The first group consists of **LocationCallback** & **GoogleLocationApiManager** and the second group consists of **GeofenceCallback** & **GeofencingManager**.

Lets have a closer look at each of the two groups and their responsibilities!

The first group (LocationCallback & GoogleLocationApiManager) is responsible for providing the location awareness feature to our application. The GoogleLocationApiManager handles this process.

{{< gist kostovtd 6c82763713e17f2fe50c9f612bf88946 >}}

You probably noticed that there is something strange with the overall process of getting the last known location and so on! And you will be right! The GoogleLocationApiManager is not using the good old Android framework location APIs, but it is using Google Services instead. Why is that? Because Google strongly encourages us to use that approach.

If you are currently using the Android framework location APIs, you are strongly encouraged to switch to the Google Play services location APIs as soon as possible.

## Location manager VS Google Services

I won't go deep into the discussion of which approach is better, but I will give my two cents on the topic. Obviously, the Android Location API was present back in Android API level 1. That was long looong ago! And step by step, some more features were included in that particular package. At some point in time, the folks from Google, decided to improve even further the location-based functionality for Android. So they came up with a separated location service included in their not infamous Google Services package.

The Google Location Services API, part of Google Play Services, provides a more powerful, high-level framework that automatically handles location providers, user movement, and location accuracy. It also handles location update scheduling based on power consumption parameters you provide. In most cases, you’ll get better battery performance, as well as more appropriate accuracy, by using the Location Services API.

All in all, the new approach should handle, in a better way, some specific points like connecting, maintaining and disconnecting from the whole service suit. Of course, you can still use the built in Android Location API, if you want to. If you want to have a closer look on the topic, check [this](https://antoniohongkr.wordpress.com/2013/08/19/google-play-service-analysis-4-choice-between-google-play-location-service-and-android-location-service/) article!

The GoogleLocationApiManager class provides multiple method for handling the results of the communication between our app and Google Services.

Also it provides a basic notification mechanism in order to inform the presenter layer for any particular changes related to the user's location. Remember that the MapsPresenterImpl class acts like a hub in our app?

Here you will find a brief description of the some of the methods in the GoogleLocationApiManager class:
* onConnected() - this method is invoked when a connection between our application and Google Services was established. If you take a closer look at the constructor, you will see that this is the place where we launch our connection process. The two most important things that this method does is that it extracts the user's last know location from the service and registers the current class as the one responsible for handling location updates, pending results and so on.

```
pendingResult = LocationServices.SettingsApi.checkLocationSettings(mGoogleApiClient,mLocationSettingsRequestBuilder.build());
mLastKnownLocation = LocationServices.FusedLocationApi.getLastLocation(mGoogleApiClient);
LocationServices.FusedLocationApi.requestLocationUpdates(mGoogleApiClient, mLocationRequest, this);
```

* onConnectionSuspended() - the method is invoked whenever your app is temporarily in a disconnected state, due to problems with the remote service. The [GoogleApiClient](https://developers.google.com/android/reference/com/google/android/gms/common/api/GoogleApiClient) will automatically try to reconnect to Google Play services, but during the time, the connection is down, you should disable all UI components which rely on the service.
* onConnectionFailed() - this method is called if there was a problem when connecting your application with the Google Play services. The difference between this method and the one mentioned above is that, the **onConnectionSuspended()** is called if there was a problem with the connection **AFTER** it was established.
* onLocationChanged() - this is pretty much self explanatory. Whenever the user's location is changed, this method will be invoked, so that we will be able to handle the new location in the appropriate way - save it, update the map UI, etc.

In the next part of these series, we will have a look at the second group of entities responsible for the actual registration and addition of the predefined POJO geofences and will make a small summery of the things we already went through.

## Resources

* https://developer.android.com/training/location/index.html
* http://stackoverflow.com/questions/33022662/android-locationmanager-vs-google-play-services
* https://antoniohongkr.wordpress.com/2013/08/19/google-play-service-analysis-4-choice-between-google-play-location-service-and-android-location-service/

Feel free to share, comment & give your opinion on the topic!