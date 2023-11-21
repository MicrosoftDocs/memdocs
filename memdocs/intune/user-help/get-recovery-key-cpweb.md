---
# required metadata

title: Get a recovery key for a macOS device from the Intune Company Portal website  
description: View the recovery key for an enrolled macOS device on the Company portal webiste.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/20/2023
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

ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Get a recovery key for a macOS device  

**Applies to macOS**  

Use the Company Portal website to get a recovery key for your locked macOS device. If you forget your device password, you can sign in to the Company Portal from another device to retrieve your key.  

## Get recovery key from Company Portal website

This option is available for Macs that were encrypted by your organization using FileVault. It's not available for Macs that you've personally encrypted.

1. On any device, sign in to the [Company Portal website](https://portal.manage.microsoft.com).
2. Open the menu and go to **Devices**.  
2. Select the encrypted Mac.  
3. Select **Get recovery key**.  

    ![Screenshot of Company Portal website, highlighting Get recovery key section.](./media/1907-recovery2-cpweb-intune.PNG)  

4. Your recovery key appears. For security reasons, the key disappears after five minutes. To see the key again, select **Get recovery key**.  

    ![Screenshot of Company Portal website, showing recovery key.](./media/1907-recovery-cpweb-intune.PNG)  

If a key isn't found but your device is properly encrypted, contact your organization's support person. For contact information, check for helpdesk details on the Company Portal website.  

## Get recovery key from Company Portal app for iOS  

Retrieve your personal recovery key (FileVault key) using the Company Portal app for iOS. This option is not available for devices that you've personally encrypted. 

The personal recovery key must belong to a device that's enrolled in Microsoft Intune, and encrypted with FileVault through Microsoft Intune. 

Using the Company Portal app, you can open the Safari web view and retrieve your personal recovery key. 

1. Open the Intune Company Portal app.  
2. Select **Get recovery key**. The Company Portal website opens in Safari and shows the key.  

    ![Screenshot of Company Portal app for iOS, showing recovery key](./media/get-recovery-key-cpweb-02.png)  

## IT pro support

If you're an IT support person and want to configure and manage FileVault encryption for macOS devices, see [Use device encryption with Intune](/intune/protect/encrypt-devices).  

## Next steps

For more information about Company Portal website features and capabilities, see [Using the Intune Company Portal website](using-the-intune-company-portal-website.md).    