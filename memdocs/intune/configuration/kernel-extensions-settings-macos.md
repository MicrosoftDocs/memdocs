---
# required metadata

title: macOS extension settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add, configure, or create settings on macOS devices to use system extensions and kernel extensions. Also, allow users to override approved extensions, allow all extensions from a team identifier, or allow specific extensions or apps in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/25/2021
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

# macOS device settings to configure and use kernel and system extensions in Intune

> [!NOTE]
> macOS kernel extensions are being replaced with system extensions. For more information, see [Support Tip: Using system extensions instead of kernel extensions for macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

This article describes the different kernel and system extension settings you can control on macOS devices. As part of your mobile device management (MDM) solution, use these settings to add and manage extensions on your devices.

To learn more about extensions in Intune, and any prerequisites, see [add macOS extensions](kernel-extensions-overview-macos.md).

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

## Before you begin

Create a [macOS extensions device configuration profile](kernel-extensions-overview-macos.md).

> [!NOTE]
> These settings apply to different enrollment types. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Kernel extensions

This feature applies to:

- macOS 10.13.2 and newer
- User approved device enrollment is required 

> [!IMPORTANT]
> Kernel extensions don't work on macOS devices with the M1 chip, which are macOS devices running on Apple silicon. This behavior is a known issue, with no ETA.
> 
> For any macOS devices running 10.15 and newer, we recommend using [system extensions](#system-extensions) (in this article). If you use the kernel extensions settings, then consider excluding macOS devices with M1 chips from receiving the kernel extensions profile.

### Settings apply to: User approved device enrollment, Automated device enrollment

- **Allow User Overrides**: **Yes** lets users approve kernel extensions not included in the configuration profile. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might prevent users from allowing extensions not included in the configuration profile. Meaning, only extensions included in the configuration profile are allowed.

  For more information on this feature, see [user-approved kernel extension loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (opens Apple's web site).

- **Allowed Team Identifiers**: Use this setting to allow one or many team IDs. Any kernel extensions signed with the team IDs you enter are allowed and trusted. In other words, use this option to allow all kernel extensions within the same team ID, which may be a specific developer or partner.

  **Add** a team identifier of valid and signed kernel extensions to load. You can add multiple team identifiers. The team identifier must be alphanumeric (letters and numbers) and have 10 characters. For example, enter `ABCDE12345`.

  After you add a team identifier, it can also be deleted.

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's web site) has more information.

  > [!TIP]
  > The Team ID is stored on the local KextPolicy database. You can get the Team ID using the `sqlite3` command from a macOS device that has the same app installed:
  >
  > 1. On the macOS device, open the Terminal app, and run the following script:
  >
  >     `sudo /Volumes/Macintosh\ HD/usr/bin/sqlite3 /Volumes/Macintosh\ HD/var/db/SystemPolicyConfiguration/KextPolicy "SELECT * from kext_policy"`
  >
  >     - In our example, the volume name is **Macintosh HD**. Update the script with your volume name.
  >     - Be sure you have root access, and can run a `SUDO` command on the device.
  >
  > 2. Review the output. The first entry is the Team ID. In our example, the Team ID is `PXPZ95SK77`:
  > 
  >     `PXPZ95SK77|com.paloaltonetworks.kext.pangpd|1|Palo Alto Networks|5`

- **Allowed Kernel Extensions**: Use this setting to allow specific kernel extensions. Only the kernel extensions you enter are allowed or trusted.

  **Add** the bundle identifier and team identifier of a kernel extension to load. For unsigned legacy kernel extensions, use an empty team identifier. You can add multiple kernel extensions. The team identifier must be alphanumeric (letters and numbers) and have 10 characters. For example, enter `com.contoso.appname.macos` for **Bundle ID**, and `ABCDE12345` for **Team identifier**.

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

## System extensions

This feature applies to:

- macOS 10.15 and newer
- User approved device enrollment is required

### Settings apply to: User approved device enrollment, Automated device enrollment

- **Block User Overrides**: **Yes** prevents users from approving system extensions that aren't in the allowed list. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to approve unknown extensions not included in the configuration profile. Meaning, extensions not included in the configuration profile are allowed.

- **Allowed team identifiers**: Use this setting to allow one or many team IDs. Any system extensions signed with the team IDs you enter are always allowed and trusted. In other words, use this option to allow all system extensions within the same team ID, which may be a specific developer or partner.

  **Add** a **Team identifier** of valid and signed system extensions to load. You can add multiple team identifiers. The team identifier must be alphanumeric (letters and numbers) and have 10 characters. For example, enter `ABCDE12345`.

  After you add a team identifier, it can also be deleted.

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's web site) has more information.

  > [!TIP]
  > You can also get the Team ID from a mac where the application is installed
  > 
  > In the Terminal, run:
  >
  > `systemextensionsctl list`
  >
  > and note the output:
  >
  > E.g. `UBF8T346G9	com.microsoft.wdav.netext (101.04.48/101.04.48)	Microsoft Defender for Endpoint Network Extension`
  >
  > The first entry is the Team ID you need. `UBF8T346G9` in our example

- **Allowed system extensions**: Use this setting to always allow specific system extensions. Only the system extensions you enter are allowed or trusted.

  **Add** the **Bundle identifier** and **Team identifier** of a system extension to load. For unsigned legacy system extensions, use an empty team identifier. You can add multiple system extensions. The team identifier must be alphanumeric (letters and numbers) and have 10 characters. For example, enter `com.contoso.appname.macos` for **Bundle ID**, and `ABCDE12345` for **Team identifier**.

- **Allowed system extension types**: Enter the Team ID, and system extension types to allow for that Team ID:
  - **Team identifier**: Enter the Team ID of another system extension you want to allow specific extension types. Or, enter a Team ID you added to **Allowed system extensions**.
  - **Allowed system extension types**: Select the system extension types to allow for each Team ID. Your options:
    - Select all
    - Driver extensions
    - Network extensions
    - Endpoint security extensions

    For more information on these extension types, see [System Extensions](https://developer.apple.com/system-extensions/) (opens Apple's web site).

    You can add a team ID from the **Allowed system extensions** list, and allow a specific extension type. If the extension is a type that isn't allowed, then the extension might not run.

    To allow all extension types for a Team ID, add the Team ID to the **Allowed system extensions** list. Don't add the Team ID to the **Allowed system extension types** list. In other words, if a team ID is in the **Allowed system extensions** list, and not in the **Allowed system extension types** list, then all extension types are allowed for that team ID.

> [!NOTE]
> Adding the same Team ID for **Allowed system extensions** and **Allowed team identifiers** can result in an error and the profile failing. Don't add the same exact Team Identifier to both settings. 

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
