---
# required metadata

title: Encrypt your Android device - Microsoft Intune | Microsoft Docs
description: Learn how to turn on Android device encryption when required by Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/23/2020
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: esmich
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---


# Encrypting your Android device

Device encryption protects your files and folders from unauthorized access if your device is lost or stolen. It makes the data inaccessible and unreadable to people who don't have a passcode. 

Before you can access school or work resources, your organization might require you to:

* [Encrypt your device](#encrypt-device)
* [Enable secure startup](#enable-secure-startup)
* [Set startup passcode, PIN, or other authentication method](#set-startup-passcode)  

> [!Note]
> Certain Android devices from Huawei, Vivo, and OPPO can't be encrypted. For more information, see [Device encrypted but app says otherwise](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## Encrypt device

Follow these steps to encrypt your device. Your device may restart several times. The name and location of the encryption option will vary depending on your device manufacturer and Android version. 

1. Open the **Settings** app.
2. Type **security** or **encrypt** in the search bar to find related settings.  
3. Tap the option to encrypt your device. Follow the onscreen instructions.  
4. When prompted, set a lock screen password, PIN, or other authentication method (if allowed by your organization). 
5. To recheck settings, open the Company Portal or Microsoft Intune app.
    * Company Portal users: Select your device and tap **Check device settings**. 
    * Microsoft Intune users: You'll have to wait until the page updates, but when it does, your encryption status should change to compliant. 

## Enable secure startup

Secure startup protects your device by requiring a password or PIN each time the device is turned on. 

The name and location of the secure startup option can vary depending on your device manufacturer and Android version. 

1. Open the **Settings** app.
2. Type **secure startup** in the app's search bar. 
    a. If that doesn't bring up a matching result, try searching for **Strong protection**. 
3. Tap **Secure startup** > **Require PIN when device turns on**.  
4. When prompted, enter your device PIN.   
5. If you're going through device setup/enrollment, return to the app and select **CONTINUE**. If you received this message outside or after enrollment:  
   * Company Portal app users: Open the app, select your device, and then tap **Check device settings**. 
   * Microsoft Intune app users: Open the app, wait until the screen loads, and then your encryption status should change to compliant.  


## Set startup passcode   
Once you encrypt your device and enable secure startup, you'll be prompted to set your device PIN, password, or other authentication method (if allowed by your organization). Competing that step will satisfy the startup passcode requirement. 

To set a lock screen on your device or change the type that you're currently using:  

1. Open the **Settings** app.
2. Type **screen lock** in the app's search bar.
3. Tap **Screen lock type**.
4. Tap the screen lock type you want to use and follow the onscreen instructions to confirm.  

## Troubleshoot    
**Issue**: The encryption button is disabled.   

**Thing to try**: 
* Make sure your device is fully charged and plugged in. Encryption may take a while and requires a full battery.   

**Issue**: You see a message saying that you still need to encrypt your device.  

**Things to try**:
   *  [Set a lock screen](#set-startup-passcode) on your device. 
   * [Enable secure startup](#enable-secure-startup).

Still need help? Contact your company support (check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information), or write the <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android team</a>.  
