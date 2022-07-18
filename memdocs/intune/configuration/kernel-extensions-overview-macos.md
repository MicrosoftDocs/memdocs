---
# required metadata

title: Create macOS system and kernel extensions with Microsoft Intune
titleSuffix:
description: Add or create a macOS device profile that configures system extensions or kernel extensions to allow user override, adds team identifier, and adds a bundle and team identifier in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/19/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add macOS system and kernel extensions in Intune

> [!NOTE]
> macOS kernel extensions are being replaced with system extensions. For more information, see [Support Tip: Using system extensions instead of kernel extensions for macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

On macOS devices, you can add kernel extensions and system extensions. Both kernel extensions and system extensions allow users to install app extensions that extend the native capabilities of the operating system. Kernel extensions execute their code at the kernel level. System extensions run in a tightly controlled user-space.

To add extensions that are always allowed to load on your devices, use Microsoft Intune. Intune uses "configuration profiles" to create and customize these settings for your organization's needs. After you add these features in a profile, you then push or deploy the profile to macOS devices in your organization.

This article describes system extensions and kernel extensions. It also shows you how to create a device configuration profile using extensions in Intune.

## System extensions

System extensions run in the user space, and don’t access the kernel. The goal is to increase security, provide more end user control, and limit kernel level attacks. These extensions can be:

- Driver extensions, including drivers to USB, network interface cards (NIC), serial controllers, and human interface devices (HID)
- Network extensions, including content filters, DNS proxies, and VPN clients
- Endpoint security extensions, including endpoint detection, endpoint response, and antivirus

System extensions are included in an app's bundle, and installed from the app.

For more information on system extensions, see [system extensions](https://developer.apple.com/documentation/systemextensions) (opens Apple's web site).

## Kernel extensions

Kernel extensions add features at the kernel-level. These features access parts of the OS that regular programs can't access. Your organization may have specific needs or requirements that aren't available in an app, a device feature, and so on.

For example, you have a virus scanning program that scans your device for malicious content. You can add this virus scanning program's kernel extension as an allowed kernel extension in Intune. Then, "assign" the extension to your macOS devices.

With this feature, administrators can allow users to override kernel extensions, add team identifiers, and add specific kernel extensions in Intune.

For more information on kernel extensions, see [kernel extensions](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (opens Apple's web site).

> [!IMPORTANT]
> Kernel extensions don't work on macOS devices with the M1 chip, which are macOS devices running on Apple silicon. This behavior is a known issue, with no ETA. It's possible you can get them to work, but it's not recommended. For more information, see [Kernel extensions in macOS](https://support.apple.com/guide/deployment-reference-macos/kernel-extensions-in-macos-apd37565d329/web) (opens Apple's web site).
> 
> For any macOS devices running 10.15 and newer, we recommend using [system extensions](#system-extensions) (in this article). If you use the kernel extensions settings, then consider excluding macOS devices with M1 chips from receiving the kernel extensions profile.

## Prerequisites

- This feature applies to:

  - macOS 10.13.2 and newer (kernel extensions)
  - macOS 10.15 and newer (system extensions)

  From macOS 10.15 to 10.15.4, kernel extensions and system extensions can run side by side.

- To use this feature, devices must be:

  - Enrolled in Intune using Apple's Device Enrollment Program (DEP). [Automatically enroll macOS devices](../enrollment/device-enrollment-program-enroll-macos.md) has more information.

    OR

  - Enrolled in Intune with "user approved enrollment" (Apple's term). [Prepare for changes to kernel extensions in macOS High Sierra](https://support.apple.com/en-us/HT208019) (opens Apple's web site) has more information.

## What you need to know

- Unsigned legacy kernel extensions and system extensions can be added.
- Be sure to enter the correct team identifier and bundle ID of the extension. Intune doesn't validate the values you enter. If you enter wrong information, the extension won't work on the device. A team identifier is exactly 10 alphanumeric characters long.

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

    - **Platform**: Select **macOS**
    - **Profile**: Select **Templates** > **Extensions**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS: Add AV scanning to kernel extensions on devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, configure your settings:

    - [macOS](kernel-extensions-settings-macos.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Next steps

Be sure to [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
