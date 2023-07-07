---
# required metadata

title: Check compliance in Microsoft Intune app for AOSP | Microsoft Docs
description: Use the Intune app to confirm that the settings on your device meet your organization's requirements. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/17/2022
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Check compliance on your AOSP device  

Refresh the device setting status in the Microsoft Intune app to:

* Recheck compliance on a device after setting changes.   
* Get the latest compliance status on an enrolled device. 

During a refresh, the Intune app does a compliance check. It verifies that the settings on your device meet your organization's requirements, and updates the device settings status to reflect the results. A device with a noncompliant status may be restricted from accessing work resources. You can resolve access issues by updating your device settings and refreshing the device settings status. 

This article describes how to refresh the device settings status in the Intune app.  

## Check compliance  
Complete these steps to check compliance on an enrolled device. 

1. Open the Microsoft Intune app for AOSP on your device.   

2. Tap **Devices** and then select your device.  

3. Under **Device Settings Status**, tap **Refresh**.  Wait while the Intune app checks device settings.  

4. The device settings status appears as **In Compliance** or **Not in Compliance**. A compliant device can access work resources as normal. If your device is noncompliant and you're required to make changes, you receive a compliance notification in the Intune app. Tap the notification for more information.  

## Compliance notifications  
Microsoft Intune app notifications fall into two categories: 

* Device compliance: A compliance notification alerts you when your device falls out of compliance with your organization's requirements. Notifications persist until you address or resolve the issue.  
* Organizational notifications: You can receive, dismiss, and delete notifications that you receive from your organization.  
