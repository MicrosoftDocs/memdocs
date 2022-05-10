---
# required metadata

title: What info can your company see when you enroll your device?
description: Explains what IT can and can't see on your managed device.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/10/2022
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
---

# What information can my organization see when I enroll my device?

Your organization cannot see your personal information when you enroll a device in Microsoft Intune. Enrolling your device does make certain information, such as device model and serial number, visible to your support person. Other information is only accessible to your support person in certain situations to help with resolving a device or app issue.   

This article describes everything a support person can and can't access on an enrolled device, and provides explanations for why certain data *might* be visible.   

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

 > [!NOTE]
 > Organizations cannot see all app inventory on Android Enterprise fully managed devices, corporate-owned work profile devices, and dedicated devices.  
 
### What is a managed app? 
An app is considered a **managed app** when it's installed in one of the following ways:  
 * You install it from the Company Portal app after it's made available by your support person, an Intune admin.
 * Your organization requires you to have a certain app for work and school and automatically installs it on the device upon enrollment.  

## Things your organization might see  

At times, your organization may need to review data about an enrolled device to help with enrollment, troubleshooting, or finding a lost device. This section describes the information they could view and why.   

### Phone number  
If you're using a corporate-owned device (excluding corporate-owned devices with a work profile), your full phone number is visible to your organization. If you're using a personal device, the last four digits of your phone number are visible. 

 > [!TIP]
 > You can view the ownership type for your device on the Intune Company Portal > **Device Details** page.  

### Device storage space   
If you can't install an app that's required for work or school, your organization can view your storage size to figure out if space is too low.   

### Location
Your organization can access the location of a device to the following extent:  

* Corporate-owned device: Your organization can view the location of your lost device. 
* Personal device: Your organization can't view the location of your device, ever.   

A support person can put a corporate-owned iPhone or iPad into *managed last mode*, which lets them request the location of a missing device. When a support person requests access to your device's location, the device locks and a message appears on the lock screen to explain what's happening. For more information about *supervision*, which is a type of configuration for corporate-owned Apple devices, see [Get started with a supervised iPhone, iPad, or iPod touch](https://go.microsoft.com/fwlink/?linkid=853816) in the Apple support docs. 

### App inventory details

You might be required to install a mobile threat defense (MTD) app as part of your organization's security requirements. If your organization requires you to install an MTD app on your: 

* Corporate-owned device: Your support person can view details about all apps on the device. 
* Personal-owned device: Your support person can only view the details of your managed apps.  

For more information about mobile threat defense, see [Install mobile threat defense app](set-up-mobile-threat-defense.md).  

### App permissions  
Your IT administrator can automatically grant permissions to apps in your work profile. The permissions could be for things like the camera, microphone, and location. If they grant permission to an app that belongs to your organization, they could see that you installed the app. This applies to devices running Android 12.0 and earlier.  

 > [!TIP]
 > If your device is running Android 11 or later, you'll receive a push notification when your IT administrator grants permissions to an app.    

###  Network information
Some information about network connections for Android devices may be available to your organization support. For example, if your organization requires devices to remain within a certain building, your device would identify the network where it is connected.  


