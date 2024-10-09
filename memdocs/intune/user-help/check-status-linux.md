---
# required metadata

title: Check device status in Microsoft Intune app for Linux | Microsoft Docs
description: Verify work access and resolve compliance issues in the Intune app for Linux. 
keywords: 
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/08/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: ilwu 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Check status in Microsoft Intune app for Linux  

You can use the Microsoft Intune app for Linux to resolve access and compliance issues for enrolled devices. This article describes how to:  

* View the status of a device  

* View and resolve compliance issues with your device settings   

* Refresh device status  

## View device status  

The Intune app routinely checks in with your device to verify that it complies with setting requirements. Check-ins occur at the time of enrollment, and thereafter whenever you're using your device for work. The status reveals the result of the last check-in. To view the status of a device, sign in to the Intune app and select the device. 

There are three statuses in the Intune app:  

 * **Compliant** – Your device meets your organization’s requirements. It should have access to work or school resources.   

 * **Checking status** – Intune is checking the device settings.     

 * **Not compliant** – Your device doesn't meet your organization’s requirements. It may be restricted from accessing work or school resources. Additional action is needed from you to update your settings.  

## View compliance issues 

To view compliance issues: 


1. Sign in to the Intune app. 

2. Select a device.  

3. On the device details page, select **View Issues**. This option is only available when issues are present.  

The app shows you the following information:  

  * The action required, such as *Upgrade your operating system*. 

  * The reason for noncompliance, such as *This device’s operating system is not supported*. 

  * The **How to resolve this** link that, when available, points to a help article on learn.microsoft.com.  

### Operating system and version 
When OS and version requirements are enforced, devices running Linux flavors or versions that aren't supported are marked as noncompliant. To resolve this issue, upgrade to or install a version that’s supported by your organization.  

Contact your support person for more information about your organization’s OS requirements.  

### Password complexity 

When password complexity requirements are enforced, devices with weak passwords are marked as noncompliant. To resolve this issue, update your device password so that it meets your organization’s requirements for length and quality.  

### Device encryption  
When encryption requirements are enforced, devices that aren’t encrypted are marked as noncompliant. To resolve this issue, encrypt the local data on your device in accordance with your organization’s encryption policies. 

Not all filesystem partitions need to be encrypted:    

  * Read-only partitions are ignored. 

  * Pseudo-filesystems (such as */proc* or *tmpfs*) are ignored. 

  * The */boot* or */boot/efi* partitions are ignored.  

Intune supports all encryption systems that use the [*dm-crypt* subsystem](https://gitlab.com/cryptsetup/cryptsetup/-/wikis/DMCrypt), the standard underlying infrastructure for Linux systems. We recommend setting up dm-crypt by using the *LUKS format* with the *cryptsetup tool*.  
