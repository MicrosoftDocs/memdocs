---
# required metadata

title: Setup Intune enrollment for Android Enterprise fully managed devices
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise fully managed devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/9/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up Intune enrollment of Android Enterprise fully managed devices

Android Enterprise fully managed devices are corporate-owned devices associated with a single user and used exclusively for work and not personal use. Admins can manage the entire device and enforce policy controls unavailable to personally-owned/corporate-owned work profiles, such as:

- Allow app installation only from Managed Google Play.
- Block uninstallation of managed apps.
- Prevent users from factory resetting devices, and so on.

Microsoft Intune helps you deploy apps and settings to Android Enterprise devices, including Android Enterprise fully managed devices. For specific details about Android Enterprise, see [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## Technical requirements

You must have an Intune standalone tenant to manage Android Enterprise fully managed devices. Devices must meet these requirements to be managed as an Android Enterprise fully managed device:

- Android OS version 8.0 and above.
- Devices must run a build of Android that has Google Mobile Services (GMS) connectivity. Devices must have GMS available and must be able to connect to GMS.

There is no restriction on device manufacturer/OEM if the above requirements are met.

## Set up Android Enterprise fully managed device management

To set up Android Enterprise fully managed device management, follow these steps:

1. To prepare to manage mobile devices, you must [set the mobile device management (MDM) authority to **Microsoft Intune**](../fundamentals/mdm-authority-set.md). You set this item only once, when you're first setting up Intune for mobile device management.
2. [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md).
3. [Enable corporate-owned user devices](#enable-corporate-owned-user-devices)
4. [Enroll the fully managed devices](#enroll-the-fully-managed-devices).

### Enable corporate owned user devices

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Android** > **Android enrollment**  > **Corporate-owned, fully managed user devices**.
2. Under **Allow users to enroll corporate-owned user devices**, choose **Yes**.

> [!NOTE]
> If you have an Azure AD Conditional Access policy defined that uses the *require a device to be marked as compliant* Grant control or a Block policy and applies to **All Cloud apps**, **Android**, and **Browsers**, you must exclude the **Microsoft Intune** cloud app from this policy. This is because the Android setup process uses a Chrome tab to authenticate your users during enrollment. For more information, see [Azure AD Conditional Access documentation](/azure/active-directory/conditional-access/).

When this setting is set to **Yes**, it provides you with an enrollment token (a random string) and a QR code for your Intune tenant. This single enrollment token is valid for all your users and won't expire. Depending on the Android OS and version of the device, you can use either the token or QR code to enroll the device.

## Enroll the fully managed devices

You can now [enroll your fully managed devices](android-dedicated-devices-fully-managed-enroll.md) (but not when using DEM accounts).

## Next steps

- [Add Android Enterprise fully managed device configuration policies](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)
- [Configure app configuration policies for Android Enterprise fully managed devices](../apps/app-configuration-policies-use-android.md)
