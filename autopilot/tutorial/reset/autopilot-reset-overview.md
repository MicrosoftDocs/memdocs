---
title: Overview for Windows Autopilot Reset in Intune
description: Overview for Windows Autopilot Reset in Intune.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Step by step tutorial for Windows Autopilot Reset in Intune

Windows Autopilot Reset takes the device back to a business-ready state, allowing the next user to sign in and get productive quickly and simply. In addition, once the Windows Autopilot Reset begins, it blocks the user from accessing the desktop until information is restored, including reapplying any provisioning packages. Windows Autopilot Reset also blocks the new user from accessing the desktop until an Intune sync is completed.

> [!IMPORTANT]
>
> Windows Autopilot Reset only supports Microsoft Entra join devices. Windows Autopilot Reset doesn't support Microsoft Entra hybrid join devices. For Microsoft Entra hybrid join devices, a [full device wipe](/mem/intune/remote-actions/devices-wipe) is required. When a hybrid Microsoft Entra device goes through a full device reset, it might take up to 24 hours for it to be ready to be deployed again. This request can be expedited by re-registering the device. Consider also using the [Windows Autopilot deployment for existing devices](../existing-devices/existing-devices-workflow.md) scenario to wipe the device.

## Information removed and reset by a Windows Autopilot Reset

The Windows Autopilot Reset process removes or resets the following information from the existing device:

- The device's primary user is removed. The next user who signs in after the Windows Autopilot Reset will be set as the primary user.
- Removes personal files, apps, and settings.
- Reapplies a device's original settings.
- Sets the region, language, and keyboard to the original values.

## Information kept and migrated after a Windows Autopilot Reset

The Windows Autopilot Reset process automatically keeps the following information from the existing device:

- Maintains the device's identity connection to Microsoft Entra ID.
- Maintains the device's management connection to Intune.
- Wi-Fi connection details.
- Provisioning packages previously applied to the device.
- A provisioning package present on a USB drive when the reset process is started.
- Microsoft Entra device membership and Intune enrollment information.
- System Center Endpoint Protection (SCEP) certificates.

## Windows Autopilot Reset requirements

- Enrolled in Microsoft Entra ID. Only Microsoft Entra join devices are supported. Microsoft Entra hybrid join devices aren't supported.
- Enrolled in Intune.
- [Windows Recovery Environment (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) is correctly configured and enabled on the device where Windows Autopilot Reset is used.
- User initiating [local Windows Autopilot Reset](local-autopilot-reset.md) must be a local administrator on the device.
- Admins initiating a [remote Windows Autopilot Reset](remote-autopilot-reset.md) must be a member of the Intune Service Administrator role.

## Windows Autopilot Reset Scenarios in Intune

Windows Autopilot Reset in Intune supports two scenarios:

- [Local reset](local-autopilot-reset.md) - a Windows Autopilot Reset started locally on the device by a user.
- [Remote reset](remote-autopilot-reset.md) - a Windows Autopilot Reset started remotely by an Intune admin in Microsoft Intune.

## How Windows Autopilot Reset works

Windows Autopilot Reset works by using the [push-button reset](/windows-hardware/manufacture/desktop/push-button-reset-overview) feature in Windows. The following actions occur during a Windows Autopilot Reset:

- A new OS of the same version is created by reconstructing it from the WinSxS store.
- Migration of data is performed between the old OS and the new OS to preserve the items from [Information kept and migrated after a Windows Autopilot Reset](#information-kept-and-migrated-after-a-windows-autopilot-reset).
- All existing user profiles and data are deleted.
- Non-Microsoft apps are uninstalled.

## Walkthrough

Both local Windows Autopilot Reset and remote Windows Autopilot Reset require a minimal number of steps to implement. Unlike other Autopilot scenarios, instructions with multiple steps aren't needed. Select the desired Windows Autopilot Reset scenario for instructions on how to implement the scenario:

> [!div class="nextstepaction"]
> [Local Windows Autopilot Reset](local-autopilot-reset.md)

> [!div class="nextstepaction"]
> [Remote Windows Autopilot Reset](remote-autopilot-reset.md)

## Related content

For more information on Windows Autopilot Reset, see the following articles:

- [Windows Autopilot self-deploying mode](../../windows-autopilot-reset.md).
- [Push-button reset](/windows-hardware/manufacture/desktop/push-button-reset-overview).
