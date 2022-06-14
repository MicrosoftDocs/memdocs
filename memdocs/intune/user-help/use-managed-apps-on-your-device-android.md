---
# required metadata

title: Get work or school apps for Android - Microsoft Intune | Microsoft Docs
description: Learn about managed apps and where to get Android apps for work or school.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/14/2022
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
---


# Work or school apps for Android  
Intune-managed apps (*managed* apps for short) are work and school-approved apps that are configured to prevent intentional or unintentional data loss on a mobile device. This article describes how to access your work or school data in an Intune-protected app.    

Your organization can restrict and require the use of work apps like Microsoft Outlook, Word, and Google Play. For example, if you're signed in to an app with your work or school account, your org can restrict certain features, such as copy and paste and screen capture. Policies like these help prevent sensitive work information from being shared or leaked outside of the app. 

Your organization's app protection policies are only enforced when you're using an app for work or school, like when:  

* You're signed into an app with your work account.   
* You try to access work files in OneDrive, Teams, or SharePoint.  
* You're using apps in the work profile area on your device.  


## App protection capabilities    

 An IT admin can control the following settings and features in an Android work or school app. 

* Access to specific websites  

* Access to internal company websites using Microsoft Edge and the Azure Active Directory proxy  

* Minimum version of app, version of OS

* Ability to share and transfer data between apps  

* How and where you save work files  

* Copy and paste functionality  

* PIN access requirements  

* How you sign in, using workplace credentials  

* Ability to back up data to the cloud  

* Ability to take screenshots  

* Data encryption requirements  

## How do I know I'm using a managed app?
When you sign in or try to access work data in a managed app, you'll receive an on-screen message that the app is protected by your organization. On a device with a work profile, a work app is marked with a briefcase badge.    

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
*Available* apps aren't neccessarily required for you to install, but are appropriate apps to use for work or school. You can view all available apps in the Company Portal app. Apps are made available based on device type. For example, if you're using the Company Portal app on your Android device, you'll have access to Android apps, but not iOS apps.   

### Request an app for work or school   
 If there's an app you need, but don't see in Company Portal, you can request it. You'll find contact details for your IT support person in the Company Portal app. The same contact information is available on the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).   

 ## View protected media files with Azure Information Protection app  
TheAzure Information Protection (AIP) mobile apps enable you to view protected emails, PDFs, images, and text files that cannot be opened with your regular apps for these file types. The mobile viewer app is available for Android devices on [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer).  

For more information about AIP, see [Mobile viewer apps for Azure Information Protection on iOS and Android](/azure/information-protection/rms-client/mobile-app-faq).  

