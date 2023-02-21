---
# required metadata

title: Intune actions and options supported with Apple User Enrollment
titleSuffix: Microsoft Intune
description: Learn which Intune actions and options are supported with Apple User Enrollment
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/15/2022
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
ms.collection:
- tier2
- M365-identity-device-management
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
- SCEP User profiles with Subject Name Format of Serial Number.
- Device-level VPN.
- Device-licensed VPP app deployment.
- Install App Store apps as managed apps.
- MDM control of applications outside of the managed APFS volume.
  - Application Protection Policies will still apply to these apps. However, you won't be able to take over management or deploy a managed version of these apps unless the user deletes them from their device.
- Actions, configurations, settings, and commands requiring supervision. 
- Customized privacy text in the Company Portal. If the admin has customized the text indicating what organizations can/can't see, then users will see the same text indicating what organizations can/can't see for User and Device Enrollment in the Company Portal. 
- Devices running iOS 15.5 cannot enroll with User Enrollment if MFA text or call is needed on the same device during enrollment. 
- Devices running iOS 15.7 through iOS 16.3 cannot enroll with User Enrollment with MFA text. MFA call must be used in order to enroll with User Enrollment if MFA is needed on the same device during enrollment. 
- Application reporting for app types unsupported with User Enrollment. 


## Next steps

[Set up iOS/iPadOS and iPadOS User Enrollment](ios-user-enrollment.md)
