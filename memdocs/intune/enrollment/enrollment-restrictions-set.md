---
# required metadata

title: Overview of enrollment restrictions  
titleSuffix: Microsoft Intune 
description: Learn about the enrollment restrictions available in Microsoft Intune. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/02/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
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
- tier1
- M365-identity-device-management
- highpri
- highseo
- ContentEnagagementFY23
---

# What are enrollment restrictions?      

**Applies to**
* Android  
* iOS
* macOS
* Windows 10
* Windows 11

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

Device enrollment restrictions let you restrict devices from enrolling in Intune based on certain device attributes. There are two types of device enrollment restrictions you can configure in Microsoft Intune:   

* **Device platform restrictions**: Restrict devices based on device platform, version, manufacturer, or ownership type.     
* **Device limit restrictions**: Restrict the number of devices a user can enroll in Intune.  

Each restriction type comes with one default policy that you can edit and customize as needed. Intune applies the default policy to all user and userless enrollments until you assign a higher-priority policy.  

This article provides an overview of the available enrollment restrictions, and feature limitations. To start creating restrictions, skip to [Next steps](enrollment-restrictions-set.md#next-steps) (in this article).   

## Available restrictions  
You can configure the following restrictions in the admin center: 

* Device limit 
* Device platform  
* OS version  
* Device manufacturer
* Device ownership (personally owned devices)    

### Device limit 
Put a limit on the number of devices a person can enroll. You can set the device limit from 1 to 15.  

This configuration is in the admin center under **Enrollment device limit restrictions**. 

### Device platform  
 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]  
Block devices running on a specific device platform. You can apply this restriction to devices running: 

   * Android device administrator
   * Android Enterprise work profile
   * iOS/iPadOS
   * macOS
   * Windows 10/11  

In groups where both Android platforms are allowed, devices that support work profile will enroll with a work profile. Devices that don't support work profile will enroll on the Android device administrator platform. Neither work profile nor device administrator enrollment will work until you complete all prerequisites for Android enrollment.   

This restriction is in the admin center under **Enrollment device platform restrictions**.  

### OS version 
This restriction enforces your maximum and minimum OS version requirements. This type of restriction works with the following operating systems: 

   * Android device administrator\*
   * Android Enterprise work profile\*  
   * iOS/iPadOS\*
   * Windows  

\* Version restrictions are supported on these operating systems for devices enrolled via Intune Company Portal only.    

This restriction is in the admin center under **Enrollment device platform restrictions**.  

### Device manufacturer  
This restriction blocks devices made by specific manufacturers, and is applicable to Android devices only. It is in the admin center under **Enrollment device platform restrictions**.    

### Personally owned devices  
This restriction helps prevent device users from accidentally enrolling their personal devices, and applies to devices running:  

* Android
* iOS/iPad OS
* macOS
* Windows 10/11 

This restriction is in the admin center under **Enrollment device platform restrictions**.  

#### Blocking personal Android devices  
By default, until you manually make changes in the admin center, your Android Enterprise work profile device settings and Android device administrator device settings are the same. 

If you block Android Enterprise work profile enrollment on personal devices, only corporate-owned devices can enroll with [personally owned work profiles](../apps/android-deployment-scenarios-app-protection-work-profiles.md#android-enterprise-personally-owned-work-profiles).  


#### Blocking personal iOS/iPadOS devices  
By default, Intune classifies iOS/iPadOS devices as personally owned. To be classified as corporate-owned, an iOS/iPadOS device must fulfill one of the following conditions:
- [Registered with a serial number or IMEI](corporate-identifiers-add.md).
- Enrolled by using Automated Device Enrollment (formerly Device Enrollment Program).

> [!NOTE]
> An iOS User Enrollment profile overrides an enrollment restriction policy. For more information, see [Set up iOS/iPadOS and iPadOS User Enrollment (preview)](ios-user-enrollment.md).  

#### Blocking personal Macs  
By default, Intune classifies macOS devices as personally owned. To be classified as corporate-owned, a Mac must fulfill one of the following conditions:
- [Registered with a serial number](corporate-identifiers-add.md).
- Enrolled via Apple Automated Device Enrollment (ADE).  

#### Blocking personal Windows devices  
If you block personally owned Windows devices from enrollment, Intune checks to make sure that each new Windows enrollment request has been authorized for corporate enrollment. Unauthorized enrollments are blocked.  

The following enrollment methods are authorized for corporate enrollment:  
- The device enrolls through [Windows Autopilot](/autopilot/enrollment-autopilot).
- The device enrolls through GPO, or [automatic enrollment from Configuration Manager for co-management](/configmgr/comanage/quickstart-paths#bkmk_path1).
- The device enrolls through a [bulk provisioning package](windows-bulk-enroll.md).
- The enrolling user is using a [device enrollment manager account](device-enrollment-manager-enroll.md).

> [!NOTE]
> Since a co-managed device enrolls in the Microsoft Intune service based on its Microsoft Entra device token, and not a user token, only the default Intune enrollment restriction will apply to it.

Intune marks devices going through the following types of enrollments as corporate-owned, and blocks them from enrolling (unless registered with Autopilot) because these methods don't offer the Intune administrator per-device control:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Microsoft Entra join during Windows setup](/azure/active-directory/device-management-azuread-joined-devices-frx).  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Microsoft Entra join from Windows Settings](/azure/active-directory/user-help/user-help-join-device-on-network).  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with Microsoft Entra join or hybrid Entra join via [Windows Autopilot for existing devices](/autopilot/existing-devices).  

Intune also blocks personal devices using these enrollment methods:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Add Work Account from Windows Settings](/azure/active-directory/user-help/user-help-register-device-on-network).
- [MDM enrollment only](/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) option from Windows Settings.
- [Enrollment using the Intune Company Portal app](../user-help/enroll-windows-10-device.md).  
- Enrollment via a Microsoft 365 app, which occurs when users select the **Allow my organization to manage my device** option during app sign-in. 

> [!IMPORTANT] 
> Devices joined by Workplace Join could be blocked from enrolling if they were ever previously Microsoft Entra joined to the tenant. To avoid being blocked, deregister and remove the device's associated object in Microsoft Entra ID before attempting to join the device by Workplace Join.  

## Limitations  

* Enrollment restrictions are applied to enrollments that are user-driven. Intune enforces the default policy in enrollment scenarios that aren't user-driven, such as:  
  
  *  Windows Autopilot self-deploying mode and Autopilot for pre-provisioned deployment  
  *  Bulk enrollment via Windows Configuration Designer  
  *  Userless Apple automated device enrollment (without user-device affinity)  
  *  Azure Virtual Desktop   
  *  Windows 365   

* Device limit restrictions can't be applied to devices in the following Windows enrollment scenarios, because these scenarios utilize shared device mode:  

  * Co-managed enrollments  
  * Group Policy (GPO) enrollments  
  * Microsoft Entra joined enrollments, including bulk enrollments  
  * Windows Autopilot enrollments  
  * Device enrollment manager enrollments

  Instead, you can configure a hard limit for these enrollment types in Microsoft Entra ID. For more information, see [Manage device identities by using the Azure portal](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings).  

## Next steps  
Select the type of enrollment restriction you want to apply and create the profile:   
 * [Create device platform enrollment restrictions](create-device-platform-restrictions.md)    
 * [Create device limit enrollment restrictions](create-device-limit-restrictions.md)  
