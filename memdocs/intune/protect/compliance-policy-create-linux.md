---
# required metadata

title: Linux device compliance settings in Microsoft Intune
description: View the device compliance settings that are available for Linux in Microsoft Intune.
keywords:
author: brenduns    
ms.author: brenduns
manager: dougeby
ms.date: 03/15/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
  - highseo
---

# Device compliance settings for Linux in Intune

This article lists and describes the different compliance settings you can configure for Linux devices in Intune.

For Linux, compliance settings are available from the [settings catalog](../configuration/settings-catalog.md) instead of from a pre-determined template as seen for other platforms. Therefore, when configuring a compliance policy for Linux you choose the settings you want to include in your policy by browsing the catalog and selecting them.

In addition to the platform-specific compliance policy, devices are also governed by tenant-wide compliance policy settings. To manage the tenant-wide compliance policy settings in your tenant, sign in to Microsoft Endpoint Manager admin center and go to **Endpoint security** > **Device compliance** > **Compliance policy settings**.

To learn more about compliance policies, and what they do, see [get started with device compliance](device-compliance-get-started.md).

This feature applies to:

- Linux

## Linux settings categories

Compliance policies for Linux can include settings from the following categories. Where applicable, guidance on configuring the setting is provided.

### Allowed Distros

Add entries that define a maximum and minimum OS version for a Linux distribution type.

Users of devices that fail to meet the defined criteria need to install a different version or distribution of Linux to bring the device into compliance.

### Custom Compliance

Add the settings in this category when you use custom compliance settings for Linux.

For information about the available settings for custom compliance and how to use them, see [Use custom compliance policies and settings for Linux and Windows devices with Microsoft Intune](../protect/compliance-use-custom-settings.md).

### Device Encryption

Add settings to manage disk encryption.

- **Require Device Encryption** – Specifies whether device-level encryption is required for writable fixed disks on this computer.

  Users of devices that aren’t encrypted receive a message that they must encrypt the drives to bring the device into compliance.

  There are several options for disk and partition encryption on Linux operating systems. At this time, Intune recognizes any encryption system that uses the underlying [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/-/wikis/DMCrypt) subsystem that has been standard on Linux systems for some time.

  The preferred method of setting up dm-crypt is to use the LUKS format with the [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/) tool.

  Keep the following things in mind when configuring encryption:

  - Encrypting Linux system volumes after installation is possible, but potentially very time consuming. Microsoft recommends setting up disk encryption while installing the operating system.
  - Not all filesystem partitions need to be encrypted to meet organizational standards. The following are ignored:
    - Read-only partitions
    - Pseudo-filesystems like */proc* or *tmpfs*
    - The */boot* or */boot/efi* partitions

### Password Policy

Enforce common password requirements for Linux devices:

- Minimum Lowercase - Specifies the minimum number of lowercase letters a password must contain.
- Minimum Uppercase - Specifies the minimum number of uppercase letters a password must contain.
- Minimum Symbols - Specifies the minimum number of symbols a password must contain.
- Minimum Length - Specifies the minimum number of total characters a password must contain.
- Minimum Digits - Specifies the minimum number of digits a password must contain.

Users that fail to meet password complexity requirements can receive a message that they must use a strong password to bring the device into compliance.

## Refresh compliance status

If you must modify a device’s configuration, use one of the following methods to refresh the device compliance status with Intune after making changes:

- If the Microsoft Intune app is still running, on the apps *device details* page or the *compliance issues* page, select the **Refresh** link. The device starts a new check-in.

- If the Microsoft Intune app isn't running, start the app and sign in. Signing in starts a new check-in.
- By default, the Microsoft Intune app periodically uses a background task to checks in while the computer is on and logged in.

## Next steps

- [Add actions for noncompliant devices](actions-for-noncompliance.md) and [use scope tags to filter policies](../fundamentals/scope-tags.md).
- [Monitor your compliance policies](compliance-policy-monitor.md).
