---
# required metadata

title: Enroll a Linux device in Intune| Microsoft Docs
description: Enroll a work provided Linux device in Microsoft Intune to get secure access to work or school resources in Microsoft Edge. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/04/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
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
- tier1
---


# Enroll Linux device in Intune

Enroll a Linux device in Microsoft Intune to get secure access to work or school resources in Microsoft Edge. This article describes how to enroll and register a work or school-provided device on your organization's network.   

## System requirements  

Enrollment is supported on the following versions of Linux:

* Ubuntu Desktop 24.04, 22.04 or 20.04 LTS (physical or Hyper-V machine with x86/64 CPUs)  
* RedHat Enterprise Linux 8  
* RedHat Enterprise Linux 9

Devices must be configured with a GNOME graphical desktop environment, which is automatically included with Ubuntu Desktop 22.04 and 20.04 LTS.  

Linux devices enrolled with Microsoft Intune are considered corporate-owned devices. Device enrollment isn't supported with personal devices. 

We recommend enabling encryption when you first install Ubuntu Desktop on your device. Your organization may require your device to be encrypted, and it's easiest to encrypt the device during OS installation. For help with setting up Ubuntu Desktop, see the following resources on the Ubuntu website:   

   * [Ubuntu desktop downloads](https://ubuntu.com/download/desktop) 
   * [How to install Ubuntu desktop](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview)  

## Prerequisites  
Install these apps on your device prior to enrollment:  

* [Microsoft Edge web browser, version 102.*X* or later](https://www.microsoft.com/edge): The Edge browser is used to access your organization's websites and other online resources.  
* [Microsoft Intune app](microsoft-intune-app-linux.md): The Linux version of the Microsoft Intune app is used for enrollment. The Intune app registers your device with your org and enrolls it in Intune.   

## Enroll device  
Follow these steps to register a Linux device on your organization's network.  

1. Open the Microsoft Intune app.  
2. Sign in with your work or school account.    
3. Review the pre-enrollment screens. Then select **Next** to begin enrollment. 
4. Wait a few minutes while the Intune app enrolls your device. 
   1. If instructed to, update the settings on your device to meet your organization's security requirements.   
   2. An on-screen confirmation appears when your device is enrolled and ready-to-use for work. You can begin using your device for work right away. 
   3. Sign in to Microsoft Edge with your work or school account to access your org's internal websites.   

> [!NOTE]
> Ubuntu on WSL2 is not a supported scenario.  

## Next steps
As long as your device meets your organization's requirements, it will continue to have work access. Your organization may limit access if the Intune app flags your device as noncompliant. You can view and resolve all compliance issues in the Microsoft Intune app. For more information, see [Check status on Linux devices](check-status-linux.md).  
