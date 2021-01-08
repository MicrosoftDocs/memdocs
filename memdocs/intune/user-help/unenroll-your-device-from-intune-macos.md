---
# required metadata

title: Unenroll device in Company Portal for macOS app - Microsoft Intune | Microsoft Docs
description: Describes how to unenroll a device in the Company Portal for macOS app.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/07/2020
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: dd79fc4d-6265-4dd0-87fb-8ab66b1cf692
searchScope:
 - User help

# optional metadata

ROBOTS:   
#audience:

ms.reviewer: elocholi
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---


# Remove device from Company Portal for macOS app

You can use the Company Portal app for macOS to unenroll a device that you no longer need for work or school. Removing a device unenrolls it from Intune and removes any device restrictions put into place by your organization. 

After you remove the device, it will no longer be associated with your work or school account. So you won't be able to use it to access internal resources, such as file shares and work apps.  

This article describes how to remove a device from Intune in the Company Portal app, and how to uninstall the app on a macOS device. 

## Remove a device 
Follow these steps to remove a device you no longer need for work or school from Intune.   

1. Sign in to the Company Portal for macOS.
2. Go to **Devices** and select the device you want to unenroll.
3. From the toolbar menu, select **Devices** > **Remove**. 
4. When asked to confirm the removal, select **Remove**. The device is immediately removed from Intune. 


### What happens after device removal  

After you remove a device:

- The device is removed from Intune and Company Portal.   
- You can't install apps for the device from the Company Portal.   
- You lose access to internal file shares and websites from your device.  
- You lose access to internal apps on your device.    
- You might be blocked from connecting to your org's network over Wi-Fi or virtual private network (VPN).  
- Work and school email profiles are removed from the device.   
- Device restrictions previously enforced by Intune (for example, disabling the camera or requiring a certain password length) are no longer required.   

## Uninstall Company Portal app  
To uninstall the Company Portal app from a macOS device:

1. Open **Finder** > **Applications**. 
2. Select and drag the Company Portal app to **Trash** (located in your dock). Or select the app and then choose **File** > **Move to Trash**.  

    ![Example screenshot of macOS Finder, Applications folder, Company Portal app, highlighting "Move to Trash" option in the app menu.](./media/intune-company-portal-move-to-trash.png)  
3. If prompted to, enter your device username and password to uninstall the app. 

## Next steps  

If you change your mind and want your access back later, install the Company Portal app and go through device setup again. For detailed instructions, see [Enroll your Mac with Intune Company Portal](enroll-your-device-in-intune-macos-cp.md).  

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
