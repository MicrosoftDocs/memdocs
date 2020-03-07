---
# required metadata

title: Encrypt Android device for Intune | Microsoft Docs
description: Steps to turn on Android device encryption when required by Intune
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
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

ms.reviewer: arnab
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---


# Encrypting your Android device

Device encryption protects your files and folders from unauthorized access if your device is lost or stolen. After you turn on device encryption, only individuals with the correct password or pin will be able to sign in to your device. 

Before you can access school or work resources, your organization might require you to encrypt your Android device. Some newer Android devices are encrypted by default, out-of-the-box.  

## Turn on encryption

If Company Portal or the Microsoft Intune app prompts you to encrypt your device, complete the following steps. 

> [!Note]
> Certain Android devices from Huawei, Vivo, and OPPO can't be encrypted. Find out more [here](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

1. Set a device screen lock.  
    a. Go to **Settings** > **Lock screen and security** > **Screen lock type**.  
    b. Select either **PIN**, **Password**, or **Pattern**.  
    c. Follow the onscreen instructions to configure your screen lock.  

2. Go back to **Lock screen and security** and select **Secure startup**.
3. Choose **Require PIN when device turns on** > **OK**.
4. Enter your PIN to confirm and encrypt your device.
5. Open the Company Portal or Microsoft Intune app.
    * Company Portal users: Select your device and tap **Check device settings**. 
    * Microsoft Intune users: You'll have to wait until the page updates, but when it does, your encryption status should change to compliant.  

Devices running Android 4.4 and earlier might not have the **Secure startup** option. In that case, complete the following steps to encrypt your device.

1. Go to **Settings** > **Security** > **Encrypt Device**. Onscreen labels vary between Android devices. If you don't see the **Encrypt Device** option, check in:
    * **Storage** > **Storage encryption**
    * **Storage** > **Lock screen and security** > **Other security settings** 

2. Follow the onscreen instructions. During encryption, your device could restart several times.
3. Open the Company Portal or Microsoft Intune app.
    * Company Portal users: Select your device and tap **Check device settings**.  
    * Microsoft Intune users: You'll have to wait until the page updates, but when it does, your encryption status should change to compliant.

## Troubleshoot  
**Issue**: You've already encrypted your device and

- The encryption button is disabled.
- You see a message saying that you still need to encrypt.
- You get errors when trying to use the Company Portal or Microsoft Intune app.

**Things to try**

- Make sure that your device is charged and plugged in.  
- Make sure that you've set a PIN or password on your device.  

Still need help? Contact your company support (check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information), or write the <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android team</a>.  
