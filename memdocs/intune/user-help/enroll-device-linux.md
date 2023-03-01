---
# required metadata

title: Enroll a Linux device in Intune| Microsoft Docs
description: Enroll your personal Linux device in Microsoft Intune to get secure access to work or school resources in Microsoft Edge. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/12/2022
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

ms.reviewer: ilwu
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---


# Enroll Linux device in Intune

Enroll your personal Linux device in Microsoft Intune to get secure access to work or school resources in Microsoft Edge. This article describes how to enroll and register your personal Linux device on your organization's network.    

## System requirements  
Enrollment is supported on devices with:  

* Ubuntu Desktop 22.04 or 20.04 LTS (pyhsical or Hyper-V machine with x86/64 CPUs)
* A GNOME graphical desktop environment (automatically included with Ubuntu Desktop 22.04 and 20.04 LTS)  

We recommend enabling encryption when you first install Ubuntu Desktop on your device. Your organization may require your device to be encrypted, and it's easiest to encrypt the device during OS installation. 

For help with setting up Ubuntu Desktop, see the following resources on the Ubuntu website:   

   * [Ubuntu desktop downloads](https://ubuntu.com/download/desktop) 
   * [How to install Ubuntu desktop](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview)  

## Prerequisites  
Install these apps on your device prior to enrollment:  

* [Microsoft Edge web browser, version 102.*X* or later](https://www.microsoft.com/edge): The Edge browser is used to access your organization's websites and other online resources.  
* [Microsoft Intune app](microsoft-intune-app-linux.md): The Linux version of the Microsoft Intune app is used for enrollment. The Intune app registers your device with your org and enrolls it in Intune.   

## Enroll device  
Follow these steps to register your personal Linux device on your organization's network.  

1. Open the Microsoft Intune app.  
2. Sign in with your work or school account.    
3. Review the pre-enrollment screens. Then select **Next** to begin enrollment. 
4. Wait a few minutes while the Intune app enrolls your device. 
   1. If instructed to, update the settings on your device to meet your organization's security requirements.   
   2.  An on-screen confirmation appears when your device is enrolled and ready-to-use for work. You can begin using your device for work right away. 
   3. Sign in to Microsoft Edge with your work or school account to access your org's internal websites.   

> [!NOTE]
> Ubuntu on WSL2 is not a supported scenario.  

## Next steps
As long as your device meets your organization's requirements, it will continue to have work access. Your organization may limit access if the Intune app flags your device as noncompliant. You can view and resolve all compliance issues in the Microsoft Intune app. For more information, see [Check status on Linux devices](check-status-linux.md).  
