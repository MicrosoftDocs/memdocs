---
# required metadata

title: Reset device passcode from Intune Company Portal website | Microsoft Docs
description: Go to the Company Portal website to reset a lost or forgotten PIN on an enrolled device. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/04/2025
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 4fa3255b-9d1e-42d5-bd8b-70963dcf2d86
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: jieyang
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Reset device passcode from Company Portal website

**Applies to**:  
* Android   
* iOS/iPadOS  

Remotely reset an enrolled device's PIN or passcode. Sign in to the [Company Portal website](https://portal.manage.microsoft.com) on any device to access the *reset passcode* option. The reset passcode option can't be used on all corporate-owned devices. Contact your support person for help if the option is missing and you need to reset a device.  

>[!NOTE]
> Passcode reset doesn't work on these types of devices:  
> * Personal devices that have an Android work profile, running Android 8.0 and later  
> * Dedicated Android Enterprise work devices, such as kiosks, running Android 8.0 and later  
> * Devices utilizing Android device administrator, running Android 8.0 and later   
> 
> If you forget your passcode on one of these devices, the only way to regain access is to reset the whole device to factory settings. 

## Reset your passcode

1. Sign in to the [Company Portal website](https://portal.manage.microsoft.com).
2. Go to __Devices__.  

2. Select the device that needs a passcode reset.  

3. Select **Reset Passcode**. If the passcode option isn't visible at the top of your page, select the **More (…)** menu to see all overflow actions. 

   ![Device details page for a selected device on the Company Portal website, with a list of links at the top showing Rename, Remove, Reset Device, Reset Passcode, and Remote Lock. ](./media/reset-your-passcode-cpwebsite/rename-reset-device-1808.png)   

4. When prompted, choose **Sign out**. When prompted again, sign back in. Sign back in to the Company Portal website within five minutes, or Company Portal won't reset the device passcode. You must sign back in to confirm your identity. This step prevents malicious attempts to reset your device passcode.  

   ![Example screenshots showing a prompt to sign out of the Company Portal. The buttons for user input are Sign Out and Cancel.](./media/reset-your-passcode-cpwebsite/iwp-reset-passcode-popup-1808.png)

5. A message appears to warn you that the existing device passcode is about to be removed. Select **Reset passcode** to confirm.  
    > [!WARNING]
    > After you reset your passcode, anyone who has physical access to the device can access most personal and corporate information on it. If you don't currently have the device in your possession, don't reset the passcode.  

   ![Example screenshot showing second reset passcode message. Includes link to learn more about setting a new passcode in the documentation, and individual buttons to reset passcode and cancel.](./media/reset-your-passcode-cpwebsite/iwp-reset-passcode-popup2-1808.png) 

6. If you're resetting the passcode for an iOS device, its existing passcode is removed. For Android devices, you are issued a temporary passcode to unlock the device and set a new passcode. 

   > [!NOTE]
   > You can find the temporary password for an Android device in Company Portal. Select the device to drill down into device details.     
   
7. On your device, go to the **Settings** app and change your passcode. 

8. Select the notification that appears on the Company Portal website. Confirm that the password was successfully reset.  

## Set up a new passcode  

This section describes the passcode reset and the temporary password behavior for each device platform.  

**Android**: Removes the existing passcode and creates a temporary passcode made up of letters and numbers.

**iOS**: Removes the existing passcode and doesn't create a temporary passcode. If you use Touch ID to open your device or make purchases, you must set it up again.  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
