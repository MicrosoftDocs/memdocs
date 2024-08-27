---
# required metadata

title: Company Portal device setting requirements for Mac | Microsoft Intune
description: Learn more about Intune Company Portal device setting requirements for Macs.     
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/04/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
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

# Company Portal device setting requirements for Macs              

This article describes the macOS device setting requirements that the Intune Company Portal can enforce on behalf of your workplace or school. Company Portal enforces these requirements on behalf of your workplace or school to ensure your device is secure while accessing their network. Requirements are specific to each organization. You only need to update the device settings that Company Portal flags.

## Device limit reached    

To prevent unauthorized access to internal data, your school or workplace might limit the number of devices you can register. If you reach the device limit, we recommend removing one of your devices or contacting your support person to increase the device limit. Your options:  

* Remove a device in Company Portal.  

* Contact your IT support person and ask if they can increase the number of devices allowed to register.  

## Identify device  

If Company Portal prompts you to identify your device during enrollment, then there is another enrolled device associated with your work account. In this case, the device was enrolled via a method other than the Company Portal app. To resolve this message, select your device from the list in Company Portal.  

If your device isn't listed:  

1. Select **new device**.  

2. Select **Continue**.  

3. Enter the last four characters of your device's serial number. For more information, see [Find the serial number of your Apple product](https://support.apple.com/en-us/102858) on Apple Support.  

## Update operating system version  
Keeping your device up-to-date lets you access the newest features, and it also ensures that your device has the most secure version of its operating system. While using the device for work or school, we recommend keeping both personal and corporate devices up-to-date with the newest versions. Before updating your device, back up all of the information on it. Keeping a backup can help you recover your data if something should interrupt any updates, or lets you transfer your information to a replacement device. 

To check your Mac for available software updates, go to **App Store** > **Updates**. Select the newest macOS update available, and then select **Update**.  

## Operating system isn't supported  
The operating system (OS) version running on your device isn't supported. It's possible that the latest version of macOS doesn't work with your organization's apps, tools, and other internal infrastructure. To resolve this issue, contact your IT support person and find out what the OS requirements are for your device.   

## Unable to get macOS device managed

If you receive these messages while trying to get your macOS device managed, contact your IT support person for help.    

**Message 1**: *We're having trouble getting your device managed. This problem could be caused if you're using a virtual machine, have a restricted serial number, or if this device is already assigned to someone else. Learn how to resolve these problems or contact your company support.*  

**Message 2**: *It looks like you're using a virtual machine. Make sure you've fully configured your virtual machine, including serial number and hardware model. If this isn't a virtual machine, please contact support.*  

Your device may be blocked from enrolling for one of the following reasons: 

* A macOS virtual machine (VM) isn't configured correctly.     

* Your organization requires that the device is corporate-owned or has a registered device serial number.     

* The device is already enrolled, and is assigned to someone else in your organization.    

Your IT support person or IT administrator can help you identify and resolve the problem that applies to your device. For contact information, check the Company Portal app or [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
