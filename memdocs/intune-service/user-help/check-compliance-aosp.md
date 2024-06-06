---
# required metadata

title: Check compliance in Microsoft Intune app for AOSP | Microsoft Docs
description: Use the Intune app to confirm that the settings on your device meet your organization's requirements. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/15/2023
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: abigailstein
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Check compliance in Microsoft Intune app for AOSP 

*Applies to Microsoft Intune app for AOSP*  

Use the Microsoft Intune app to remotely check the compliance status of an enrolled device, and confirm or resolve access issues caused by noncompliant settings. During a status check, the Intune app checks your device settings to make sure they meet your organization's requirements. If your device isn't compliant with requirements, your organization might limit or restrict it from accessing work resources until you make changes.  

>[!TIP]
> After you update the settings on a noncompliant device, start a compliance check to register the changes with the Intune app.   

## Compliance notifications  
Microsoft Intune app notifications fall into two categories: 

* Device compliance: A compliance notification alerts you when your device falls out of compliance with your organization's requirements. Notifications persist until you address or resolve the issue.  
* Organizational notifications: You can receive, dismiss, and delete notifications that you receive from your organization.  

## Check compliance  
Complete these steps to check compliance and refresh the device settings status on an enrolled device. 

1. Open the Microsoft Intune app for AOSP on your device.   

2. Tap **Devices** and then select your device.  

3. Under **Device Settings Status**, tap **Refresh**.  Wait while the Intune app checks device settings and updates the device settings status.  

4. If your device is noncompliant and you're required to make changes, you receive a compliance notification in the Intune app. Tap the notification for more information.  

## Device settings status  

The device settings status tells you the following information about your enrolled device:    
* **Compliant**: Your device is allowed to access work or school resources.  
* **Can access resources, but action required**: Your device is allowed to access work or school resources, but one or more settings don't meet your organization's requirements. Update your device settings by the date shown to keep your access.  
* **Not compliant**: Your device isn't allowed to access work or school resources. Make the required changes to gain access.  
