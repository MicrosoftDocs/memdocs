---
# required metadata

title: Resolve enrollment issues on Macs integrated with Jamf | Microsoft Intune
description: Resolve Intune Company Portal device registration issues on Macs managed by Jamf Pro.  
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/08/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 56771f9f-0583-4df8-b3e9-3f0d8edee172
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
- tier3
---

# Resolve Company Portal device registration errors on Macs  
**Applies to macOS**  

This article is for employees and students setting up a Mac for work or school access using Intune Company Portal, and describes how to resolve device registration issues on Macs managed by Jamf Pro. The Intune Company Portal app flags Jamf Pro-managed devices for the following device registration issues:  

* Account not onboarded.  
* Device is already enrolled.  

## Account not onboarded

For a device to successfully enroll and register for work, you must use Jamf Self Service to open the Intune Company Portal. If you open the Company Portal app any other way, the device enrolls and registers without its connection to Jamf, which results in the *Account not onboarded* message.  

To resolve this issue, exit Company Portal. Then open the Jamf Self Service app and select the Company Portal app that's available there to begin device registration.    

## Device is already enrolled   
The following actions may result in multiple instances of your device showing up in the Intune Company Portal and failed enrollment:  
* The device you're using was previously enrolled, and it unenrolled from the Jamf service correctly but didn't successfully unenroll from the Microsoft Intune service.  
* Several attempts to register the device were made.    

Contact your support person for help with unenrolling your device, or see [Troubleshoot Jamf Pro integration- The device was previously enrolled in Intune](/troubleshoot/mem/intune/device-protection/troubleshoot-jamf#cause-6---the-device-was-previously-enrolled-in-intune) for steps to properly unenroll the device. Sign into the Intune Company Portal app or [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) and go to **Help & support** for your organization's support information.  
