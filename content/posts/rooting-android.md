---
author: "Todor Kostov"
title: "Rooting Android"
date: "2017-11-23"
tags: [
    "android"
]
cover:
    image: "/posts/www_ijailbreak_com.jpg"
---

The Android OS is famous with it’s many customization capabilities. This gives us the opportunity to experiment as much as we want. We can change the look and feel of the OS, or we can dive deeper and tinker with things like GPU, CPU and other scary abbreviations. But before getting our hands dirty, we need to do something else. We need to root our phone first.

## What is rooting?

Long story short, to root your phone means to get all the privileges, permissions and goodies of an admin user. So what?! Well, the Android OS has something called a Linux kernel. Because of that, Android relies heavily on the idea that each and every user has permissions to do a certain set of actions. Of course, there is a special set of permissions called **admin** or **superuser** permissions. A user with such permissions is something like a god for the OS. This user can do everything with all the components of the system. Such security measures are widely used in other operating systems as well.

By getting all these powers and gaining superuser permissions, we can do things which would be otherwise impossible. But please remember:

![](/memegenerator_net.jpg)

## Pros and Cons of rooting

We are all humans and we all love power! But before going ALL IN for rooting your phone, you should consider it’s pros & cons. 

**Pros:**
* Get rid of all the extra apps that your phone comes with.
* Customize the overall look and feel of the OS.
* Improve performance.
* Add new functionalities to the OS.

**Cons:**
* You can brick your phone. (a.k.a. your phone can become useless)
* Decrease performance.
* Introduce new security breaches.
* Lose your warranty.
* You can brick your phone. (in case you already forgot the first point)

Obviously, you can gain a lot if you root your phone, but the risks of messing things up are real as well. Thus, please spend some time before going ALL IN.

## How to root a phone (briefly)

![](/4332143.jpg)

The process of gaining root access depends on the phone’s brand. For some devices it can be as simple as clicking a button. For others it can require a significant amount of effort. The reason for that is the fact that to gain root privileges we must exploit one or multiple security bugs in the installed Android OS. Now, these bugs can be fairly easy to find and exploit, but sometimes they can make your day really miserable.

Let’s look at the general idea behind the rooting process! There are two major ways to gain root access to your phone:
* Install **Superuser** or **SuperSU** .zip file through recovery
* Install a new custom ROM with either Superuser or SuperSU included

Now, for some of the folks who are new to this field, lets give a brief description of the terms above:
* **Superuser** or **SuperSU** - these two are root permission manager apps. They have different features, but their main purpose is the same. They manage and inform you for each app, which requires a root access. If you are not a power user, the free version of Superuser is more than enough for you.
* **Custom ROM** - in the Android world, this is a custom version of the Android OS. Because Android is an open source operating system, everyone can edit the code. Therefor, everyone can create a new custom made version of the official OS. There is a great list of custom ROMs written by teams of exceptional developers like: CyanogenMod, LineageOS, Paranoid Android, etc.
* **Recovery** - be patient young padawan! Just keep on reading and you will gain this divine knowledge as well!

![](/young_padawan.jpeg)

The following diagram represents the connection between three of the most important software components of your device: **Bootloader**, **ROM** & **Recovery**

![](/document-1.png)

* **‘Bo-bo-boot’ what?!** - The bootloader is a small program, which loads / starts either the Android OS or the Recovery. If it can NOT start the Android OS, it will try to launch the Recovery instead. The bootloader is hardware specific. This means that there are versions of it written for each specific phone model. Each bootloader has a different name (e.x. HBOOT for HTC, rrload for Motorola, etc.). Usually, the bootloader is locked. We can not play with it unless we unlock it, or replace it with a new custom one.
We need to bypass the bootloader’s security in order to make it launch the Recovery, despite the fact that the Android OS can be started successfully.
* **Recovery** - This is a small console, which has options for deleting user’s data or installing official OS updates. The stock / default recovery has very limited options. This is not the case with custom recoveries. They have a lot more features. Also, we can install unofficial software through them. The stock recovery allows only official software to be installed. If the package you want to install was not developed by the phone’s manufacturer, the stock recovery will reject it.

Because of the stock recovery’s security, we must get rid of it, if we want to install custom software. The recovery is not device specific. Thus, we can install any recovery we want. Two of the most famous one are **CWM** (ClockworkMod) and **TWRP** (Team Win).
Once we have a custom recovery up and running, we are able to install SuperSU or Superuser. Also, we can delete the stock Android OS and install a custom ROM, which contains one of the two manager apps.

## References

* https://en.wikipedia.org/wiki/Rooting_(Android)
* https://www.androidcentral.com/root
* https://forum.xda-developers.com/wiki/Rooting

Feel free to share, comment & give your opinion on the topic!Feel free to share, comment & give your opinion on the topic!