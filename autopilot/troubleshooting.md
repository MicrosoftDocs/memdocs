---
title: Windows Autopilot troubleshooting overview
description: Learn how to handle issues as they arise during the Windows Autopilot deployment process.
ms.subservice: itpro-deploy
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/04/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Troubleshooting overview

Windows Autopilot is designed to simplify all parts of the Windows device lifecycle, but there are always situations where issues might arise. When troubleshooting an issue, it's helpful to understand:

- The Windows Autopilot [process flow](#windows-autopilot-flow).
- How Windows Autopilot [device profiles](#profile-download) are downloaded.
- [Key activities](#key-troubleshooting-activities) to perform during troubleshooting.

## Windows Autopilot diagnostics page

On Windows 11, you can open the Autopilot diagnostic page to view additional detailed troubleshooting information about the Autopilot provisioning process. To enable the Autopilot diagnostics page:

1. Go to the [ESP profile](/mem/intune/enrollment/windows-enrollment-status) where the Autopilot diagnostics page needs to be enabled.

1. Make sure that **Show app and profile configuration progress** is selected to **Yes**.

1. Make sure that **Turn on log collection and diagnostics page for end users** is selected to **Yes**.

Once the diagnostic page is enabled, you can select the **View Diagnostics button** or use the keyboard shortcut **Ctrl**+**Shift**+**D** to access any diagnostic information. The Autopilot diagnostics page is currently supported for commercial OOBE, and Autopilot user-driven mode.

> [!NOTE]
>
> By default diagnostics are automatically collected upon an Autopilot failure. For more information, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

> [!NOTE]
>
> For diagnostics to be able to upload successfully from the client, make sure that the URL `lgmsapeweu.blob.core.windows.net` isn't blocked on the network.

## Windows Autopilot flow

Whether you're performing user-driven or self-deploying device deployments, the troubleshooting process is about the same. It's useful to understand the flow for a specific device:

1. A network connection is established. The connection can be a wireless (Wi-fi) or wired (Ethernet) connection.

1. The Windows Autopilot profile is downloaded. When you use a wired connection, or manually establish a wireless connection, the profile downloads from the Autopilot deployment service as soon as the network connection is in place.

1. User authentication occurs. During a user-driven deployment, the user enters their Microsoft Entra credentials, which is then validated.

1. Microsoft Entra join occurs. For user-driven deployments, the device is joined to Microsoft Entra ID using the specified user credentials. For self-deploying scenarios, the device is joined without specifying any user credentials.

1. Automatic mobile device management (MDM) enrollment occurs. As part of the Microsoft Entra join process, the device enrolls in the MDM service configured in Microsoft Entra ID (for example, Microsoft Intune).

1. Settings are applied. If the [enrollment status page](enrollment-status.md) is configured, most settings are applied while the enrollment status page is displayed. If not configured or available, settings will be applied after the user is signed in.

## Profile download

When an Internet-connected Windows device boots up, it attempts to connect to the Autopilot service and download an Autopilot profile. The Autopilot profile is downloaded as soon as possible, and again after each reboot.

> [!NOTE]
>
> At this stage, it's important that an Autopilot profile exists in the tenant so that a blank profile isn't cached locally on the device. If necessary, you can retrieve a new Autopilot profile by rebooting the device.
>
> If you need to reboot a computer during OOBE to retrieve a new Autopilot profile:
>
> 1. Press Shift-F10 on the keyboard to open a command prompt window.
>
> 1. In the command prompt window, enter one of the following two options:
>
>    1. Enter `shutdown.exe /r /t 0` to **restart** immediately.
>
>    1. Enter `shutdown.exe /s /t 0` to **shut down** immediately.
>
> For more information, see [Windows Setup Command-Line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

## Key troubleshooting activities

Key activities to perform when troubleshooting are:

- Review configuration: Has Microsoft Entra ID and Microsoft Intune (or an equivalent MDM service) been configured as specified in [Windows Autopilot configuration requirements](requirements.md?tabs=configuration)?
- Check network connectivity: Can the device access the services described in [Windows Autopilot networking requirements](requirements.md?tabs=networking)?
- Autopilot out-of-box experience (OOBE) behavior: Are the [expected OOBE](troubleshoot-oobe.md) screens displayed? Is the Microsoft Entra credentials page customized with organization-specific details as expected?
- Microsoft Entra join issues: Is the device able to [join Microsoft Entra ID](troubleshoot-aad-join.md)?
- MDM enrollment issues: IS the device able to [enroll in Microsoft Intune](troubleshoot-device-enrollment.md) (or an equivalent MDM service)?
- Review logs that are automatically collected upon Autopilot failure. For more information, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics). <!--1895390-->

## Next steps

See the following articles for help with troubleshooting specific issues:

- [Troubleshoot device enrollment](troubleshoot-device-enrollment.md).
- [Troubleshoot OOBE issues](troubleshoot-oobe.md).
- [Troubleshoot Microsoft Entra join issues](troubleshoot-aad-join.md).
- [Policy conflicts](policy-conflicts.md).
- [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).
- [Known issues](known-issues.md).

## Related content

- [Collect MDM logs](/windows/client-management/mdm-collect-logs).
