---
# required metadata

title: Check status in Microsoft Intune app for Android | Microsoft Docs
description: Start a status check to confirm that a device meets requirements for access, or to resolve access issues after you've made required changes.    
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/26/2023
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: d98d9bbe-98fa-48a9-8808-110435eac9e4
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: shthilla  
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Check device settings status   
*Applies to Microsoft Intune app for Android*  

Use the Microsoft Intune app to remotely check the status of a device, and confirm or resolve access issues caused by noncompliant settings. 

During a status check, the Company Portal app assesses the *device settings status* on an enrolled device, and reports whether or not the settings are compliant with your organization's requirements. If your device doesn't meet requirements, your organization may limit or restrict it from accessing internal resources. When applicable, the status provides information about how to maintain or regain access.    

>[!TIP]
> After you update the settings on a noncompliant device, we recommend running a status check to register the changes with the Intune app.     

## Check status    
To check the status of a device:  

1. Open the Microsoft Intune app for Android.  

2. Tap **Devices**, and then select your device.  

3. Tap **Check status**. Wait while the Intune app checks your device.  

The updated status appears under **Device settings status**, and the **Last checked** timestamp changes to show the date and time completed.  

## Status descriptions  

The Intune app reports the following status:         

* **Compliant**: Your device is allowed to access work or school resources.  
* **This device will soon be unable to access company resources**: Your device is allowed to access work or school resources, but one or more settings don't meet your organization's requirements. Update your device settings by the date shown to keep your access.  
* **Noncompliant**: Your device isn't allowed to access work or school resources. Make the required changes to gain access.  

## Next steps  
Requirements and next steps are determined by your organization's policies. If you're required to make any changes to your device, the Intune app will include that information next to the device settings status. For specific questions about your organization's requirements, contact your support person.   
