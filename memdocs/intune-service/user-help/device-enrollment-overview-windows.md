---
# required metadata

title: Overview of device enrollment for Windows - Microsoft Intune  | Microsoft Docs
description: Describes what happens after you enroll your device in Intune, for Windows 10 and later.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby 
ms.date: 06/28/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: d65e3452-5bbf-4d26-a06e-401ddcc47f39
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: priyar
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---


# About Windows device enrollment with Intune Company Portal  

**Applies to**
- Windows 10  
- Windows 11  

By enrolling your device in Intune, you get secure access to work or school apps on your mobile device, and access to apps in Intune Company Portal. The Company Portal app also monitors your device settings to make sure they meet your organization's requirements, and syncs things (like apps, policies, and updates) from your organization to your device. 

This article describes what to expect once you've enrolled your device for work. 

## What happens on all devices after enrollment  
After you enroll a device for work or school using Intune Company Portal:    

- You can access your org's network, email, and work files on the device.   

- You can install work or school apps from the Company Portal website and app, and access them by signing into your work or school account. 

- Your work or school email is automatically set up.  

- You can reset your phone to factory settings if it's lost or stolen.  

### What happens on Windows PCs after enrollment   
In addition to everything under [What happens on all devices after enrollment](device-enrollment-overview-windows.md#what-happens-on-all-devices-after-enrollment), after you enroll a Windows device in Intune:   

- Software installs on the device that enables your organization to manage the device. Your support person can automatically update this software.  

- If your organization requires it, anti-malware and virus software is installed on the device. 

- Intune requires access to the hard drive so that it can verify that the device meets device and security requirements. This is the same kind of access that Intune needs on a mobile device (for example, on an Android or iOS device).  IT support can't view or make changes to anything on your hard drive. 

- Your IT support person can install work apps and updates on your device.  

## IT support permissions   
When you enroll your device, you are giving IT support permission to:  

- Reset your device back to the manufacturer's default settings. This is helpful if the device is lost or stolen.   

- Remove work-related files and business apps. Personal data and settings aren't removed.  

- See the software installed on the device, including software you've personally installed.  

- Set requirements on your device, like requiring you to have a device password or PIN. As another example, your org could limit how many times you can enter an incorrect password, and lock you out of the device after too many failed attempts.  

- Require you to encrypt the data on your device to help protect company data, in case your device is lost or stolen.

- Require you to accept terms and conditions.

- Block you from using the device camera or screenshot feature. This restriction limits the sharing of work-related data.  

## Device syncing for updates  

Every eight hours, enrolled devices sync with Intune to get the latest updates and policies from your org. During check-in the device can: 

- Download policy or app updates.  

- Receive hardware inventory updates.  

- Receive app inventory updates.  


## Next steps  

* When you're ready to install Company Portal and enroll your device, see [Enroll Windows 10/11 device](enroll-windows-10-device.md).  

* Need additional support? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
