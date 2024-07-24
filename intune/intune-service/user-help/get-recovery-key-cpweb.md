---
# required metadata

title: Get Mac recovery key from Intune Company Portal website  
description: Get the recovery key for your work or school device on the Company portal website.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/18/2024
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

# Get recovery key for enrolled Mac 

Get the recovery key for your locked Mac. If you forget the password on the Mac you use for work or school and are locked out, you can sign in to the Company Portal on another device to retrieve your key. 

## Get recovery key from Company Portal website

This option is available for Macs that were encrypted by your organization using FileVault. It's not available for Macs that you have personally encrypted.

1. On any device, sign in to the [Company Portal website](https://portal.manage.microsoft.com).  
2. Open the menu and go to **Devices**.  
2. Select the encrypted Mac.  
3. Select **Get recovery key**.  

    ![Screenshot of Company Portal website, highlighting Get recovery key section.](./media/1907-recovery2-cpweb-intune.PNG)  

4. Your recovery key appears. For security reasons, the key disappears after five minutes. To see the key again, select **Get recovery key**.  

    ![Screenshot of Company Portal website, showing recovery key.](./media/1907-recovery-cpweb-intune.PNG)   

## Get recovery key from Company Portal app 

This option isn't available for Macs that you have personally encrypted. The personal recovery key must belong to a device that's enrolled in Microsoft Intune, and encrypted with FileVault through Microsoft Intune.  

1. Open the Intune Company Portal app. The following apps support recovery key retrieval:  

    - Company Portal for iOS  
    - Company Portal for macOS
      
1. Go to **Devices** and select the Mac you're locked out of.  
1. On the device details page, select **Get recovery key**. The Company Portal website opens in Safari and shows the key.  After 5 minutes of inactivity, Company Portal returns you to the device details page on the Company Portal website. You can view the key again from there.    

    ![Screenshot of Company Portal app for iOS, showing recovery key](./media/get-recovery-key-cpweb-02.png)  

## IT pro support  

If a key isn't found but your device is properly encrypted, contact your organization's support person. For contact information, check for helpdesk details on the Company Portal website. 

If you're an IT support person and want to configure and manage FileVault encryption, see [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md#manage-filevault).  
