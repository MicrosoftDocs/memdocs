---
# required metadata

title: Managed work and school apps for Android - Microsoft Intune | Microsoft Docs
description: Learn about managed apps and where to get Android apps for work or school.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/19/2022
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: ed10a62c-b026-4ad3-ac41-641933522df2
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: chrisbal
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---


# Managed work and school apps for Android  

> [!NOTE]
> Managed apps are not currently supported on AOSP devices.  

Intune-managed apps (*managed* apps for short) are work-approved apps managed by your organization, and configured to prevent intentional or unintentional data loss. When signed into a managed app with your work or school account, you may encounter your organization's requirements and restrictions for access. This article provides an overview of Intune-managed apps, how to get the ones you need for work or school, and their restrictions and requirements.   

## How do I know I'm using a managed app?
When you sign in or try to access work data in a managed app, you'll receive a message that the app is protected by your organization. 

On a device with a work profile, a work app is marked with a briefcase badge. For more information about Android work profiles, see [Introduction to Android work profile](what-happens-when-you-create-a-work-profile-android.md).    


## App and data protection policies        

Managed apps enforce your organization's app and data protection policies, which may restrict or require: 

* Access to specific websites  

* Access to internal company websites using Microsoft Edge and the Azure Active Directory proxy  

* Minimum app and OS version  

* Ability to share and transfer data between apps  

* How and where you save work files  

* Copy and paste functionality  

* PIN access   

* How you sign in, using workplace credentials  

* Ability to back up data to the cloud  

* Ability to take screenshots  

* Data encryption requirements    

These policies prevent sensitive work information from being shared or leaked outside of your org. Restrictions and requirements are only enforced when using an app for work or school, such as when:  

* You're signed into an app with your work account.   
* You try to access work files in OneDrive, Teams, or SharePoint.  
* You're using apps in the work profile area on your device.  

## How do I install work or school apps?  

There are three ways to get work apps:   

* Install an app from the Google Play store, and then sign in to the app with your work or school account.  
* Your organization configures apps to install automatically at the time of device enrollment.  
* Your organization makes apps available to you in Company Portal.   

You don't need to enroll your device in Intune to use work or school apps, unless it's required by your organization, but you do need to have the Intune Company Portal app installed on your device.    

### Add work or school account      
Only one work or school account can be associated with the managed apps on your device. You'll see this policy enforced in the following scenarios:    

* You try to add a second work or school account. Company Portal will prompt you to remove the work account you're not using.   
* Your IT admin assigns a policy to your second account. Company Portal will prompt you to remove the work account you're not using.   

### Available apps   
*Available* apps aren't necessarily required for you to install, but are appropriate apps to use for work or school. You can view all available apps in the Company Portal app. Apps are made available based on device type. For example, if you're using the Company Portal app on your Android device, you'll have access to Android apps, but not iOS apps.   

### Request an app for work or school   
 If there's an app you need, but don't see in Company Portal, you can request it from your support person. Sign in to the Company Portal app or [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information.     

### View protected media files with Azure Information Protection app  
The Azure Information Protection (AIP) mobile apps enable you to view protected emails, PDFs, images, and text files that cannot be opened with your regular apps for these file types. The mobile viewer app is available for Android devices on [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer).  

For more information about AIP, see [Mobile viewer apps for Azure Information Protection on iOS and Android](/azure/information-protection/rms-client/mobile-app-faq).  
## View and edit default apps    
Company Portal securely saves and stores your default app selections for managed apps. To view and remove your default selections:   

1. Open Company Portal.  
2. Tap the main menu > **Settings** .  
3. Scroll down to **Default Apps** and tap **See Defaults** to view and remove your current defaults.    