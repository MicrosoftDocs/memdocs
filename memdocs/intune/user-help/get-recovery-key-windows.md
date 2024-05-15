---
# required metadata

title: Get Bitlocker recovery key for enrolled device   
description: Get a Bitlocker recovery key for your work or school device on the Company portal website.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
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

# View recovery key for Windows   

**Applies to**:  
 - Windows 10  
 - Windows 11  

This article describes how to retrieve the recovery key for a locked work or school device. If you forget the password on a PC you use for work or school and are locked out, you can sign in to Company Portal on another device to retrieve the stored recovery key.    

You can retrieve a recovery key for an enrolled, corporate-owned PC that's encrypted with Bitlocker. Your organization is responsible for encrypting the device. Recovery keys aren't available for devices you personally encrypt.  

## View recovery key on Company Portal website  

Retrieve your personal recovery key on the Company Portal website. 

1. On any device, sign in to the [Company Portal website](https://portal.manage.microsoft.com).   
2. Open the menu and go to **Devices**.  
2. Select the device.  
3. Select **View recovery key**.  
4. Your recovery key appears. For security reasons, the key disappears after five minutes. To see the key again, select **Get recovery key**.  

    ![Screenshot of Company Portal website, showing recovery key.](./media/1907-recovery-cpweb-intune.PNG)  

If a key isn't found, but your device is properly encrypted, contact your IT support person for help. Check the Company Portal website for your organization's helpdesk details.   

## View recovery key in Company Portal app   

Retrieve your personal recovery key in the Company Portal app. 

1. Open the Intune Company Portal app.  
2. Select the device. 
2. Select **Get recovery key**. The Company Portal website opens in Microsoft Edge and shows the key.  

## IT pro support

If you're an IT support person and want to configure and manage Bitlocker encryption, see [Manage BitLocker policy for Windows devices with Microsoft Intune](../protect/encrypt-devices.md).  