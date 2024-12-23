---
# required metadata

title: Enroll AOSP device with Microsoft Intune app| Microsoft Docs
description: Describes how to enroll a corporate-owned AOSP device in Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/24/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: jieyang  
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---


# Enroll AOSP device with the Microsoft Intune app

Enroll your corporate-owned AOSP device to get secure, mobile access to your organization's internal resources. This article describes the enrollment requirements and steps for AOSP devices.   

## Prerequisites 

AOSP devices must meet the following requirements to enroll:  

* New or factory-reset 
* Running Android 10.0 or later 
* Corporate-owned (not a personal device) 
* [A supported device](../fundamentals/supported-devices-browsers.md#android)  

Additionally, you need the enrollment QR code that's provided by your organization.  

## Enroll device  
Complete these steps to set up and enroll your device.  

1. Turn on your new or factory-reset device.  
1. If prompted to, connect to Wi-Fi. Then tap **NEXT**. 
1. When you receive the QR code, stop. Then make sure that:  

   - The QR code comes from a trusted source, via a trusted channel.  

   - You're enrolling your device into the right organization.    
1. Scan the QR code.  
1. Follow the onscreen prompts to enroll your device. 
1. If prompted to, review the device terms and conditions. Then select **ACCEPT & CONTINUE**. 
1. The Microsoft Intune app opens. The next step depends on the type of device you're using. Complete the step that matches the screen shown on your device: 

   - Tap **START** to begin enrollment.  
   - Sign in with your work account. 
      1. Enter your email, and then tap **NEXT**. 
      2. Enter your password, and then tap **SIGN IN** to begin enrollment.   
1. When you see the message that your device is ready, tap **DONE**. 

If after enrolling you have trouble accessing your organization's resources, go to the Microsoft Intune app to verify that all of your device settings meet your organization's requirements. For more information about checking compliance, see [Check compliance on your AOSP device](check-compliance-aosp.md). 
