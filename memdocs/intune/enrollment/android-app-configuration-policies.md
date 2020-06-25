---
# required metadata

title: Android Enterprise security configuration framework
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings suggested for Android Enterprise device basic and high security.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
---

# Android Enterprise security configuration framework app configuration policies

As part of the [Android Enterprise security configuration framework](android-configuration-framework.md), you must properly set app configuration polices for Android Enterpise devices.

Android Enterprise work profile devcies are designed to make sure that work and personal data are isolated from each another. Android Enterprise fully managed devices are designed work or school data only. Therefore, Microsoft apps deployed on these devices must be configured to disallow personal accounts.

## Disallow personal accounts for Microsoft apps on Android Enteprise devices

1. Add the apps to Managed Google Play. For more information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work).
2. Create a policy for each Managed Google Play app as described in [Add app configuration policies for managed Android Enterprise devices]().
3. Create the following single key in each policy:

    | Key | Values |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | One or more ; delimited UPNs.<br>Only account(s) allowed are the managed user account(s) defined by this key.<br>For Intune enrolled devices, the {{userprincipalname}} token may be used to represent the enrolled user account. |


## Next steps
Apply [Android Enterprise work profile security settings](android-work-profile-security-settings.md) or [Android Enterprise fully managed security settings](android-fully-managed-security-settings.md).