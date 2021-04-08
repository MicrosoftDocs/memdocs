---
# required metadata

title: Reset device passcode from Intune Company Portal website | Microsoft Docs
description:
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/26/2021
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
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
---

# Reset device passcode from Company Portal website

If you lose your device PIN or password, you can use the [Company Portal website](https://portal.manage.microsoft.com) to reset it. 

The reset passcode option might not appear for a corporate-enrolled device. In this case, contact your company support to have it reset for you.  

Passcode reset can't be used on the following types of enrolled devices:

* Personally-owned device with a work profile, running Android 7.0 and later  
* Android Enterprise dedicated device, running Android 7.0 and later  
* Android device administrator device, running Android 7.0 and later  

If you forget your passcode on one of these devices, you must reset it to factory settings.  

## Reset your passcode

1. Open the [Company Portal website](https://portal.manage.microsoft.com) and select the __Menu__ button > __Devices__.  

2. Select the device that needs a passcode reset.  

    ![A screenshot of the Devices page, with two tiles that show unidentified, generically named devices. A gray banner sits directly below the devices and prompts user to identify the device they're using or add a new one.](./media/rename-reset-device-step2-1808.png) 

3. Select **Reset Passcode**. If the passcode option isn't visible at the top of your page, select **More (…)** > **Reset Passcode**.   

   ![Device details page for a selected device on the Company Portal website, with a list of links at the top showing Rename, Remove, Reset Device, Reset Passcode, and Remote Lock. ](./media/rename-reset-device-1808.png)   

    ![Screenshot of the More icon, highlighted with a red arrow.](./media/rename-reset-device-step3-more-1808.png)  

4. When prompted, click **Sign out**. When prompted again, sign back in. Sign back in to the Company Portal website within five minutes, or Company Portal won't reset the device passcode.  

   > [!NOTE]
   > You must sign back in to confirm your identity. This is to prevent malicious attempts to reset your device passcode.

   ![Example screenshots showing a prompt to sign out of the Company Portal. The buttons for user input are Sign Out and Cancel.](./media/iwp-reset-passcode-popup-1808.png)

5. A message appears to warn you that the existing device passcode is about to be removed. Click **Reset passcode** to confirm.  
    > [!WARNING]
    > After you reset your passcode, anyone who has physical access to the device will be able to access most personal and corporate information on it. If you don't currently have the device in your possession, don't reset the passcode.  

   ![Example screenshot showing second reset passcode message. Includes link to learn more about setting a new passcode in the documentation, and individual buttons to reset passcode and cancel.](./media/iwp-reset-passcode-popup2-1808.png) 

6. If you're resetting the passcode for an iOS device, its existing passcode will be removed. For Windows or Android devices, you'll be issued a temporary passcode to unlock the device and set a new passcode. 

   > [!NOTE]
   > You can find the temporary password for Windows and Android devices in the Company Portal, under the device's details page. See the section [Set up a new passcode](reset-your-passcode-cpwebsite.md#set-up-a-new-passcode) for more OS-specific passcode descriptions.  
   
7. On your device, go to **Settings** and change the temporary passcode. 

8. A flag appears in the top right of the Company Portal website. Click to read the notification and confirm that the password was successfully reset.  

## Set up a new passcode  

This section describes the passcode reset and the temporary password behavior for each device platform.  

**Android**: Removes the existing passcode and creates a temporary passcode made up of letters and numbers.

**iOS**: Removes the existing passcode and doesn't create a temporary passcode. If you use Touch ID to open your device or make purchases, you must set it up again.  

**Windows 10 Mobile**: Removes the existing passcode and creates a temporary passcode made up of letters and numbers. If set up, Windows Hello facial recognition will still work with the device.

**Windows Phone 8.1**: Removes the existing passcode and creates a temporary passcode made up of numbers.  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
