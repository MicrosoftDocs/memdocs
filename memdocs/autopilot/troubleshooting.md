---
title: Windows Autopilot troubleshooting overview
description: Learn how to handle issues as they arise during the Windows Autopilot deployment process.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 02/09/2022
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Troubleshooting overview

**Applies to**

- Windows 11
- Windows 10

Windows Autopilot is designed to simplify all parts of the Windows device lifecycle, but there are always situations where issues may arise. When troubleshooting an issue, it is helpful to understand:

- The Windows Autopilot [process flow](#windows-autopilot-flow)
- How Windows Autopilot [device profiles](#profile-download) are downloaded
- [Key activities](#key-troubleshooting-activities) to perform during troubleshooting

## Windows Autopilot diagnostics page
On Windows 11, you can open the Autopilot diagnostic page to view additional detailed troubleshooting information about the Autopilot provisioning process. The diagnostics page can be enabled by going to the ESP profile and selecting **Yes** to **Turn on log collection and diagnostics page for end users**. Once it is enabled you can select the **View Diagnostics button** or the keyboard shortcut Ctrl+Shift+D to access any diagnostic information. The diagnostics page is currently supported for commercial OOBE, and Autopilot user-driven mode.

## Windows Autopilot flow

Whether you're performing user-driven or self-deploying device deployments, the troubleshooting process is about the same. It's useful to understand the flow for a specific device:

1. A network connection is established. The connection can be a wireless (Wi-fi) or wired (Ethernet) connection.
2. The Windows Autopilot profile is downloaded. When you use a wired connection, or manually establish a wireless connection, the profile downloads from the Autopilot deployment service as soon as the network connection is in place.
3. User authentication occurs. When performing a user-driven deployment, the user will enter their Azure Active Directory credentials, which will be validated.
4. Azure Active Directory join occurs. For user-driven deployments, the device will be joined to Azure AD using the specified user credentials. For self-deploying scenarios, the device will be joined without specifying any user credentials.
5. Automatic MDM enrollment occurs. As part of the Azure AD join process, the device will enroll in the MDM service configured in Azure AD (for example, Microsoft Intune).
6. Settings are applied. If the [enrollment status page](enrollment-status.md) is configured, most settings will be applied while the enrollment status page is displayed. If not configured or available, settings will be applied after the user is signed in.

## Profile download

When an Internet-connected Windows device boots up, it will attempt to connect to the Autopilot service and download an Autopilot profile. Note: It's important that a profile exists at this stage so that a blank profile isn't cached locally on the PC. To remove the currently cached local profile in Windows 10 version 1803 and earlier, it's necessary to re-generalize the OS using **sysprep /generalize /oobe**, reinstall the OS, or re-image the PC. In Windows 10 version 1809 and later, you can retrieve a new profile by rebooting the PC.

When a profile is downloaded depends upon the version of Windows client that is running on the PC. See the following table.

| Windows 10 version | Profile download behavior |
| --- | --- |
| 1709 | The profile is downloaded after the OOBE network connection page. This page isn't displayed when using a wired connection. In this case, the profile is downloaded before the EULA screen. |
| 1803 | The profile is downloaded as soon as possible. If wired, it's downloaded at the start of OOBE. If wireless, it's downloaded after the network connection page. |
| 1809 | The profile is downloaded as soon as possible (same as 1803), and again after each reboot. |

If you need to reboot a computer during OOBE:
- Press Shift-F10 to open a command prompt.
- Enter **shutdown /r /t 0** to restart immediately, or **shutdown /s /t 0** to shut down immediately.

For more information, see [Windows Setup Command-Line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

## Key troubleshooting activities

For troubleshooting, key activities to perform are:

- Review configuration: Has Azure Active Directory and Microsoft Intune (or an equivalent MDM service) been configured as specified in [Windows Autopilot configuration requirements](configuration-requirements.md)?
- Check network connectivity: Can the device access the services described in [Windows Autopilot networking requirements](networking-requirements.md)?
- Autopilot out-of-box experience (OOBE) behavior: Are the [expected OOBE](troubleshoot-oobe.md) screens displayed? Is the Azure AD credentials page customized with organization-specific details as expected?
- Azure AD join issues: Is the device able to [join Azure Active Directory](troubleshoot-aad-join.md)?
- MDM enrollment issues: IS the device able to [enroll in Microsoft Intune](troubleshoot-device-enrollment.md) (or an equivalent MDM service)?

## Next steps

See the following topics for help troubleshooting specific issues:

- [Troubleshoot device enrollment](troubleshoot-device-enrollment.md)
- [Troubleshoot OOBE issues](troubleshoot-oobe.md)
- [Troubleshoot AAD join issues](troubleshoot-aad-join.md)
- [Policy conflicts](policy-conflicts.md)
- [Known issues](known-issues.md)

## Related topics

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)
