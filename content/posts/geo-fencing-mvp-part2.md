---
author: "Todor Kostov"
title: "Geo-fencing with MVP Part 2"
date: "2016-12-11"
tags: [
    "android"
]
cover:
    image: "posts/yg8cz-i5u30-stephen-monroe.jpg"
---

In the [previous post](https://kostovtd.com/posts/geo-fencing-mvp-part1/), we talked about the idea behind geo-fencing, why is it so useful and what is the reason behind choosing a particular design pattern like MVP. It was most like an introductory step before getting our hands dirty with some actual source code. Thus, in this part of the series, I will try to go through the different layers of the MVP pattern and will try to explain as much as possible the things that are happening there.

## The GeofenceExample application
As said earlier, the application which will be used as an example will rely on the usage of predefined geo-fences with some radius. The main task is to display these geo-fences on a map and fire events each time we enter or exit the predefined radius of such a location. Lets see the main classes separated by layers based on the MVP design pattern:

![](/overall_mvp.png)

## Model Layer

This is the most simple layer of all of them. It consists of a single class called **CompanyLocation**. This is a simple POJO which contains a [LatLng](https://developers.google.com/android/reference/com/google/android/gms/maps/model/LatLng) and [Geofence](https://developers.google.com/android/reference/com/google/android/gms/location/Geofence) fields. It represents a single company which has particular GPS coordinates and contains a geofence in it. That's all!

{{< gist kostovtd 74f60e3b9ee252daa25040f65af96b15 >}}

## View Layer

The View layer consists of **MapsActivity** and **MapsView** (interface). In other words, the single activity we have will be our actual view. It's responsibilities will be only to show / hide information and controls from the screen and to initialize the entities from the Presenter layer.

{{< gist kostovtd b6cf912ca01c3e56916c247b92529877 >}}

{{< gist kostovtd 2263b3af944aebded7eaa99ac4c85ac6 >}}

The **MapsView** is a simple interface which describes the major actions which the **MapsActivity** is responsible for.

## Presenter Layer

The number of the entities in the Presenter Layer is no different than the number in the View Layer. Again we have just two items in here - a simple interface and a class which implements it. Now, the **MapsPresenterImpl** class, which implements **MapsPresenter**, is a bit more complicated. That's due to the fact that this class is playing the role of a hub. It contains instances of all of the components in the application and is distributing responsibilities and tasks to the right places.

{{< gist kostovtd 4d3b214308fa4e9162d88f9d61c447c0 >}}

{{< gist kostovtd 88ac5310c53afc10fbf6dbe8db2c8ef1 >}}

The **MapsPresenterImpl** class also contains a function for 'fetching' data from e remote server. But in order to keep the example as simple as possible, the actual communication with a server is replaced by manually creating some dummy **CompanyLocation** objects and including them in a List.

Despite acting like a hub, the **MapsPresenterImpl** class is also listening for several important events to occur. Such events are:
* A change in the user's location - when a new location is registered, the pointer of the user's current location on the MapView must be updated.

```
public void onLocationChanged(Location location)
```
* A successfully established connection to the Google Location Service

```
public void onLocationApiManagerConnected()
```
* A successful result from the Google Geofencing API
```
public void onGeofenceResultAvailable()
```

Feel free to share, comment & give your opinion on the topic!