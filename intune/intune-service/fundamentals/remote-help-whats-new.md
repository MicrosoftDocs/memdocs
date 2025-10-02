---
title: What's new in Remote Help with Microsoft Intune
description: Find out what's new in Remote Help with Microsoft Intune.
author: lenewsad
ms.author: lanewsad
ms.date: 03/18/2025
ms.topic: how-to
ms.localizationpriority: high
ms.reviewer: karawang
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

 # What's new in Remote Help

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [remote-help-overview](includes/remote-help-overview.md)]

## What's New for Remote Help Windows

Updates for Remote Help are released periodically. When we update Remote Help, you can read about the changes here.

### March 21, 2025

Version: 5.1.1998.0

- Added support for users on multi-session AVD

- Resolved accessibility bugs

### June 25, 2024

Version 5.1.1419.0

- Resolve issue where the screen may be blank on first launch.

### March 13, 2024

Version: 5.1.1214.0

- Changed the primary endpoint for Remote Help from https://remoteassistance.support.services.microsoft.com to https://remotehelp.microsoft.com.
  > [!NOTE]
  > This could cause a breaking change for some organizations that have not yet allowed remotehelp.microsoft.com through their firewall after 5/30/2024.
- Resolved various bugs including an issue with Conditional Access. If a tenant had a **Terms of Use** policy enabled for Office 365, Remote Help wouldn't know how to respond and would instead present an authentication error message to the user.
- Enabled a shortcut to open context menus with the keyboard shortcut 'Alt + Space'

### October 25, 2023

Version: 5.0.1311.0

- Disabled the relaying of system audio from the Sharer device to the Helper device, which caused an echo when both users were using another app to communicate (such as Teams).
- Added the capability for Helpers that have elevation permissions to also be able to elevate apps on devices where the Sharer is an Administrator.

### September 7, 2023

Version: 5.0.1045.0

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and sharer's device from Intune by sending a notification to the sharer's device.

### July 13, 2023

Version: 5.0.1045.0
This version of Remote Help provides support for ARM64 devices including the Microsoft Surface Pro X and Parallels Desktop on macOS.

### June 20, 2023

Version: 4.2.1424.0
With Remote Help 4.2.1424.0, a new in-session connection mode feature provides users with a way to seamlessly switch between full control and view-only modes during a remote assistance session.

### May 1, 2023

Version: 4.2.1270.0

This version includes a minor update that enables future functionality.

- Added support for slashes within the Remote Help URI (to enable future functionality)

### March 27, 2023

Version: 4.2.1167.0 - Changes in this release:

This release addresses a bug in the Laser Pointer and includes some updates to prepare for future releases.

- Updated product name from **Remote help** to **Remote Help**
- Updated application description to better localize it for non-US locales
- Resolved a bug where the app would flash a white screen when launched in dark mode
- Fixed a bug with the Laser pointer color change

### February 6, 2023

Version: 4.1.1.0 - Changes in this release:

A new Laser Pointer feature has been added to better assist a helper guide a sharer during a session. A helper can use the Laser Pointer in both Full Control and View Only sessions. Other updates include improvements to localization, and error handling.

Various bug fixes included in this release:

- Fixed an issue where in some cases a helper is unable to interact with elevated applications

- Resolved an accessibility issue where a helper was unable to use some keyboard navigation hotkeys

- Reliability fixes and improved logging for WebView2 integration

### September 6, 2022

Version: 4.0.1.13 - Changes in this release:

Fixes were introduced to address an issue that prevented people from having multiple sessions open at the same time. The fixes also addressed an issue where the app was launching without focus, and prevented keyboard navigation and screen readers from working on launch.

For more information, go to [Use Remote Help with Intune](remote-help.md).

### July 26, 2022

Version: 4.0.1.12 - Changes in this release:

Various fixes were introduced to address the 'Try again later' message that appears when not authenticated. The fixes also include an improved auto-update capability.

### May 11, 2022

Version 4.0.1.7 - Webview 2 release

### April 5, 2022

Version 4.0.0.0 - GA release

## Next Steps

> [!div class="nextstepaction"]
> [Next: Plan Remote Help >](remote-help-plan.md)
