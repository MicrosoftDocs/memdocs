---
title: Windows Autopilot troubleshooting overview
description: Learn how to handle issues as they arise during the Windows Autopilot deployment process.
ms.technology: itpro-deploy
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
---


# Troubleshooting overview

*Applies to:*

- Windows 11
- Windows 10

Windows Autopilot is designed to simplify all parts of the Windows device lifecycle, but there are always situations where issues may arise. When troubleshooting an issue, it is helpful to understand:

- The Windows Autopilot [process flow](#windows-autopilot-flow)
- How Windows Autopilot [device profiles](#profile-download) are downloaded
- [Key activities](#key-troubleshooting-activities) to perform during troubleshooting

## Windows Autopilot diagnostics page
On Windows 11, you can open the Autopilot diagnostic page to view additional detailed troubleshooting information about the Autopilot provisioning process. To enable the Autopilot diagnostics page:

1. Go to the [ESP profile](../intune/enrollment/windows-enrollment-status.md) where the Autopilot diagnostics page needs to be enabled.
2. Make sure that **Show app and profile configuration progress** is selected to **Yes**.
3. Make sure that **Turn on log collection and diagnostics page for end users** is selected to **Yes**.

Once the diagnostic page is enabled, you can select the **View Diagnostics button** or use the keyboard shortcut **Ctrl**+**Shift**+**D** to access any diagnostic information. The Autopilot diagnostics page is currently supported for commercial OOBE, and Autopilot user-driven mode.

> [!NOTE]
> By default diagnostics will be automatically collected upon an Autopilot failure. For more information, see [Collect diagnostics from a Windows device](../intune/remote-actions/collect-diagnostics.md)

> [!NOTE]
> For diagnostics to be able to upload successfully from the client, make sure that the URL `lgmsapeweu.blob.core.windows.net` is not blocked on the network.

## Windows Autopilot flow

Whether you're performing user-driven or self-deploying device deployments, the troubleshooting process is about the same. It's useful to understand the flow for a specific device:

1. A network connection is established. The connection can be a wireless (Wi-fi) or wired (Ethernet) connection.
2. The Windows Autopilot profile is downloaded. When you use a wired connection, or manually establish a wireless connection, the profile downloads from the Autopilot deployment service as soon as the network connection is in place.
3. User authentication occurs. When performing a user-driven deployment, the user will enter their Azure Active Directory credentials, which will be validated.
4. Azure Active Directory join occurs. For user-driven deployments, the device will be joined to Azure AD using the specified user credentials. For self-deploying scenarios, the device will be joined without specifying any user credentials.
5. Automatic MDM enrollment occurs. As part of the Azure AD join process, the device will enroll in the MDM service configured in Azure AD (for example, Microsoft Intune).
6. Settings are applied. If the [enrollment status page](enrollment-status.md) is configured, most settings will be applied while the enrollment status page is displayed. If not configured or available, settings will be applied after the user is signed in.

## Profile download

When an Internet-connected Windows device boots up, it will attempt to connect to the Autopilot service and download an Autopilot profile. The Autopilot profile is downloaded as soon as possible, and again after each reboot.

> [!NOTE]
> At this stage, it's important that an Autopilot profile exists in the tenant so that a blank profile isn't cached locally on the device. If necessary, you can retrieve a new Autopilot profile by rebooting the device.
>
> If you need to reboot a computer during OOBE to retrieve a new Autopilot profile:
> 1. Press Shift-F10 on the keyboard to open a command prompt window.
> 2. In the command prompt window, enter one of the following two options:
>    1. Enter `shutdown.exe /r /t 0` to **restart** immediately.
>    2. Enter `shutdown.exe /s /t 0` to **shut down** immediately.
>
> For more information, see [Windows Setup Command-Line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

<!-- To remove the currently cached local profile in Windows 10 version 1803 and earlier, it's necessary to re-generalize the OS using **sysprep /generalize /oobe**, reinstall the OS, or re-image the PC. -->
 
<!-- In Windows 10 version 1809 and later, -->

<!-- When a profile is downloaded depends upon the version of Windows client that is running on the PC. See the following table.

| Windows 10 version | Profile download behavior |
| --- | --- |
| 1709 | The profile is downloaded after the OOBE network connection page. This page isn't displayed when using a wired connection. In this case, the profile is downloaded before the EULA screen. |
| 1803 | The profile is downloaded as soon as possible. If wired, it's downloaded at the start of OOBE. If wireless, it's downloaded after the network connection page. |
| 1809 | The profile is downloaded as soon as possible (same as 1803), and again after each reboot. | -->

## Key troubleshooting activities

For troubleshooting, key activities to perform are:

- Review configuration: Has Azure Active Directory and Microsoft Intune (or an equivalent MDM service) been configured as specified in [Windows Autopilot configuration requirements](configuration-requirements.md)?
- Check network connectivity: Can the device access the services described in [Windows Autopilot networking requirements](networking-requirements.md)?
- Autopilot out-of-box experience (OOBE) behavior: Are the [expected OOBE](troubleshoot-oobe.md) screens displayed? Is the Azure AD credentials page customized with organization-specific details as expected?
- Azure AD join issues: Is the device able to [join Azure Active Directory](troubleshoot-aad-join.md)?
- MDM enrollment issues: IS the device able to [enroll in Microsoft Intune](troubleshoot-device-enrollment.md) (or an equivalent MDM service)?
- Review logs that are automatically collected upon Autopilot failure. For more information, see [Collect diagnostics from a Windows device](../intune/remote-actions/collect-diagnostics.md). <!--1895390-->

## Next steps

See the following topics for help with troubleshooting specific issues:

- [Troubleshoot device enrollment](troubleshoot-device-enrollment.md)
- [Troubleshoot OOBE issues](troubleshoot-oobe.md)
- [Troubleshoot AAD join issues](troubleshoot-aad-join.md)
- [Policy conflicts](policy-conflicts.md)
- [Collect diagnostics from a Windows device](../intune/remote-actions/collect-diagnostics.md)
- [Known issues](known-issues.md)

## Related topics

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)
