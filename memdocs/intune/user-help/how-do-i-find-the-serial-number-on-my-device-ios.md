---
# required metadata

title: Device compliance and enrollment messages for Apple devices | Microsoft Intune
description: Learn more about the device compliance and enrollment messages you receive in the Intune Company Portal app.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/26/2024
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: e6c4fedc-47b6-44b1-8c59-2fb81417f978
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
- tier3
---

# Compliance and setting requirements for Apple devices          

**Applies to:**  
* iOS/iPadOS
* macOS  

Learn more about the policies the Intune Company Portal app enforces on iPhones, iPads, and Macs used for work or school.    

## Device limit reached    

To prevent unauthorized access to internal data, your school or workplace might limit the number of devices you can register. If you reach the device limit, we recommend removing one of your devices or contacting your support person to increase the device limit. Your options:  

* Remove a device in Company Portal.
* Contact your IT support person and ask if they can increase the number of devices you're allowed to register.  

## Identify Apple device  

If you're prompted to identify your device during enrollment, at least one of your devices has already been enrolled and assigned to your account using a method other than the Company Portal app. Select your device from the list in Company Portal to identify your device. 

If your device isn't listed:  
1. Select **new device**.  
2. Select **Continue**.
3. Enter the last four characters of your device's serial number. For more information, see [Find the serial number of your Apple product](https://support.apple.com/en-us/102858) on Apple Support.

## Update operating system version  
Keeping your device up-to-date lets you access the newest features, and it also ensures that your device has the most secure version of its operating system. While using the device for work or school, we recommend keeping both personal and corporate devices up-to-date with the newest versions. Before updating your device, back up all of the information on it. Keeping a backup can help you recover your data if something should interrupt any updates, or lets you transfer your information to a replacement device. 

* To check your iOS device for available software updates, go to **Settings**  and tap **General** > **Software Update**.

* To check your Mac for available software updates, go to **App Store** > **Updates**. Select the newest macOS update available, then select **Update**.  

## Operating system isn't supported  
The operating system (OS) version that's on your device isn't supported. It's possible that the latest version of iOS/iPadOS doesn't work with your organization's apps, tools, and other internal infrastruture. To resolve this issue, contact your IT support person and find out what the OS requirements are for your device.   

## Remove an existing email account 

**Applies to iOS/iPadOS only**  

If you set up your work email on your device prior to device enrollment, your organization might require you to remove the account and resync it. First, disconnect the email account that's linked to your work account. For steps, see [Add and remove email accounts on iPhone](https://support.apple.com/guide/iphone/add-and-remove-email-accounts-iph44d1ae58a/ios) (opens Apple Support).  

After you disconnect the account, sync your device in the Intune Company Portal app.  

1. Open the Company Portal app.  
2. Select your device.  
3. Select **Check status**. Wait while your device syncs your new email settings.
4. Sign in to your email with your work account.

## Reconnect compromised device  
**Applies to iOS/iPadOS only**   

A *jailbroken* device is a device that has been altered to enable unrestricted access to certain critical files. Jailbroken devices can compromise security and cause a threat to work or school data. If Company Portal detects a jailbroken device, it revokes access to work or school resources. You likely need to reset your device to factory settings to return your device to its original configuration. We recommend that you contact your IT support person for help and other possible options.   


Need additional help? Contact your IT support person. For contact information, check the Company Portal app or [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
