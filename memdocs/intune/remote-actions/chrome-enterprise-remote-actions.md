---
# required metadata

title: Remote actions for ChromeOS devices | Microsoft Intune  
description: Remotely run Microsoft Intune device actions on ChromeOS devices in the Microsoft Intune admin center.   
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/26/2022  
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shsivak
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Remote device actions for ChromeOS   

Remotely run device actions on ChromeOS devices synced with Microsoft Intune. There are four remote actions supported on ChromeOS devices:  

* Deprovision  
* Lost mode, known in Chrome Enterprise as *disabling a device*  
* Wipe  
* Restart (only for kiosk devices and managed guest session devices)  

To access remote actions, select a device in your **Chrome Enterprise** list or go to **Devices** > **All devices** and select a device. This article describes the remote actions, and provides information about required permissions and known issues.  

## Prerequisites     
[Set up the Chrome Enterprise connector](../enrollment/chrome-enterprise-connector-configure.md) with Microsoft Intune, and enroll devices using the Google Admin console. 

Permission requirements are provided in the sections that follow.  

## Deprovision  
Select **Deprovision** to remove Google Admin policies from devices your organization no longer uses. To deprovision a ChromeOS device, you must be assigned a role that has the *Remote tasks: Retire* permission.  

After you deprovision a device, it remains in the Intune admin center and the Google Admin console. Then on the admin center **System info** page, the device status changes to **DEPROVISIONED**. The device can't be enrolled again until you restore it to factory settings. For more information about the deprovision action, such as how to select the best reason for deprovisioning, see the [Chrome Enterprise and Education Help documentation](https://support.google.com/chrome/a/answer/3523633?).  

## Lost mode  
Select **Lost mode** to prevent other people from using a lost or stolen ChromeOS device. Devices in lost mode display the contact information and message you configured in the Google Admin console. To deprovision a device, you must be assigned a role that has the following permissions:  

* *Remote tasks: Enable lost mode*     
* *Remote tasks: Disable lost mode*        

>[!TIP]
> Chrome Enterprise and the Google Admin console refer to devices in lost mode as *disabled*. For more information about how to disable a device, see the Chrome Enterprise and Education Help documentation. 

 ## Wipe   
 Select **Wipe** to remove data from a device. With this action, you can either: 
 
 * **Remove user profiles only**: This option removes all user account data. Device and enrollment policies remain on the device.  
 * **Factory reset (powerwash)**: This option fully restores a device to its factory state, removing all personal and work data. Before using this action, [deprovision](chrome-enterprise-remote-actions.md#deprovision) the device. Otherwise, once it connects to Wi-Fi, it will automatically enroll again.  
 
To wipe a device, you must be assigned a role that has the *Remote tasks: Wipe* permission. For more information about wiping ChromeOS devices, see [Wipe ChromeOS device data](https://support.google.com/chrome/a/answer/1360642) (opens Google Chrome Enterprise Help).    

## Restart  
Select **Restart** to restart a device. To restart a device, you must be assigned a role that has the *Remote tasks: Reboot now* permission.  

>[!IMPORTANT]
> Device users aren't automatically notified of restarts, and might lose unsaved work if you don't tell them about it ahead of time. 

Restart is only available for kiosk devices and managed guest session devices. The restart fails on any other type of device. For more information, see [Kiosk apps, managed guest sessions, and smart cards](https://support.google.com/chrome/a/topic/6128720?) (opens Google Chrome Enterprise Help).  

## Bulk device actions   
You can issue all of these remote actions as part of a bulk device action. For more information about how to do that, see [Use bulk device actions](bulk-device-actions.md).  

## Known issues  
In some cases, device commands remain in a pending state, even if they’ve already completed or failed. 
