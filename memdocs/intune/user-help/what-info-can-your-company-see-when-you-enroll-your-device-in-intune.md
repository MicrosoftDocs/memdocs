---
# required metadata

title: What info can your company see when you enroll your device?
description: Describes the information on your enrolled device that's visible to your organization.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/23/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
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

**Applies to**: 
- Windows 10
- Windows 11
- Android
- iOS/iPadOS
- macOS
- Linux 

Your organization can't see your personal information when you enroll a device in Microsoft Intune, but enrolling your device makes other information, such as device model and serial number, visible to IT administrators and support people with administrator access. This article describes the information that your organization can and can't see on enrolled devices, and explains why certain data is made visible. 

> [!NOTE]
> A support person is the person or department at your organization that you're supposed to contact if you're having problems with your device. They provide technical support for device setup, enrollment, and access. An IT administrator, or *IT admin* for short, is the person or team of people that configure the Microsoft Intune device management and enrollment settings for your organization. Some IT admins also provide technical support.  

## Device ownership  

There are two types of devices we refer to in this article:    

* Personal devices: You own the device.   
* Devices configured by your organization: Your workplace or school owns the device. Also referred to as corporate-owned.  

To view the ownership type for an enrolled device, sign in to the Intune Company Portal app or website and go to **Device Details**.  

## Things your organization can never see

Your organization can't see:  

- Calling and web browsing history
- Email and text messages
- Contacts
- Calendar
- Passwords
- Pictures, including what's in the photos app or camera roll
- Content of user created documents  

Additionally, on Android devices that have a work profile, and that are configured by your organization, they can never see: 
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
  - On devices configured by them, your organization can see all apps installed.    
  - On Android devices configured by them, your organization can only see the apps installed in the work profile.  
 
### What is a managed app? 
An app is considered a **managed app** when it's installed in one of the following ways:  
 * You install it from the Company Portal app after your organization makes it available to you. 
 * Your organization requires you to have a certain app for work and school and automatically installs it on the device upon enrollment.  

## Things your organization might see  

Your organization can see and access certain aspects of your device when assisting with or troubleshooting device setup. This section describes the type of information  available.       

### Phone number  
Your organization can see the full phone number of all devices configured by them, except for Android devices with a work profile.   

Your organization can see the last four digits of a phone number for a personal device.     

### Device storage space   
If you have trouble installing a required app, your support person may look at your storage size to find out if low space is the cause.   

### Location 

* Device configured by your organization: Your organization can view the location of a lost device. 
* Personal device: Your organization can't view the location of a personal device.   

If necessary, your organization can put an iPhone or iPad they configured into *managed lost mode*, This mode lets them request the location of the device. When someone requests access to the device location, the device locks and a message appears on the lock screen to explain what's happening. For more information about *supervision*, which is another available mode for Apple devices configured by your organization, see [Get started with a supervised iPhone, iPad, or iPod touch](https://go.microsoft.com/fwlink/?linkid=853816) in the Apple support docs.  

### App inventory details

Your organization can require you to install a mobile threat defense (MTD) app. If you're required to install an MTD app on your device:   

* Device configured by your organization: Your organization can view details about all apps on the device. 
* Personal-owned device: Your organization can't see any data, such as texts, emails, and pictures, in your personal apps. Mobile threat defense apps fo report information about your apps, such as name and version, to your organization. Your organization can view all the details about managed apps.  

For more information about mobile threat defense, see [Install mobile threat defense app](set-up-mobile-threat-defense.md).  

### App permissions  
*Applies to devices running Android 11 and earlier* 

An IT admin can grant permission to apps in the work profile, both manually and by automation. The IT admin does this to reduce the number of prompts you receive. The permissions could be for things like the camera, microphone, and location. If your device is running Android 11, you'll receive a push notification when someone grants permission to an app.

###  Network information
Some information about network connections for Android devices may be available to your organization. For example, if your organization requires devices to remain within a certain building, your device would identify the network where it's connected.  

### Additional device details

Your organization can query these details about a Windows device configured by them:  

 - Hardware and operating system environment information

 - Installed certificate details

 - File paths and file names

 - Operating system user and group information

 - Registry and event log entries

 - Details about running processes

For more information go to [Device Query](../../analytics/device-query.md)
