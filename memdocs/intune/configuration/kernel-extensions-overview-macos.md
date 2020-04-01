---
# required metadata

title: Create macOS kernel extensions device profile with Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add or create a macOS device profile, and then configure kernel extensions to allow user override, add team identifier, and a bundle and team identifier in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add macOS kernel extensions in Intune

> [!NOTE]
> macOS kernel extensions are being replaced with system extensions. For more information, see [Support Tip: Using system extensions instead of kernel extensions for macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

On macOS devices, you can add features at the kernel-level. These features access parts of the OS that regular programs can't access. Your organization may have specific needs or requirements that aren't available in an app, a device feature, and so on. 

To add kernel extensions that are always allowed to load on your devices, add "kernel extensions" (KEXT) in Microsoft Intune, and then deploy these extensions to your devices.

For example, you have a virus scanning program that scans your device for malicious content. You can add this virus scanning program's kernel extension as an allowed kernel extension in Intune. Then, "assign" the extension to your macOS devices.

With this feature, administrators can allow users to override kernel extensions, add team identifiers, and add specific kernel extensions in Intune.

This feature applies to:

- macOS 10.13.2 and later

To use this feature, devices must be:

- Enrolled in Intune using Apple's Device Enrollment Program (DEP). [Automatically enroll macOS devices](../enrollment/device-enrollment-program-enroll-macos.md) has more information.

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

> [!NOTE]
> The Intune user interface (UI) is updating to a full screen experience, and may take several weeks. Until your tenant receives this update, you will have a slightly different workflow when you create or edit settings described in this article.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **macOS**
    - **Profile**: Select **Extensions**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS: Add kernel extensions to devices**.
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

After the profile is created, it's ready to be assigned. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
