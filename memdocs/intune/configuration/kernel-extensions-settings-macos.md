---
# required metadata

title: macOS kernel extension settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add, configure, or create settings on macOS devices to use kernel extensions. Also, allow users to override approved extensions, allow all extensions from a team identifier, or allow specific extensions or apps in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/14/2020
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

# macOS device settings to configure and use kernel extensions in Intune

This article lists and describes the different kernel extension settings you can control on macOS devices. As part of your mobile device management (MDM) solution, use these settings to add and manage kernel extensions on your devices.

To learn more about kernel extensions in Intune, and any prerequisites, see [add macOS kernel extensions](kernel-extensions-overview-macos.md).

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

## Before you begin

[Create a macOS device kernel extensions configuration profile](kernel-extensions-overview-macos.md).

> [!NOTE]
> These settings apply to different enrollment types. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Kernel extensions

### Settings apply to: User approved device enrollment, Automated device enrollment

- **Allow User Overrides**: **Yes** lets users approve kernel extensions not included in the configuration profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from allowing extensions not included in the configuration profile. Meaning, only extensions included in the configuration profile are allowed.

  For more information on this feature, see [user-approved kernel extension loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (opens Apple's web site).

- **Allowed Team Identifiers**: Use this setting to allow one or many team IDs. Any kernel extensions signed with the team IDs you enter are allowed and trusted. In other words, use this option to allow all kernel extensions within the same team ID, which may be a specific developer or partner.

  **Add** a team identifier of valid and signed kernel extensions that you want to load. You can add multiple team identifiers. The team identifier must be alphanumeric (letters and numbers) and have 10 characters. For example, enter `ABCDE12345`.

  After you add a team identifier, it can also be deleted.

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's web site) has more information.

- **Allowed Kernel Extensions**: Use this setting to allow specific kernel extensions. Only the kernel extensions you enter are allowed or trusted.

  **Add** the bundle identifier and team identifier of a kernel extension that you want to load. For unsigned legacy kernel extensions, use an empty team identifier. You can add multiple kernel extensions. The team identifier must be alphanumeric (letters and numbers) and have 10 characters. For example, enter `com.contoso.appname.macos` for **Bundle ID**, and `ABCDE12345` for **Team identifier**.

  > [!TIP]
  > To get the Bundle ID of a kernel extension (Kext) on a macOS device, you can:
  >
  > 1. In the Terminal, run `kextstat | grep -v com.apple`, and note the output. Install the software or Kext that you want. Run `kextstat | grep -v com.apple` again, and look for changes.
  >
  >    In the Terminal, `kextstat` lists all the kernel extensions on the OS. 
  >
  > 2. On the device, open the Information Property List file (Info.plist) for a Kext. The bundle ID is shown. Each Kext has an Info.plist file stored inside.

> [!NOTE]
> You don't have to add team identifiers and kernel extensions. You can configure one or the other.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
