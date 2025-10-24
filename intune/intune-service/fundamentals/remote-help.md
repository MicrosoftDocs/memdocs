---
title: Use Remote Help to Assist Users Authenticated by your Organization
description: With the Remote Help app, provide remote assistance to authenticated users who also run the Remote Help app.
author: lenewsad
ms.author: lanewsad
ms.date: 03/18/2025
ms.topic: how-to
ms.reviewer: karawang
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

 # Use Remote Help with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Microsoft Intune Remote Help is a cloud-based remote support solution that allows IT support teams to connect securely to an end-user's device for real-time assistance. It's available as a standalone add-on to Microsoft Intune, or as part of the Intune Suite, enabling organizations to provide remote troubleshooting and guidance with enterprise security controls in place. Remote Help distinguishes between helpers (support personnel) and sharers (end users sharing their screen), both of whom must sign in with corporate Entra ID accounts for each session. This requirement means Remote Help only works within your organization's tenant – helpers can't assist users in another tenant or external organization.

## Remote Help capabilities

The Remote Help app supports the following capabilities in general across the supported platforms.

- **Enable Remote Help for your tenant**: By default, Remote Help isn't enabled for Intune tenants. If you choose to turn on Remote Help, its use is enabled tenant-wide. Remote Help must be enabled before users can be authenticated through your tenant when using Remote Help.
  
  :::image type="content" source="media/remote-help/remote-help-enable.png" alt-text="A screenshot of the tenant administration screen where you can enable Remote Help." lightbox="media/remote-help/remote-help-enable-expanded.png":::

- **Requires Organization login**: To use Remote Help, both the helper and the sharer must sign in with a Microsoft Entra account from your organization. You can't use Remote Help to assist users who aren't members of your organization.
  
  :::image type="content" source="media/remote-help/remote-help-organizational-account.png" alt-text="Screenshot of Remote Help requiring an organizational account.":::

- **Compliance Warnings**: Before a helper connects to a user's device, helpers see a noncompliance warning about that device if it's not compliant with its assigned policies.

- **Role-based access control**: Admins can set RBAC rules that determine the scope of a helper's access, such as:
  - The users who can help others and the range of actions they can do while providing help. For example, who can run elevated privileges while helping.
  - The users who can only view a device, and who can request full control of the session while assisting others.

- **Monitor active Remote Help sessions, and view details about past sessions**: In the Microsoft Intune admin center, you can view reports that include details about who helped who, on what device, and for how long. You can also find details about active sessions. An administrator can also reference audit log sessions created for Remote Help in Intune under **Tenant Administration** > **Audit Logs**.

  For unenrolled devices, auditing the Remote Help sessions is limited.

- **Web app for sharers** - In situations where the Sharer needs assistance but is unable to install the native application for macOS or Windows, the Sharer can use the Web App to share their screen to a helper. This web app provides view only capabilities to the helper, allowing them to guide the user through resolving issues.

## Platform-specific capabilities

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

- **Elevation**: Allows helpers to enter UAC credentials when prompted on the sharer's device. Enabling elevation also allows the helper to view and control the sharer's device when the sharer grants the helper access.
  
  :::image type="content" source="media/remote-help/remote-help-windows-elevation.png" alt-text="Screenshot of the prompt to enable elevation support during a remote help session on Windows." lightbox="media/remote-help/remote-help-windows-elevation-expanded.png":::
- **Remote launch**: Allows helpers to launch Remote Help on the helper and sharer's device from Intune by sending a notification to the sharer's device.
  
  :::image type="content" source="media/remote-help/remote-help-windows-remote-launch.png" alt-text="A screenshot of the sharer's computer showing the prompt to start a Remote Help session using the Remote Launch feature.":::
- **Optional support for unenrolled devices**: This setting is turned off by default. Enabling this option allows help to be provided to devices that aren't enrolled in Intune. This setting doesn't apply to devices used by helpers.
  
  :::image type="content" source="media/remote-help/remote-help-unenrolled.png" alt-text="A screenshot of the option to enable unenrolled devices":::
- **Conditional access support**: You can use Conditional Access policies to control how helpers and sharers access Remote Help. For example, you can require multifactor authentication (MFA) for helpers or restrict access to specific locations or compliant devices.
- **Chat functionality**: Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages Supported](remote-help-plan.md#supported-languages-for-chat).
- **Web app for sharers** - In situations where the Sharer needs assistance but is unable to install the native application for macOS, the Sharer can use the Web App to share their screen to a helper. This web app provides view only capabilities to the helper, allowing them to guide the user through resolving issues.

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

- **Conditional access support**: You can use Conditional Access policies to control how helpers and sharers access Remote Help. For example, you can require multifactor authentication (MFA) for helpers or restrict access to specific locations or compliant devices.
- **Chat functionality**: Remote Help includes enhanced chat that maintains a continuous thread of all messages. This chat supports special characters and other languages including Chinese and Arabic. For more information on languages supported, see [Languages Supported](remote-help-plan.md#supported-languages-for-chat).
- **Optional support for unenrolled devices**: This setting is turned off by default. For Windows and macOS devices, enabling this option allows help to be provided to devices that aren't enrolled in Intune. This setting doesn't apply to devices used by helpers.
  
  :::image type="content" source="media/remote-help/remote-help-unenrolled.png" alt-text="A screenshot of the opion to enable unenrolled devices":::

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

- **Unattended access**: Helpers can connect to Android devices without requiring the sharer to accept the connection each time. This capability requires the Android device to be enrolled in Intune as a fully managed device or as a dedicated device.
  
  :::image type="content" source="media/remote-help/remote-help-android-unattended.png" alt-text="Screenshot of an unattended Remote Help session on Android" lightbox="media/remote-help/remote-help-android-unattended-expanded.png":::

---

## Demos and Videos

### [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

The [Remote Help]( https://regale.cloud/Microsoft/viewer/1746/remote-help/index.html#/0/0) interactive demo walks you through scenarios step-by-step with interactive annotations and navigation controls.

### [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

Use the interactive demos to explore Remote Help on macOS:

- [macOS native experience](https://regale.cloud/microsoft/play/1746/remote-help#/7/0)
- [macOS web app experience](https://regale.cloud/microsoft/play/1746/remote-help#/6/0)

### [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

Check back in this space for demos and videos of Remote Help for Android.  
---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Plan Remote Help >](remote-help-plan.md)
