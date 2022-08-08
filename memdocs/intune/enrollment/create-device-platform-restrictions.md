---
# required metadata

title: Create device platform restrictions  
titleSuffix: Microsoft Intune  
description: Restrict personally owned devices, and specific device platforms and OS versions from enrolling in Intune. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/08/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: 
ms.technology:
ms.assetid: 

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

# Create device platform restrictions   

**Applies to**
* Android  
* iOS
* macOS 
* Windows 10
* Windows 11 


[!INCLUDE [azure_portal](../includes/azure_portal.md)]  

Use the device platform enrollment restrictions in Microsoft Intune to block personally owned devices from enrolling, and to block devices by device platform and OS version.  

You can create a new Intune device platform restriction policy in the Microsoft Endpoint Manager admin center or use the default policy that's already available. You have one default policy for platform restrictions, and you can edit and customize it as needed. 

You can have up to 25 device platform restriction policies. Intune applies the default policy to all user and userless enrollments until you assign a higher-priority policy.  

This article describes the device platform restrictions supported in Microsoft Intune and how to configure them from the Microsoft Endpoint Manager admin center.  

## Default policy 
Microsoft Intune provides one default policy for device platform restrictions. You can edit and customize it as needed. Intune applies the default policy to all user and userless enrollments until you assign a higher-priority policy.  

## Available restrictions  
This section describes the restrictions you can configure in a device platform-enrollment restriction policy. 

### Device platform 
This restriction blocks devices running on specific platforms from enrolling. You can restrict devices running the following platforms: 

   * Android device administrator
   * Android Enterprise work profile
   * iOS/iPadOS
   * macOS
   * Windows 

In groups where both Android platforms are allowed, devices that support work profile will enroll with a work profile. Devices that don't support work profile will enroll on the Android device administrator platform. Neither work profile nor device administrator enrollment will work until you complete all prerequisites for Android enrollment.   

Since Intune supports two Android platforms, it's important to understand how platform restrictions work when used with version restrictions:   
  * If you allow both platforms for the same group, and then refine it for specific and non-overlapping versions, devices are sent through the Android enrollment flow that's picked for their version.   
  * If you allow both platforms, but block the same versions, devices running blocked versions cannot enroll. Users on these devices are sent through the Android device administrator enrollment flow before they are blocked and prompted to sign out. 

### OS version 
This restriction enforces your maximum and minimum OS version requirements. Devices running earlier or later OS versions are not allowed to enroll. This type of restriction works with the following operating systems: 

   * Android device administrator\*
   * Android Enterprise work profile\*  
   * iOS/iPadOS\*
   * Windows  

\* Version restrictions are supported on these platforms for devices enrolled via Intune Company Portal only.    

### Personally-owned devices  
This restriction helps prevent device users from accidentally enrolling their personal devices, and applies to devices running:  

* Android
* iOS/iPad OS
* macOS
* Windows  

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
 
Intune marks devices going through the following types of enrollments as corporate-owned. But Intune blocks devices enrolling  since they don't offer the Intune administrator per-device control, they are blocked:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Azure Active Directory join during Windows setup](/azure/active-directory/device-management-azuread-joined-devices-frx)\*.
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Azure Active Directory join from Windows Settings](/azure/active-directory/user-help/user-help-register-device-on-network)\*.
 
Intune also blocks personal devices using these enrollment methods:  
- [Automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with [Add Work Account from Windows Settings](/azure/active-directory/user-help/user-help-join-device-on-network)\*.
- [MDM enrollment only]( /windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) option from Windows Settings.

\* These won't be blocked if registered with Autopilot.  

## Create a device platform restriction   

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Go to **Devices** > **Enroll devices** > **Enrollment device platform restrictions**.  
3. Select the tab along the top of the page that corresponds with the platform you're configuring. Your options:  

    * **Android restrictions**
    * **Windows restrictions**
    * **MacOS restrictions**
    * **iOS restrictions**  

4. Select **Create restriction**.  
5. On the **Basics** page, give the restriction a name and optional description. 
6. Select **Next**.  
7. On the **Platform settings** page, configure the restrictions for your selected platform. Your options:       
    - **Platform** (Android): Select **Allow** to permit a platform to enroll, and **Block** to restrict it.       
    - **MDM** (Windows, macOS, and iOS/iPadOS): Select **Allow** to permit a platform to enroll, and **Block** to restrict it.   
    - **Personally-owned**: Select **Allow** to permit devices to enroll and operate as personal devices.  
    - **Device manufacturer** (Android): Enter a comma-separated list of the manufacturers that you want to block. 
    - **Allow min/max range** (Android, Windows, iOS/iPadOS): Enter the minimum and maximum OS versions allowed to enroll. Supported version formats include:  
        - Windows supports major.minor.build.rev for Windows 10 and Windows 11 only.  
        - Android device administrator and Android Enterprise work profile support major.minor.rev.build.  
        - iOS/iPadOS supports major.minor.rev.  

             > [!TIP]
             > The min/max range isn't applicable to Apple devices that enroll with the Device Enrollment Program, Apple School Manager, or the Apple Configurator app. Although Intune doesn't block ADE enrollments that use Company Portal to authenticate, not meeting OS requirements impacts registration because devices can't create the Azure AD device record used to evaluate Conditional Access policies. You can tell that this is the case if a device user receives an error message that says "Couldn't map device record with a user" after they sign in to Company Portal.        

8. Select **Next**. 
9. Optionally, add scope tags to the restriction. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md). 

      > [!NOTE]
      >  If you apply scope tags to a restriction, only Intune users within scope can view and manage the policy. Only people in scope can view and reorder a restriction, or change its priority level. They can also see the relative priority of the restriction, even if they can't see all restrictions.  

10. Select **Next**. 
11. On the **Assignments** page, select **Add groups** and then use the search box to find and select groups. To assign the restriction to all device users, select **Add all users**. If you don't assign a restriction to at least one group, the restriction won't take effect.  
12. Optionally, after you assign groups, select **Edit filter** to restrict the policy assignment further with filters. Filters are available for macOS, iOS, and Windows policies. For more information, see [Apply assignment filters](enrollment-restrictions-set.md#apply-assignment-filters) (in this article).  
13. Select **Next**. 
14. Review your policy, and then select **Create** to create it. 

You can view the new restriction policy and access its properties in the **Enrollment device platform restrictions** > **Device type restrictions** table. Select and drag the restriction to reposition it in the table and change its priority.   

## Apply assignment filters 

You can use assignment filters to include and exclude additional devices from certain group-targeted policies. Enrollment restrictions and ESP policies both support the use of assignment filters.   

For example, you can use a filter to allow personal Windows devices to enroll while blocking devices that run a specific operating system SKU. To achieve this outcome, apply a preconfigured filter to your enrollment restriction assignments. The filter needs to have the `operatingSystemSKU` property in its rules. Example steps:  

  1. Create a platform enrollment restriction policy for Windows.  
  2. In the platform settings, select the option that allows personally-owned devices to enroll. 
  3. In the assignments settings, select the groups you want to assign.
  4. Select **Edit filter** and then apply your preconfigured filter that contains the `operatingSystemSKU` property. The applied property blocks devices running Windows 10 Home edition. 

For more information about creating filters, see [Create a filter](../fundamentals/filters.md). 

### Supported filter properties  

Enrollment restrictions support fewer filter properties than other group-targeted policies. This is because devices are not yet enrolled, so Intune doesn't have the device info to support all properties. You'll see the limited selection of properties when you:  

* Configure a device platform restriction policy for Apple and Windows devices. 
* Configure an enrollment status page (ESP) policy for Windows. 
* Edit a filter that's in-use in an enrollment restriction or ESP profile. 

The following filter properties are always available to use with enrollment policies:    

**Windows** 

* OS version 
* Operating System SKU 
* Enrollment profile name

**iOS/iPadOS and macOS**  
* Manufacturer 
* Model 
* OS version 
* Ownership 
* Enrollment profile name 

For more information about these properties, see [device properties](../fundamentals/filters-device-properties.md#device-properties). Filters cannot be used with Android enrollment restrictions.  

## Edit enrollment restrictions  

Edits are applied to new enrollments and do not affect devices that are already enrolled.  

1. Go to **Enrollment device platform restrictions**.  
2. In the **Device type restrictions** table, select the name of the policy you want to change.
3. Select **Properties**.  
4. Select **Edit**   
5. Make your changes and select **Review + save**. 
6. Review your chages and select **Save**.  































