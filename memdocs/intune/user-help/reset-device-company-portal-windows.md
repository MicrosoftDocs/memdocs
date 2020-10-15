---
# required metadata

title: Reset device from Intune Company Portal for Windows | Microsoft Docs
description: Learn how to factory reset a used, lost, or stolen device in Company Portal for Windows 10.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/05/2020
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: jieyang
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser; intune-azure
ms.collection: 
---


# Reset device in Company Portal app for Windows  

Use the Company Portal app for Windows to reset a used, lost, or stolen device back to factory settings. All apps, settings, and personal data on the device will be deleted and the device will no longer appear in Company Portal.  

The reset option may not be available for every device that appears in Company Portal. Your organization can choose to hide the option.  


## Reset device   
To reset a device to its original, out-of-box settings:  

1. Open the Company Portal app on any managed device and sign in with your work or school account.
2. Select **DEVICES**. 
3. Select the device you want to reset.
4. Select **Actions** > **Reset**.    
5. Select **Reset** to start wiping the device.   

## Reset limitations  
Company Portal device resets aren't supported on all devices. The feasibility of a reset depends on the Windows version and how your organization configured their policies. This table lists the expected outcomes for various Windows devices and configurations.       


|Device configuration and management|Device type|
|---------------------------------------|---------------|
|Your company support manages your mobile device|**Windows 10 and Windows Phone 8.1**</br>Your device won't appear in the company portal anymore, and the company portal tries to reset the device back to the manufacturer's default settings. Your personal data, apps, and settings will be removed. <br /><br />**Windows 10 Mobile**</br>The only way to unenroll your device is to reset it.|
|Your device can access company email only|**Windows Phone 8.1**<br />Your device won't appear in the company portal anymore, and your company email account and unsaved email will be deleted.<br /><br />**Windows 7 or Windows Vista**<br />You cannot reset a computer that's running Windows 7 or earlier that's used for email only.<br /><br />**Windows 8.1 and Windows 8**<br />Your device won't appear in the company portal anymore, and your company email account and unsaved email will be deleted.|
|PCs and laptops|**Windows 8.1 and Windows 8**<br />You cannot reset a computer that's running Windows 8 or Windows 8.1 unless it's used for email only.<br /><br />**Windows 7 or Windows Vista**<br />You cannot reset a computer that's running Windows 7 or earlier.|  

## Next steps 

* You can also [reset a device from the Company Portal website](reset-device-company-portal-website.md).

* If you just want to remove your device from Company Portal, see [Remove your Windows device from management](unenroll-your-device-from-intune-windows.md). Removing the device effectively removes it from Intune and may cause you to lose access to the work-related content on your device. 

* Need additional help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
