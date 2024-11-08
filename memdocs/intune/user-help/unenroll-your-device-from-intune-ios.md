---
# required metadata

title: Remove your iOS device from Intune | Microsoft Docs
description: Describes how to remove an iOS device from Intune and how to delete stored data.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby

ms.date: 01/07/2020
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 28914db1-3e62-45f5-9632-b0d2a808a44d
searchScope:
 - User help

# optional metadata

ROBOTS:   
#audience:

ms.reviewer: andycerat
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---


# Remove device from Company Portal for iOS app

You can use the Company Portal app for iOS to remove an Intune-enrolled device so that it's no longer managed by your organization. After you remove the device:

- The device is removed from Company Portal.    
- You lose access to internal file shares and websites from your device.  
- You lose access to school or work apps from your device.    
- You might be blocked from connecting to your org's network via Wi-Fi or virtual private network (VPN).  
- Work or school email profiles are removed from the device.  
- You can't install apps for the device from the Company Portal anymore.   
- Changes to device settings (for example, disabling the camera or requiring a certain password length) are no longer required.   

## Remove a device   

Follow these steps to remove a device you no longer need for work or school from Intune.   

1. Sign in to the Company Portal app and select **Devices**.

2. Select the device you want to remove. If you only have one device, skip to step 3.  

3. Next to **RENAME**, select the ellipses menu > **Remove Device** > **Remove**.  

    ![Screenshot of the Company Portal app Devices screen, showing options after user has clicked Remove. Shows "Remove Device" button, "Factory Reset" button, and "Cancel" button.](./media/unenroll-your-device-from-intune-ios/cp_ios_unenroll_after_1804_001.png) 

    ![Screenshot of the Company Portal app Devices screen, showing options after user has clicked Remove Device button. Shows red highlighted "Remove" button, and blue highlighted "Learn More" button and "Cancel" button.](./media/unenroll-your-device-from-intune-ios/cp_ios_unenroll_after_1804_002.png)  


## Remove data collected by the Company Portal app

There are three places the Company Portal app stores local data on your device.

- **Information logs**: standard app activity data that Microsoft collects, like how long the app was open or if it's crashed, is automatically erased when you remove the device from the Company Portal.  

- **Apple analytics**: standard app crash activity data that Apple collects. This information can only be removed by resetting your device back to factory settings. This will erase all personal information on your device. To do this, open **Settings** > **General** > **Reset** > **Erase All Content and Settings**.  

- **Keychain**: your device stores your passwords and other information used for sign-ins in your Keychain. Microsoft apps share your sign-in information across any Microsoft-developed apps that you have on your device, including Microsoft Outlook and Microsoft Authenticator. Like Apple analytics, this information can only be removed by resetting your device back to factory settings. This will erase all personal information on your device. To do this, open **Settings** > **General** > **Reset** > **Erase All Content and Settings**.  


##  Next steps 

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
