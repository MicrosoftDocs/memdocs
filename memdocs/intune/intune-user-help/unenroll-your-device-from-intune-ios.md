---
# required metadata

title: Remove your iOS device from Intune | Microsoft Docs
description: "Describes how to remove an iOS device from Intune"
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby

ms.date: 04/02/2018
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 28914db1-3e62-45f5-9632-b0d2a808a44d
searchScope:
 - User help

# optional metadata

ROBOTS:   
#audience:
#ms.devlang:
ms.reviewer: esmich
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---


# Remove your iOS device from Intune

When you remove your iOS device from Intune, your device will no longer be able to access company resources and will no longer be managed by Intune.


## Removing the device from My Devices

To remove your device from Intune, use these steps or watch this video:


1. In the Company Portal app, tap **Devices.** and select the device you want to unenroll. If you only have one device, when you tap **Devices**, you will go directly to the device details screen.

2. Next to **RENAME** tap the ellipses button > **Remove Device** > **Remove**.  

    |![Screenshot of the Company Portal app Devices screen, showing options after user has clicked Remove. Shows "Remove Device" button, "Factory Reset" button, and "Cancel" button.](/intune-user-help/media/cp_ios_unenroll_after_1804_001.png)|

    |![Screenshot of the Company Portal app Devices screen, showing options after user has clicked Remove Device button. Shows red highlighted "Remove" button, and blue highlighted "Learn More" button and "Cancel" button.](/intune-user-help/media/cp_ios_unenroll_after_1804_002.png)|


    When you unenroll your device from Intune, here's what happens:

    - Your device won’t appear in the Company Portal anymore.

    - You can’t install apps from the Company Portal anymore.

    - Any settings that were changed on your device when you added it (for example, disabling the camera, or requiring a certain password length) will no longer apply.

    - You might not have access to some company resources, such as file shares or internal web sites, on your device anymore.

    - You can’t use company apps and company data on your device anymore.

    - You might not be able to connect to your company network using Wi-Fi or a virtual private network (VPN) anymore.

    - Company email profiles are removed from the device.

    - Devices that are configured for email only won't appear in the Company Portal app or website anymore.

    - Apps are uninstalled. Company app data is removed.

## Removing data collected by the Company Portal app

There are three places the Company Portal stores local data on your device.

- **Information logs**: standard app activity data that Microsoft collects, like how long the app was open or if it's crashed, is automatically erased when you remove the device from the Company Portal.

- **Apple analytics**: standard app crash activity data that Apple collects. This information can only be removed by resetting your device back to factory settings. This will erase all personal information on your device. To do this, open **Settings** > **General** > **Reset** > **Erase All Content and Settings**.

- **Keychain**: your device stores your passwords and other information used for sign-ins in your Keychain. Microsoft apps share your sign-in information across any Microsoft-developed apps that you have on your device, including Microsoft Outlook and Microsoft Authenticator. Like Apple analytics, this information can only be removed by resetting your device back to factory settings. This will erase all personal information on your device. To do this, open **Settings** > **General** > **Reset** > **Erase All Content and Settings**.


Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
