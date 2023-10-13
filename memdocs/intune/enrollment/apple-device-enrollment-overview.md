---
# required metadata

title: Overview of Apple Device Enrollment in Microsoft Intune  
titleSuffix: Microsoft Intune
description: Utilize Apple Device Enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/25/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rishitasarin
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure 
ms.collection:
- tier2
- M365-identity-device-management
---

# Overview of Apple Device Enrollment in Microsoft Intune  
Apple *Device Enrollment* enables employees and students to enroll to their new and existing personal devices anytime. It enables essential management functionalities for you in Intune while protecting the personal data of employees and students. When users unenroll their device, all work-related profiles, apps, and data are deleted from the device.    

This article provides an overview of the Apple Device Enrollment features and functionality supported by Microsoft Intune.  

## Enrollment options      
Employees and students can enroll devices via the Intune Company Portal website or app. [Create an enrollment profile] in the admin center to choose and configure the enrollment type.   

> [!TIP]
> We recommend enabling web-based enrollment for devices running iOS/iPadOS 15 and later because it doesn't require employees and students to install the Company Portal app. Post-enrollment functionality remains the same as with app-based enrollment. 

Web-based enrollment utilizes Just in Time (JIT) registration and Apple single sign-on (SSO) extension functionality to handle Azure AD registration within Microsoft Office apps. JIT registration establishes SSO across the device and reduces the number of times users have to authenticate. To enable JIT registration in enrollments, create a device configuration profile with an SSO app extension policy. While web-based enrollment utilizes JIT registration, you are not required to use it with web enrollment.  

The following table provides details about app and web-based enrollment.   

| Specification | App-based enrollment | Web-based enrollment|
| --- | --- | --- | 
| Supported version | iOS/iPadOS 14 and later |iOS/iPadOS 15 and later |
| BYOD and personal devices | ✔️ |✔️ |
| Device associated with single user | ✔️ |✔️|
| Device reset required| ❌|❌|
| Enrollment initiated by device user | ✔️ |✔️|
| Supervision |❌|❌| 
| Just-in-time registration | ❌ |✔️ |
| Required apps | Intune Company Portal app for iOS <br> Microsoft Authenticator | Microsoft Authenticator |  
| Enrollment location | App-based enrollment takes place in the Company Portal app, Safari, and device settings app. |Web-based enrollment takes place in Safari and the device settings app.| 

## Supported settings    
Microsoft Intune supports a subset of device management options for devices enrolled via Apple Device Enrollment. For supported settings in Intune device configurations profiles, see:

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)  
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md) 
   * List others....

If a pre-existing configuration profile is applied to a device, only the settings supported by Apple Device Enrollment take effect. 

## User experience 
Include info about user experience, enrollment, resources.  

Employees and students can access management options for their personal devices in the Intune Company Portal app or on the Company Portal website. Supported actions include:  
- Rename   
- Remove  
- Remote lock  
- Check status  

>[!NOTE]
> The *rename* action that's available to device users changes the display name in Company Portal. It doesn't rename the device in the Microsoft Intune admin center.  

For more information about how employees and students can access these actions, see:

* [Using the Intune Company Portal website](../user-help/using-the-intune-company-portal-website.md) 
* [Check status, or sync device, in Company Portal app](../user-help/sync-your-device-manually-ios.md)
* [Reset device in Company Portal app](../user-help/effects-of-device-reset-company-portal-ios.md)  
* [Remove or unenroll device in Company Portal app](../user-help/unenroll-your-device-from-intune-ios.md)  

## Limitations   


## Next steps  

Choose the user enrollment method you want to use to enroll devices. The following articles describe how to set up these enrollment methods in the Microsoft Intune admin center:    

* [Set up app-based enrollment](app-based-device-enrollment-ios.md)   
* [Set up web-based enrollment](web-based-device-enrollment-ios.md) 

For more details about Apple Device Enrollment features and functionality, see [Device Enrollment and MDM]( https://support.apple.com/guide/deployment/device-enrollment-and-mdm-depd1c27dfe6/web) on the Apple support website.  


