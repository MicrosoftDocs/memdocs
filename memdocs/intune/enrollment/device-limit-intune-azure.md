---
# required metadata

title: Understand Intune and Azure AD device limit restrictions
titleSuffix: Microsoft Intune
description: Learn the differences between Intune device limit restrictions and Azure AD device limit restrictions. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/19/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- highpri
---

# Understand Intune and Azure AD device limit restrictions  

**Applies to**
- Android
- iOS
- macOS
- Windows 10
- Windows 11

Device limit restrictions can be configured two ways: by Intune enrollment, or by Azure Active Directory (AD) joined or Azure AD registered. This article clarifies when these limits are applied based on your configuration.  

## Intune device limit restrictions

Intune device limit restrictions set the maximum number of devices that a user can enroll. You can allow a user to enroll up to 15 devices. To set a device limit restriction, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Then go to **Devices** > **Enrollment restrictions**. For more information, see [Create a device limit restriction](create-device-limit-restrictions.md).  

## Azure device limit restriction

Azure device limit restrictions set the maximum number of devices that either Azure AD joins or Azure AD registers. To set the **Maximum number of devices per user**, go to the Azure portal > **Azure Active Directory** > **Devices**. For more information, see [Configure device settings](/azure/active-directory/devices/device-management-azure-portal)

## Settings applied based on user affinity  

If you enforce both Intune and Azure device limit restrictions, the following table shows you how each limitation is applied.   

Platform| Device management solution | User affinity | Does Azure AD limitation apply? | Does Intune limitation apply? |  
| -----| ----- | ----- | ----- | ----- |
|Android| Android Enterprise personally-owned work profile | Yes | Yes | Yes|  
|Android| Android Enterprise dedicated device | No | No | No |  
|Android| Android Enterprise fully managed | Yes | Yes | Yes |  
|Android| Android Enterprise corporate-owned work profile | Yes | Yes | Yes |  
|Android| Android device administrator | Yes | Yes | Yes |  
|Android| Android device administrator + device enrollment manager | No | Yes | No | 
|iOS and macOS| BYOD: Apple User Enrollment | Yes | Yes | Yes |  
|iOS and macOS| BYOD: Apple Device Enrollment | Yes | Yes | Yes |  
|iOS and macOS| Apple Automated Device Enrollment | Yes | Yes | Yes |  
|Windows 10/11| BYOD: User enrollment | Yes | Yes | Yes |   
|Windows 10/11| Automatic enrollment + group policy | No | No | Yes |  
|Windows 10/11| Automatic enrollment + device enrollment manager | No | Yes | No | 
|Windows 10/11| Automatic enrollment + bulk device enrollment | No | Yes | No |
|Windows 10/11| Windows Autopilot | Yes | Yes | No |  
|Windows 10/11| Co-management with Configuration Manager | No | Yes | No |  

## Android and iOS devices

### iOS or Android devices example 1

- The Azure **Maximum number of devices per user** setting is set to 3.
- The Intune **Device limit** setting is set to 5.
 
**Outcome:** The maximum number is per user. For example, if you enroll three Intune devices, the Azure registration for the fourth device will fail because of the settings to limit the number of registrations for the devices.

### iOS or Android devices example 2

- The Azure **Maximum number of devices per user** setting is set to 20.
- The Intune **Device limit** setting is set to 2.

**Outcome:** You can successfully register and enroll two devices. Intune enrollment will be blocked for any additional devices. ADE without user affinity is restricted by Azure device registration limits although it's not associated with a user.

## Windows devices  

Intune device limit restrictions don't apply for the following Windows enrollment types:
- Co-managed enrollments
- Group policy object (GPO) enrollments
- Azure AD joined enrollments
- Bulk Azure AD joined enrollments
- Autopilot enrollments
- Device enrollment manager enrollments

Devices enrolled via these methods are enrolled automatically or by an Intune admin, not by an employee or student, and are considered shared devices.  

Instead, you can set a [hard limit in Azure Active Directory](device-limit-intune-azure.md#azure-device-limit-restriction) to limit the number of devices that an employee can join or register with Azure AD. The **Maximum number of devices per user** setting in Azure AD applies to devices that are Azure AD joined or Azure AD registered. It doesn't apply to hybrid Azure AD joined devices.  

### Windows 10/11 example 1

- The Azure **Maximum number of devices per user** setting is set to 5.
- The Intune **Device limit** setting is set to 3.
- The devices are hybrid Azure AD joined and enrolled automatically (GPO configured).

**Outcome:** Because the enrollment is pushed through GPO, the Azure device registration limit doesn't apply.  The Intune device limit restriction also doesn't apply.

### Windows 10/11 example 2  

- The Azure **Maximum number of devices per user** setting is set to 5.
- The Intune **Device limit** setting is set to 2.
- The devices are local domain joined and enrolled by using **Settings** > **Access Work or School** > **Connect**.

**Outcome:** You can only enroll two devices before they're blocked. You can register up to five devices.


## Next steps

- [Create a device limit restriction in Azure.](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Learn more about registration and domain joined.](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)
