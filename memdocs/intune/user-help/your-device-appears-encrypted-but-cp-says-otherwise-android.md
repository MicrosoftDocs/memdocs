---
# required metadata

title: Your Android device seems to be encrypted | Microsoft Docs
description: Resolve encryption status in Company Portal and Microsoft Intune app
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/28/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: arnab
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Device encrypted but apps say otherwise

If Company Portal or the Microsoft Intune app say that your Android device isn't encrypted, but you're sure that it is, try the steps in this article.  

## Add a startup PIN

Certain Android devices require you to create a startup PIN for security purposes. The location of this setting will be in your device's **Settings** app. The name and location of the setting could vary. For example, on the Samsung Galaxy S7, the setting is referred to as **Secure Startup**. To enable it and create a passcode, go to **Settings** > **Lock Screen and Security** > **Secure Startup**.  

## Encrypt the entire device

This section only applies to the Company Portal app. Some devices will give you a choice between encrypting the entire device or just the used space. Choose the option to encrypt the entire device. If you selected to encrypt only the used space:

1. [Remove this device from the Company Portal](unenroll-your-device-from-intune-android.md).
2. Decrypt the used space.  
3. Encrypt the entire device.  
4. Re-enroll the device.  

## Downgrade your version of Android

This section only applies to the Company Portal app. If your device offers you the option to downgrade to Android 8.0 or later, then do so. There is a risk of data loss if you try to downgrade your device. Otherwise, we recommend that you contact your company support to resolve this issue. Get contact information for your company support on the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  

## Specific manufacturer issues

Some Android devices on version 7.0 and later encrypt data in ways that are inconsistent with certain Android platform standards. These encryption methods put device information at risk. As a result, these devices aren't supported.

For a non-exhaustive list of supported Android devices, see the article [Supported operating systems and browsers in Intune](/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices). If your device isn't listed, refer to the device manufacturer or contact your support person.

> [!Note]
> Microsoft works with manufacturers to address any issues we find while testing or that users report to us. We update this article whenever new information is available.

## Update devices

If you haven't updated your device to the most recent version of Android, go to your device's **Settings** app and select **Update**.  

## Next steps

Still need help? Contact your IT support person. Check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) or app for your organization's contact information.  
