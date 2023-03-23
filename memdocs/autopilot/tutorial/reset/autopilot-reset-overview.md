---
title: Overview for Windows Autopilot Reset in Intune
description: Overview for Windows Autopilot Reset in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/14/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Step by step tutorial for Windows Autopilot Reset in Intune

*Applies to:*

- Windows 11
- Windows 10

Windows Autopilot Reset takes the device back to a business-ready state, allowing the next user to sign in and get productive quickly and simply. In addition, Windows Autopilot Reset will also block the user from accessing the desktop until information is restored, including reapplying any provisioning packages. Windows Autopilot Reset will also block the user from accessing the desktop until an Intune sync is completed.

> [!IMPORTANT]
> Windows Autopilot Reset only supports Azure AD join devices. Windows Autopilot Reset doesn't support hybrid Azure AD join devices. For hybrid Azure AD join devices, a full device wipe is required. When a hybrid Azure AD device goes through a full device reset, it may take up to 24 hours for it to be ready to be deployed again. You can expedite this request by re-registering the device.

## What does Windows Autopilot Reset do and what information is removed?

Specifically, Windows Autopilot Reset performs the following actions and removes the following information:

- The device's primary user will be removed. The next user who signs in after the reset will be set as the primary user.
- Removes personal files, apps, and settings.
- Reapplies a device's original settings.
- Sets the region, language, and keyboard to the original values.
- Maintains the device's identity connection to Azure AD.
- Maintains the device's management connection to Intune.

## What information is kept after an Windows Autopilot Reset?

The Windows Autopilot Reset process automatically keeps information from the existing device:

- Wi-Fi connection details.
- Provisioning packages previously applied to the device.
- A provisioning package present on a USB drive when the reset process is started.
- Azure Active Directory device membership and Intune enrollment information.
- SCEP certificates.

## Windows Autopilot Reset requirements

- Azure AD join devices only. Hybrid Azure AD join devices are not supported.
- [Windows Recovery Environment (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) is correctly configured and enabled on the device.
- User initiating local Windows Autopilot Reset must be a local administrator on the device.

## Windows Autopilot Rest Scenarios

Windows Autopilot Reset supports two scenarios:

- [Local reset](local-autopilot-reset.md) - an Windows Autopilot Reset that is started locally on the device by the user.
- [Remote reset](remote-autopilot-reset.md) started remotely by IT personnel via an MDM service such as Microsoft Intune.

Additional requirements and configuration details apply with each scenario.



### Enable local Windows Autopilot Reset







## Troubleshooting

Windows Autopilot Reset requires that the [Windows Recovery Environment (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) is correctly configured and enabled on the device. If it isn't configured and enabled, an error such as `Error code: ERROR_NOT_SUPPORTED (0x80070032)` will be reported.

To make sure WinRE is enabled, use the [REAgentC.exe tool](/windows-hardware/manufacture/desktop/reagentc-command-line-options) to run the following command:

```cmd
reagentc.exe /enable
```

If Windows Autopilot Reset fails after enabling WinRE, or if you're unable to enable WinRE, contact [Microsoft Support](https://support.microsoft.com) for assistance.