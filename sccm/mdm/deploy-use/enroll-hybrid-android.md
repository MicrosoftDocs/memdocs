---
title: "Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune | Microsoft Docs"
description: "Prepare to manage Android mobile devices with Configuration Manager and Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe

---
# Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

For System Center Configuration Manager, users can download the Android company portal app from Google Play that lets them enroll Android (including Samsung KNOX Standard) devices. With the Android company portal app, you can manage compliance settings, wipe or delete Android devices, deploy apps, and collect software and hardware inventory. If the Android company portal app is not installed on Android devices, then you will not have all the management capabilities, such as inventory and compliance settings, but you can still deploy apps to Android devices.  

## Prepare to manage Android mobile devices with Configuration Manager and Intune  
 The following steps allow Configuration Manager to manage Android devices.  

#### To enable Android enrollment  

1.  **Prerequisites** - Before you can set up enrollment for any platform, complete the prerequisites and procedures in [Setup hybrid MDM](setup-hybrid-mdm.md).  

2.  In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscription**.  

3.  On the **Home** tab in the **Subscription** group, click **Configure Platforms** > **Android**.  

4.  In the **Microsoft Intune Subscription Properties** dialog box, select the **Android** tab and click to select the **Enable Android enrollment** checkbox.  

 Once you're set up, you'll need to let your users know how to enroll their devices. See [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). This information applies to both Microsoft Intune and Configuration Manager-managed mobile devices.

 > [!div class="button"]
 [< Previous step](create-service-connection-point.md)  [Next step >](set-up-additional-management.md)
