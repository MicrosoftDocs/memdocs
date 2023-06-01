---
# required metadata

title: What info can your company see when you enroll your device?
description: Describes the information on your enrolled device that's visible to your organization.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/31/2022
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
ms.localizationpriority: high
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: esmich
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
---

# What information can my organization see when I enroll my device?

Your organization can't see your personal information when you enroll a device in Microsoft Intune. Enrolling your device makes certain information, such as device model and serial number, visible to IT administrators and support people with administrator access. This article describes everything your organization can and can't access on an enrolled device, and explains why certain data is made visible. 

We use the following terms in this article: 

* Support person: This is the person or department at your organization that you're supposed to contact if you're having problems with your device. They provide technical support for device setup, enrollment, and access.  
* IT administrator: *IT admin* for short, this person or team of people configure the Microsoft Intune device management and enrollment settings for your organization. Some IT admins also provide technical support.    

## Things your organization can never see

Your organization can't see:  

- Calling and web browsing history
- Email and text messages
- Contacts
- Calendar
- Passwords
- Pictures, including what's in the photos app or camera roll
- Files
- Additionally, on corporate-owned Android devices with a work profile:
  - Apps and data in your personal profile
  - Phone number 

## Things your organization can always see  

Your organization can always see:  

- Device owner
- Device name
- Device serial number
- Device model, such as *Google Pixel*
- Device manufacturer, such as *Microsoft*
- Operating system and version, such as *iOS 12.0.1*
- Device IMEI
- App inventory and app names, such as *Microsoft Word*   
  - On personal devices, your organization can only see your managed app inventory, which includes work and school apps. 
  - On corporate-owned devices, your organization can see all apps installed on the device. 
  - On corporate-owned devices with a work profile, which is limited to Android devices, your organization can only see the apps installed in your work profile.

### What is a managed app? 
An app is considered a **managed app** when it's installed in one of the following ways:  
 * You install it from the Company Portal app after your organization makes it available to you. 
 * Your organization requires you to have a certain app for work and school and automatically installs it on the device upon enrollment.  

## Things your organization might see  

Your organization can see and access certain aspects of your device when assisting with or troubleshooting device setup. This section describes the type of information  available.       

### Phone number  
If you're using a corporate-owned device (excluding corporate-owned devices with a work profile), your organization can see your full phone number. If you're using a personal device, they can see the last four digits of your phone number.  

 > [!TIP]
 > You can view the ownership type for your device on the Intune Company Portal > **Device Details** page.  

### Device storage space   
If you have trouble installing a required app, your support person may look at your storage size to find out if low space is the cause.   

### Location 

* Corporate-owned device: Your organization can view the location of a lost device. 
* Personal device: Your organization can't view the location of a personal device.   

Your organization can put a missing, corporate-owned iPhone or iPad into *managed lost mode*, which lets them request the location of the device. When someone requests access to the device location, the device locks and a message appears on the lock screen to explain what's happening. For more information about *supervision*, which is a type of configuration for corporate-owned Apple devices, see [Get started with a supervised iPhone, iPad, or iPod touch](https://go.microsoft.com/fwlink/?linkid=853816) in the Apple support docs. 

### App inventory details

Your organization can require you to install a mobile threat defense (MTD) app. If you're required to install an MTD app on your device:   

* Corporate-owned device: Your organization can view details about all apps on the device. 
* Personal-owned device: Your organization can't see any data, such as texts, emails, and pictures, in your personal apps. The MTD app does report information about your apps, such as name and version, to your organization. Your organization can view all the details about managed apps.

For more information about mobile threat defense, see [Install mobile threat defense app](set-up-mobile-threat-defense.md).  

### App permissions  
*Applies to devices running Android 11 and earlier* 

An IT admin can grant permission to apps in the work profile, both manually and by automation. The IT admin does this to reduce the number of prompts you receive. The permissions could be for things like the camera, microphone, and location. If your device is running Android 11, you'll receive a push notification when someone grants permission to an app.    

###  Network information
Some information about network connections for Android devices may be available to your organization. For example, if your organization requires devices to remain within a certain building, your device would identify the network where it's connected.  


