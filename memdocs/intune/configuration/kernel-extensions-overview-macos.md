---
# required metadata

title: Create macOS kernel extensions device profile with Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add or create a macOS device profile, and then configure kernel extensions to allow user override, add team identifier, and a bundle and team identifier in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add macOS kernel extensions in Intune

On macOS devices, you can add features at the kernel-level. These features access parts of the OS that regular programs can't access. Your organization may have specific needs or requirements that aren't available in an app, a device feature, and so on. 

To add kernel extensions that are always allowed to load on your devices, add "kernel extensions" (KEXT) in Microsoft Intune, and then deploy these extensions to your devices.

For example, you have a virus scanning program that scans your device for malicious content. You can add this virus scanning program's kernel extension as an allowed kernel extension in Intune. Then, "assign" the extension to your macOS devices.

With this feature, administrators can allow users to override kernel extensions, add team identifiers, and add specific kernel extensions in Intune.

This feature applies to:

- macOS 10.13.2 and later

To use this feature, devices must be:

- Enrolled in Intune using Apple's Device Enrollment Program (DEP). [Automatically enroll macOS devices](../intune/enrollment/device-enrollment-program-enroll-macos.md) has more information.

  OR

- Enrolled in Intune with "user approved enrollment" (Apple's term). [Prepare for changes to kernel extensions in macOS High Sierra](https://support.apple.com/en-us/HT208019) (opens Apple's web site) has more information.

Intune uses "configuration profiles" to create and customize these settings for your organization's needs. After you add these features in a profile, you can then push or deploy the profile to macOS devices in your organization.

This article shows you how to create a device configuration profile using kernel extensions in Intune.

> [!TIP]
> For more information on kernel extensions, see [kernel extension overview](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (opens Apple's web site).

## What you need to know

- Unsigned legacy kernel extensions can be added.
- Be sure to enter the correct team identifier and bundle ID of the kernel extension. Intune doesn't validate the values you enter. If you enter wrong information, the extension won't work on the device. A team identifier is exactly 10 alphanumeric characters long. 

> [!NOTE]
> Apple released information regarding signing and notarization for all software. On macOS 10.14.5 and newer, kernel extensions deployed through Intune don't have to meet Apple's notarization policy.
>
> For information on this notarization policy, and any updates or changes, see the following resources:
>
> - [Notarizing your app before distribution](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (opens Apple's web site) 
> - [Prepare for changes to kernel extensions in macOS High Sierra](https://support.apple.com/en-us/HT208019) (opens Apple's web site)

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Select **macOS**
    - **Profile type**: Select **Extensions**.
    - **Settings**: Enter the settings you want to configure. For a list of all settings, and what they do, see:

        - [macOS](kernel-extensions-settings-macos.md)

4. When you're done, select **OK** > **Create** to save your changes.

The profile is created and shown in the list. Be sure to [assign the profile](../device-profile-assign.md) and [monitor its status](../device-profile-monitor.md).

## Next steps

After the profile is created, it's ready to be assigned. Next, [assign the profile](../device-profile-assign.md) and [monitor its status](../device-profile-monitor.md).
