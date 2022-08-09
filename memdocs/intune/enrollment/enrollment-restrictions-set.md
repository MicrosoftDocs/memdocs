---
# required metadata

title: Overview of enrollment restrictions  
titleSuffix: Microsoft Intune 
description: Learn about
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/08/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# What are enrollment restrictions?      

**Applies to**
* Android  
* iOS
* macOS 
* Windows 10
* Windows 11 


[!INCLUDE [azure_portal](../includes/azure_portal.md)]  

Device enrollment restrictions let you restrict enrollment based on device attributes. When restrictions are applied, users on restricted devices or who exceed the device limit are blocked from enrolling in Microsoft Intune. There are two types of device enrollment restrictions you can configure in Microsoft Intune:   

* *Device platform enrollment restrictions* define which platforms, versions, and management types can enroll. In Intune, you can restrict device platforms, OS versions, manufacturer, and personally owned devices.  
* *Device limit enrollment restrictions* define how many devices each user can enroll. 

Each restriction type comes with one default policy that you can edit and customize as needed. Intune applies the default to all user and userless enrollments until you assign a higher-priority policy.  

This article provides an overview of the available enrollment restrictions. When you're ready to create an enrollment restriction policy, see [Next steps](enrollment-restrictions-set.md)(in this article).   

## Available restrictions  
You can configure the following restrictions in the admin center: 

* Device platform  
* OS version  
* Device manufacturer
* Device ownership  
* Device limit   

### Platform 
This restriction blocks devices running on specific device platforms. You can apply this restriction to devices running: 

   * Android device administrator
   * Android Enterprise work profile
   * iOS/iPadOS
   * macOS
   * Windows 

In groups where both Android platforms are allowed, devices that support work profile will enroll with a work profile. Devices that don't support work profile will enroll on the Android device administrator platform. Neither work profile nor device administrator enrollment will work until you complete all prerequisites for Android enrollment.   

This configuration is in the admin center under **Enrollment device platform restrictions**.  

### OS version 
This restriction enforces your maximum and minimum OS version requirements. Devices running earlier or later OS versions aren't allowed to enroll. This type of restriction works with the following operating systems: 

   * Android device administrator\*
   * Android Enterprise work profile\*  
   * iOS/iPadOS\*
   * Windows  

\* Version restrictions are supported on these platforms for devices enrolled via Intune Company Portal only.    

This configuration is in the admin center under **Enrollment device platform restrictions**.  

## Combining restrictions      
Since Intune supports two Android platforms, it's important to understand how version restrictions work when used together with device platform restrictions:   
  * If you allow both platforms for the same group, and then refine it for specific and non-overlapping versions, devices are sent through the Android enrollment flow that's picked for their version.   
  * If you allow both platforms, but block the same versions, devices running blocked versions can't enroll. Users on these devices are sent through the Android device administrator enrollment flow before they're blocked and prompted to sign out. 

### Device manufacturer  
This restriction blocks devices made by specific manufacturers, and is applicable to Android devices only.  

This configuration is in the admin center under **Enrollment device platform restrictions**.    

### Personally-owned devices  
This restriction helps prevent device users from accidentally enrolling their personal devices, and applies to devices running:  

* Android
* iOS/iPad OS
* macOS
* Windows  

This configuration is in the admin center under **Enrollment device platform restrictions**. 

#### Blocking personal Android devices  
By default, until you manually make changes in the admin center, your Android Enterprise work profile device settings and Android device administrator device settings are the same. 

If you block Android Enterprise work profile enrollment on personal devices, only corporate-owned devices can enroll with [personally-owned work profiles](../apps/android-deployment-scenarios-app-protection-work-profiles.md#android-enterprise-personally-owned-work-profiles).  


#### Blocking personal iOS/iPadOS devices  
By default, Intune classifies iOS/iPadOS devices as personally-owned. To be classified as corporate-owned, an iOS/iPadOS device must fulfill one of the following conditions:
- [Registered with a serial number or IMEI](corporate-identifiers-add.md).
- Enrolled by using Automated Device Enrollment (formerly Device Enrollment Program).

> [!NOTE]
> An iOS User Enrollment profile overrides an enrollment restriction policy. For more information, see [Set up iOS/iPadOS and iPadOS User Enrollment (preview)](ios-user-enrollment.md).  

#### Blocking personal Macs  
By default, Intune classifies macOS devices as personally-owned. To be classified as corporate-owned, a Mac must fulfill one of the following conditions:
- [Registered with a serial number](corporate-identifiers-add.md).
- Enrolled by using Automated Device Enrollment (formerly Device Enrollment Program).

#### Blocking personal Windows devices  
If you block personally owned Windows devices from enrollment, Intune checks to make sure that each new Windows enrollment request has been authorized for corporate enrollment. Unauthorized enrollments are blocked.  

The following enrollment methods are authorized for corporate enrollment:  
- The enrolling user is using a [device enrollment manager account]( device-enrollment-manager-enroll.md).
- The device enrolls through [Windows Autopilot](../../autopilot/enrollment-autopilot.md).
- The device is registered with Windows Autopilot but isn't an MDM enrollment only option from Windows Settings.
- The device enrolls through a [bulk provisioning package](windows-bulk-enroll.md).
- The device enrolls through GPO, or [automatic enrollment from Configuration Manager for co-management](/configmgr/comanage/quickstart-paths#bkmk_path1).

> [!NOTE]
> Since a co-managed device enrolls in the Microsoft Intune service based on its Azure AD device token, and not a user token, only the default Intune enrollment restriction will apply to it. 
 
Intune marks devices going through the following types of enrollments as corporate-owned, and blocks them from enrolling because these methods don't offer the Intune administrator per-device control:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Azure Active Directory join during Windows setup](/azure/active-directory/device-management-azuread-joined-devices-frx)\*.
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Azure Active Directory join from Windows Settings](/azure/active-directory/user-help/user-help-register-device-on-network)\*.
 
Intune also blocks personal devices using these enrollment methods:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Add Work Account from Windows Settings](/azure/active-directory/user-help/user-help-join-device-on-network)\*.
- [MDM enrollment only]( /windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) option from Windows Settings.

\* These won't be blocked if registered with Autopilot.  

### Device limit 
This restriction lets you put a limit on the number of devices a person can enroll. In Intune, you can set the device limit from 1 to 15.  

This configuration is in the admin center under **Enrollment device limit restrictions**. 

## Limitations  

* Enrollment restrictions are applied to users. For enrollment scenarios that aren't user-driven, such as Windows Autopilot self-deploying mode, bulk enrollment (WCD), or Azure Virtual desktop, Intune enforces the default policy.  

* Device limit restrictions can't be applied to devices in the following Windows enrollment scenarios, because these scenarios utilize shared device mode:  

  * Co-managed enrollments  
  * Group Policy (GPO) enrollments  
  * Azure Active Directory (Azure AD) joined enrollments, including bulk enrollments  
  * Windows Autopilot enrollments  
  * Device enrollment manager enrollments

  Instead, you can configure a hard limit for these enrollment types in Azure AD. For more information, see [Manage device identities by using the Azure portal](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).  

## Next steps  

Use the table-of-contents to step through each article in the enrollment restrictions how-to guide, or jump to an article using the following links:  
  * [Create device platform enrollment restrictions](create-device-limit-restrictions.md)  
  * [Create device limit enrollment restrictions](create-device-platform-restrictions.md)  
  * [View enrollment reports](view-enrollment-reports.md)  





























