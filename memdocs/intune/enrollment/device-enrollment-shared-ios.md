---
# required metadata

title: Shared iOS and iPadOS devices
titleSuffix: Microsoft Intune
description: Learn about Shared iOS and iPadOS devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/08/2021
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# What are shared iOS and iPadOS devices?

Shared devices are organization-owned multi-user devices. These devices can be special-purpose or multi-purpose as needed in each environment. Shared devices enable front-line workers in healthcare, hospitality, retail, manufacturing, and other industries to access critical applications and tools essential to their role in the organization. In education, shared devices are used as learning aids or test-taking devices in classrooms.

## Shared device solutions on iOS and iPadOS 

Microsoft Endpoint Manager supports two types of shared device solutions for iOS and iPadOS: 
- [Shared iPads](../enrollment/device-enrollment-shared-ipad.md)
- [Shared Device Mode](/azure/active-directory/develop/msal-ios-shared-devices)

## Important considerations when choosing a shared device solution for iOS and iPadOS 

The following table captures the key differences between the two available shared devices solutions on iOS/iPadOS. Review this to select the most appropriate iOS/iPadOS shared device strategy for your organization.

| Consideration | Shared iPad | Shared Device Mode |
|-|-|-|
| Supported   device types | iPad | iPhone, iPod touch, iPad |
| Minimum   device requirements | iPadOS 13.4 or later with at   least 32 GB of storage. | iOS 13 or later, iPadOS 13 or   later |
| AAD   federation with Apple Business or School Manager | Required. This enables users to   sign in using their AAD username and password. | Not required |
| Managed Apple ID | AAD federation automatically creates Managed Apple ID when user signs in on Shared iPad for the first time.<p>If AAD   federation is not set up, Managed Apple IDs can be created manually in Apple   Business or School Manager and shared with users for signing in. | Not required   |
| Device   provisioning | Shared iPad can be enabled on   iPads enrolled using Automated Device Enrollment without user affinity. | Shared   Device Mode can be configured on devices enrolling using Automated Device   Enrollment without user affinity. For more information, see [Use Intune to enable shared device mode & SSO extension](/azure/active-directory/develop/msal-ios-shared-devices#use-intune-to-enable-shared-device-mode--sso-extension). |
| Temporary   session without signing in | Temporary   sessions that do not require a Managed Apple ID or password are allowed by   default.  Temporary sessions can be allowed or blocked by Intune policy. For more information, see [Shared iPad](../configuration/device-restrictions-ios.md#shared-ipad). | Not applicable |
| Supported   app types | Device-licensed purchased or   custom apps (VPP), line-of-business apps, web apps. | Apps   that have been modified to support Shared Device Mode including MSAL   integration. For more information, see [Modify your iOS application to support shared device mode](/azure/active-directory/develop/msal-ios-shared-devices#modify-your-ios-application-to-support-shared-device-mode). |
| Policy   and app assignment | Device-assigned required apps   and policies are supported. The same apps and policies apply to any user   signing in on a Shared iPad. | Device-assigned required apps   and policies are supported. |
| Unsupported scenarios | Conditional Access<br>App Protection Policies<br>Intune Company Portal app<br>Available apps<br>User-assigned policies and apps  | Conditional Access<br>App Protection Policies<br>Intune Company Portal app<br>Available apps<br>Apps that don’t support Shared Device Mode<br>User-assigned policies and apps |

## Recommended iOS/iPadOS shared device strategy

Shared iPad is the recommended shared device solution for Microsoft 365 on iPadOS. If you are planning your organization’s shared device strategy, it is highly recommended that you choose iPadOS devices that meet the minimum requirements for Shared iPad (see section above). 
If your organization’s shared device strategy requires cellphone capabilities or includes iOS devices, Shared Device Mode is the recommended shared device solution on iOS. 
Review the differences between Shared iPad and Shared Device Mode to ensure that the recommendations above will fit your organization’s needs.

## Next steps

- [Set up iOS/iPadOS device enrollment with Apple Configurator](../enrollment/apple-configurator-enroll-ios.md)