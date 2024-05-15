---
# required metadata

title: Get BitLocker recovery key for enrolled device   
description: Get a BitLocker recovery key for your work or school device on the Company portal website.   
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

# Get recovery key for Windows    

**Applies to**:  

 - Windows 10  
 - Windows 11  

 Access the recovery key for a work or school device on the Intune Company Portal website. If you forget the sign-in password and get locked out of an Intune-enrolled PC, you can sign in to Company Portal on another device to retrieve the stored recovery key.    

You can obtain the recovery key for a work or school device that's encrypted by your organization. Recovery keys aren't available for devices you personally encrypt.  

## Requirements  

- Enrolled, BitLocker-encrypted work or school device provided by your organization  
- Registered work or school account   
- Permission to view BitLocker recovery key  

## View recovery key  

Retrieve your personal recovery key on the Company Portal website. 

1. On any device, sign in to the [Company Portal website](https://portal.manage.microsoft.com).   
2. Go to **Devices**.  
2. Select the PC you're locked out of.  
3. Select **Get recovery key**.  
4. Your recovery key appears. For security reasons, the key disappears after five minutes. To see the key again, select **Get recovery key**.  

    ![Screenshot of Company Portal website, showing recovery key.](./media/1907-recovery-cpweb-intune.PNG)  

If a key isn't found, but your device is properly encrypted, contact your IT support person for help. Check the Company Portal website for your organization's helpdesk details.   

## IT pro support

If you're an IT support person and want to configure and manage BitLocker encryption, see [Manage BitLocker policy for Windows devices with Microsoft Intune](../protect/encrypt-devices.md).  