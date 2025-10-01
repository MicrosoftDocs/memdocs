---
title: Use Remote Help to assist users authenticated by your organization.
description: With the Remote Help app, provide remote assistance to authenticated users who also run the Remote Help app.
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

 # Use Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Microsoft Intune Remote Help is a cloud-based remote support solution that allows IT support teams to connect securely to an end-user's device for real-time assistance. It is available as a standalone add-on to Microsoft Intune, or as part of the Intune Suite, enabling organizations to provide remote troubleshooting and guidance with enterprise security controls in place. Remote Help distinguishes between helpers (support personnel) and sharers (end users sharing their screen), both of whom must sign in with corporate Entra ID accounts for each session. This requirement means Remote Help only works within your organization's tenant – helpers cannot assist users in another tenant or external organization.

## Remote Help capabilities

The Remote Help app supports the following capabilities in general across the supported platforms.

- **Enable Remote Help for your tenant**: By default, Remote Help is not eneabled for Intune tenants. If you choose to turn on Remote Help, its use is enabled tenant-wide. Remote Help must be enabled before users can be authenticated through your tenant when using Remote Help.

- **Requires Organization login**: To use Remote Help, both the helper and the sharer must sign in with a Microsoft Entra account from your organization. You can't use Remote Help to assist users who aren't members of your organization.

- **Compliance Warnings**: Before a helper connects to a user's device, the helper will see a non-compliance warning about that device if it's not compliant with its assigned policies.

- **Role-based access control**: Admins can set RBAC rules that determine the scope of a helper's access, such as:
  - The users who can help others and the range of actions they can do while providing help. For example, who can run elevated privileges while helping.
  - The users who can only view a device, and who can request full control of the session while assisting others.

- **Monitor active Remote Help sessions, and view details about past sessions**: In the Microsoft Intune admin center, you can view reports that include details about who helped who, on what device, and for how long. You can also find details about active sessions. An administrator can also reference audit log sessions created for Remote Help in Intune under **Tenant Administration** > **Audit Logs**.

  For unenrolled devices, auditing the Remote Help sessions is limited.

## Platform-specific capabilities

- **Optional support for unenrolled devices**: This setting is turned off by default. For Windows and macOS devices, enabling this option allows help to be provided to devices that aren't enrolled in Intune. This setting does not apply to devices used by helpers.

- **Conditional access support for macOS and Windows**: You can use Conditional Access policies to control how helpers and sharers access Remote Help. For example, you can require multi-factor authentication (MFA) for helpers or restrict access to specific locations or compliant devices.

### Android

- **Unattended access**: Helpers can connect to Android devices without requiring the sharer to accept the connection each time. This capability requires the Android device to be enrolled in Intune as a fully managed device or as a dedicated device.

## Try an interactive demo

The [Remote Help]( https://regale.cloud/Microsoft/viewer/1746/remote-help/index.html#/0/0) interactive demo walks you through scenarios step-by-step with interactive annotations and navigation controls.

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
