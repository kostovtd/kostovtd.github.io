---
author: "Todor Kostov"
title: "Location without Google Services"
date: "2022-10-05"
tags: [
    "android"
]
cover:
    image: "/posts/pexels-s-migaj-1464143.jpg"
---

These days you will rarely find an app that doesn't have some kind of location-based functionality. Things like navigation, geofencing or location tracking are more and more common. It's all good when you can rely on Google Play Services. Sadly, that's not always the case. Sometimes the devices that your users are going to use don't have Play Services installed. Such devices can be manufactured by some weird and unknown company, can have a custom ROM installed on them, or be located in a country where Google is not allowed to operate. No matter the reason, the fact that Google Play Services are missing from the device can make the task of obtaining the user's location quit challenging. So let's try to find out what options we have to solve this problem.

There are two different ways of obtaining a location without using Google Play Services:
1. By using the Location Manager
2. By using a 3rd party Network Location Provider (NLP)

## Location Manager

This is the old school way of obtaining a location. By using the Location Manager we can choose between four different providers:
- **GPS** - a precise way to determine the current location of the user. Although there are some drawbacks. This method is a bit slow and is not suitable for indoors use. The reason is that an actual connection with at least three GPS satellites must be established. The process is called triangulation.
[https://en.wikipedia.org/wiki/Global_Positioning_System](https://en.wikipedia.org/wiki/Global_Positioning_System)
- **Network** - that's faster than using the GPS provider. It relies on using data about your current Wi-Fi or mobile network. It's not that accurate compared to the GPS provider, but it's faster and can be used indoors as well. It's an interesting process, and it was developed long before the invention of GPS. You can read more here [https://en.wikipedia.org/wiki/Mobile_phone_tracking](https://en.wikipedia.org/wiki/Mobile_phone_tracking)
- **Passive** - by using it we will get a location only if some other app had requested it. It's power efficient, but it's not reliable at all.
- **Fused (since API 31)** - it's a combination between the other providers.

{{< gist kostovtd 9bbe9352c7ef6adfc313bac193b48424 >}}

The good thing about using the Location Manager is that it is so old that it actually doesn't use the Google Play Services under the hood. 😆

## 3rd party Network Location Providers (NLPs)

These Network Location Providers work somehow in a similar fashion like the Location Manager's Network provider. The difference is that the phone sends a HTTP request with some data regarding cell tower coverage, IP address, etc. Based on this information, the corresponding service executes a search in it's database and hopefully figures out your current location.

There are multiple services out there which provide a variety of different price packages, response formats and have different limitations. These are just three suggestions:

1. [https://github.com/microg/UnifiedNlp](https://github.com/microg/UnifiedNlp) - acts as a middle ware for multiple backends which have network location features.
2. [https://ichnaea.readthedocs.io/en/latest/index.html](https://ichnaea.readthedocs.io/en/latest/index.html) - a geolocation service that uses both Bluetooth, WiFi and Cell data. The project is open only for not commercial use.
3. [https://aws.amazon.com/location/](https://aws.amazon.com/location/) - provides a huge set of maps and location based features. Although, I was not able to find a simple way of getting the current location of the user.

## Resources
* Photo by [S Migaj](https://www.pexels.com/photo/compass-on-top-of-maps-1464143/)

Feel free to share, comment & give your opinion on the topic!