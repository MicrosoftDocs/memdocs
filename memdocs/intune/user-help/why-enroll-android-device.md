---
# required metadata

title: Android device enrollment overview  
description: Learn about enrollment for Android devices, including the benefits and why workplaces and schools require it.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/16/2020
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: d22f5aea-7be4-419b-b51b-a522ca037b69
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

# Android device enrollment overview  

Schools and employers want to make sure that you're using a secure, trusted device to access internal resources such as apps and Wi-Fi. When you enroll in Intune, the Microsoft Intune and Company Portal apps ensure that you have secure access to these resources no matter where you are or what device you're using. 

If your organization requires you to install and enroll with one of these apps, you'll need to do that before you can access internal apps on your device. This article describes the purpose and benefits of enrolling your devices with these apps. 

To skip this overview and go straight to the enrollment steps, select from one of the following articles (ask your IT support person if you're not sure which set of instructions you're supposed to follow):  
 
* [Intune Company Portal enrollment](enroll-device-android-company-portal.md)
* [Android work profile enrollment](enroll-device-android-work-profile.md)
* [Microsoft Intune app enrollment](enroll-device-android-microsoft-intune-app.md)
* Derived credentials enrollment (smart card users):  
    * [Entrust](enroll-android-device-entrust-datacard.md)  
    * [Intercede](enroll-android-device-intercede.md)  
    * [DISA Purebred](enroll-android-device-disa-purebred.md)  

## Secure your device 
 The Company Portal and Microsoft Intune app enroll your device in Intune.  Intune is a mobile device management provider that helps your org manage mobile devices and apps through security and device policies. 

The apps walk you through each step of enrollment, and configure your device settings to match your organization's policies. They also alert you to problems or settings that need to be resolved before you can get corporate access.  

Examples of policies that your organization might require are:  
* Setting up a password or PIN
* Restricting access after a set number of sign-in attempts
* Ensuring that you're not using a jailbroken or rooted device
* Installing work-required apps  

## Access internal apps, VPN, and Wi-Fi 
During enrollment, Microsoft Intune and Company Portal apps require you to connect to your work or school account.  After you authenticate and after you've configured your device settings to match your organization's policies, you'll gain access to your organization's email account, network, files, and apps.  

Organizations sometimes require you to install work or security apps, such as Microsoft Office or Mobile Threat Defense. If these apps are required or become available for you, you'll find them in Company Portal or the Microsoft Intune app.

## Remotely reset a lost or stolen device (if device supports it)
If a device is lost or stolen, you can sign in to the Company Portal app or Company Portal website on any other device, and reset your phone to factory settings. This feature is helpful if your missing device contains proprietary work data that you don't want anyone else to access. Because the device is enrolled in management, your company support or IT admin can also help reset it.  

The reset feature isn't available in the Microsoft Intune app.  

## Get latest policy updates and requirements
The Company Portal or Microsoft Intune app will automatically check in, or sync, with Intune every eight hours. If you're using Company Portal and want to check in more frequently, you or your company support can initiate a manual sync. During check-in, the apps will:  

* Download any policy or app updates that your company support makes available.  
* Send hardware inventory updates. These updates don't contain personal information.  
* Send company app inventory updates. These updates don't contain personal information.  

When your device is out-of-sync or no longer meets the requirements, its status appears as *Not compliant*. Your access to work and school-related resources might be revoked until your device meets the requirements again. The Company Portal app notifies you of these problems and the steps you need to take to fix them.  


## Get Remote Help from IT support person    
When you enroll your device, your company support or IT admin is given access to the device for limited and meaningful reasons.   

They can:  

* Reset your device back to the manufacturer's defaults. As mentioned above, you also have access to reset your device. However, if you can't access the Company Portal app right away, your company can reset the device for you.  

* Remove all company-related data. Your organization might remove company-related data from your device if you leave the company, or if your device becomes unmanaged. Your personal data and settings aren't removed, and will remain on the device.  

* Set requirements for your device, such as requiring you to have a device password or PIN. In this case, you'll get app notifications that your device isn't compliant. Your company support might also limit the number of times you can enter an incorrect password on your device. Excessive, failed password attempts might result in your device being locked.  

* Require you to accept terms and conditions.  

* Disable the camera. The purpose of this policy is to prevent you from photographing proprietary information, and also to remove distractions from school environments. Schools might disable cameras on classroom devices so that students cannot share test materials.  

* Require that all data on the device is encrypted. If lost or stolen, this policy helps protect the data on your device. It also protects data that is shared between devices or apps. 

## Next steps  

When you're ready to enroll your Android device in Intune, follow your organization's instructions to set up your device. Or select one of the articles listed [at the beginning of this article](why-enroll-android-device.md#android-device-enrollment-overview) for links to general setup instructions.    

Contact your support person to find out which setup instructions you should use.  Check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information.  
