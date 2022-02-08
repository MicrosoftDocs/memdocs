---
# required metadata

title: Intune actions and options supported with Apple User Enrollment
titleSuffix: Microsoft Intune
description: Learn which Intune actions and options are supported with Apple User Enrollment
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 2/14/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# Intune actions and options supported with Apple User Enrollment

User Enrollment supports a subset of device management options. If a pre-existing configuration profile is applied to a User Enrollment device, only settings supported by User Enrollment will be applied to that device.

> [!NOTE]
> Support for Apple's User Enrollment in Intune is currently in preview for iOS and iPadOS.

## Password settings

On User Enrollment devices, if you configure any password setting, then the **Simple passwords** settings is automatically set to **Block**, and a 6 digit PIN is enforced.

For example, you configure the **Password expiration** setting, and push this policy to user-enrolled devices. On the devices, the following happens:
- The **Password expiration** setting is ignored.
- Simple passwords, such as `111111` or `123456`, aren't allowed.
- A 6 digit pin is enforced.

## Administrator remote device actions and options
Admins can perform the following actions and options on User Enrollment devices:
- Retire
- Delete
- Remote Lock
- Sync

All other actions aren't supported.

## End-user actions
On User Enrollment devices, end users can perform these actions on their devices from the Company Portal application and website:
- Rename. This action applies only to the user-facing name within the Company Portal. It won't fully rename the device outside of that context.
- Remove
- Remote Lock
- Check Status

## App deployment options
Following app types can be deployed on User Enrollment devices:
- User-licensed Volume Purchasing Plan (VPP) apps including custom apps
- Line-of-business (LOB) apps
- Web apps

## Other supported options

The following options are supported in Intune for devices enrolled by using Apple User enrollment:
- Per-App VPN. This support excludes Safari Domains as User Enrollment doesn't support configuring Safari settings.
- WiFi 
- Corporate app removal upon unenrollment
- Jailbreak Detection

The following restrictions are supported:
- View corporate documents in unmanaged apps
- Viewing non-corporate documents in corporate apps
- Allow unmanaged apps to read from managed contacts accounts
- AirDrop as an unmanaged destination
- Required encrypted backup
- Managed apps sync to cloud
- Control Center access while device locked
- Notification Center access while device locked
- Today view while device locked
- Block screenshots
- Block Enterprise Book backup
- Block Enterprise Book metadata sync
- Require encrypted backup
- Require watch wrist detection
- Block Siri
- Block Siri while device is locked
- Require Safari fraud warnings
- Block diagnostics submission to Apple


## Options not supported
The following options aren't supported on devices enrolled with User Enrollment. If you need these options, check out Device Enrollment for personally-owned devices or Automated Device Enrollment for corporate devices.
- Collect app inventory for apps outside of the managed APFS volume.
- Collect inventory of certificates and provisioning profiles outside of the managed APFS volume.
- Collect UDID and other persistent device identifiers, such as phone number, serial number, and IMEI
- User Enrollment supports a unique enrollment ID for each device enrolled, but this ID doesn't persist after unenrollment.
- The following Intune features aren't supported because of this limitation:
- SCEP User profiles with Subject Name Format of Serial Number.
- Device-level VPN.
- Device-licensed VPP app deployment.
- Install App Store apps as managed apps.
- MDM control of applications outside of the managed APFS volume.
- Application Protection Policies will still apply to these apps. However, you won't be able to take over management or deploy a managed version of these apps unless the user deletes them from their device.
- Actions, configurations, settings, and commands requiring supervision. 


## Known issues in preview
- VPP license revocation: A notification that the license has been revoked does not appear. The current behavior is that the revocation is successful, but the end user is not notified. 
- VPP application reporting: In the report located at Client Apps > Apps > [App Name] > Device Install Status, VPP applications deployed to User Enrolled devices are reporting as "failed", even when the application successfully deploys to the device. 
- VPP License Assignment: If the VPP license is already associated with the AppleID, or the user has another device enrolled with Device Enrollment, the license will associate to the AppleID successfully. However, if the only iOS device the user has enrolled is User Enrolled, the VPP license assignment will fail and install will fail with **Can't Find VPP License For App** (0x87D13B95). Re-enrolling the device with Device Enrollment to allow the assignment then re-enrolling again as User Enrollment resolves the assignment.
- Application reporting: For app types unsupported with User Enrollment, reports may provide irrelevant error messages. 
- Company Portal app experience: Users see all applications targeted to them, regardless of whether those application types are supported for User Enrolled devices. 
- Company Portal app experience: Users see the same text indicating what organizations can see for User and Device Enrollment if the admin has customized the text indicating what organizations can't see.


## Next steps

[Set up iOS/iPadOS and iPadOS User Enrollment](ios-user-enrollment.md)
