---
title: Bulk Device Actions in Microsoft Intune
description: Learn how to use bulk remote device actions in Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
ms.reviewer: jlynn
ms.collection:
- M365-identity-device-management
---

# Bulk device actions

Managing devices at scale is a common challenge for IT pros, especially in environments like schools, enterprises, or frontline operations. Microsoft Intune supports bulk remote actions, so IT admins can perform tasks on up to 100 devices at the same time. This capability streamlines operations, reduces manual effort, and ensures consistent policy enforcement across large device fleets.

For example, at the end of a school year, IT admins can use bulk wipe to securely reset student devices before reassigning them for the next term. This approach saves time and ensures that sensitive data is removed efficiently across all devices.

Select one of the following tabs to learn more about the available bulk remote actions for each platform:

# [:::image type="icon" source="../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

| Bulk action                    | Description                                                                                      |
|--------------------------------|--------------------------------------------------------------------------------------------------|
| [Autopilot reset][RA-APRESET]  | Restores a device to its original settings and removes personal files, apps, and settings.       |
| [Collect diagnostics][RA-DIAG] | Collects diagnostic logs from a device and uploads the logs to Intune.                           |
| [Delete][RA-DELETE]            | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename][RA-REN]               | Changes the device name in Intune.                                                               |
| [Restart][RA-RESTART]          | Restarts a device.                                                                               |
| [Retire][RA-RETIRE]            | Removes company data and settings from a device, and leaves personal data intact.                |
| [Sync][RA-SYNC]                | Syncs a device with Intune to apply the latest policies and configurations.                      |
| [Wipe][RA-WIPE]                | Restores a device to the factory settings and removes all data and settings.         |

# [:::image type="icon" source="../media/icons/platforms/ios-ipados.svg"::: **iOS/iPadOS**](#tab/ios-ipados)

| Bulk action                              | Description                                                                                      |
|------------------------------------------|--------------------------------------------------------------------------------------------------|
| [Delete][RA-DELETE]                      | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename][RA-REN]                         | Changes the device name in Intune.                                                               |
| [Restart][RA-RESTART]                    | Restarts a device.                                                                               |
| [Retire][RA-RETIRE]                      | Removes company data and settings from a device, and leaves personal data intact.                |
| [Send custom notification][RA-NOTIFY]    | Sends a custom notification message to a device that can be viewed in the Company Portal app.    |
| [Sync][RA-SYNC]                          | Syncs a device with Intune to apply the latest policies and configurations.                      |
| [Update cellular data plan][RA-CELLULAR] | Updates the cellular data plan settings for a device that uses an eSIM profile.                  |
| [Wipe][RA-WIPE]                          | Restores a device to its factory settings and removes all data and settings.         |

# [:::image type="icon" source="../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

| Bulk action                              | Description                                                                                      |
|------------------------------------------|--------------------------------------------------------------------------------------------------|
| [Delete][RA-DELETE]                      | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename device][RA-REN]                  | Changes the device name in Intune.                                                               |
| [Restart][RA-RESTART]                    | Restarts a device.                                                                               |
| [Retire][RA-RETIRE]                      | Removes company data and settings from a device, and leaves personal data intact.                |
| [Sync][RA-SYNC]                          | Syncs a device with Intune to apply the latest policies and configurations.                      |
| [Wipe][RA-WIPE]                          | Restores a device to its factory settings and removes all data and settings.         |

# [:::image type="icon" source="../media/icons/platforms/android.svg"::: **Android**](#tab/android)

| Bulk action           | Description                                                                                      |
|-----------------------|--------------------------------------------------------------------------------------------------|
| [Delete][RA-DELETE]   | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename][RA-REN]      | Changes the device name in Intune.                                                               |
| [Restart][RA-RESTART] | Restarts a device.                                                                               |
| [Wipe][RA-WIPE]       | Restores a device to its factory settings and removes all data and settings.         |

# [:::image type="icon" source="../media/icons/platforms/chromeos.svg"::: **ChromeOS**](#tab/chromeos)

| Bulk action              | Description                                                                                                                                                                              |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Deprovision][RA-DEPR]   | Removes Google Admin policies from a ChromeOS device that you no longer use.                                                                                                           |
| [Lost mode][RA-LOSTMODE] | Locks a lost or stolen ChromeOS device and displays a custom message and contact info configured in the Google Admin Console. In Chrome Enterprise, this action is referred to as **Disabled**. |
| [Restart][RA-RESTART]    | Restarts a device.                                                                                                                                                                       |
| [Retire][RA-WIPE]        | Erases data from the device. You can choose to remove only user profiles or perform a full factory reset (Powerwash). A factory reset is required before re-enrollment.                  |

---

## Execute a bulk device action

Every bulk remote action has its own steps, which are detailed in the respective documentation. In general:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices** > [**Bulk device actions**][INT-AC2].
1. On the **Basics** page, select an **OS** and **Device action** from the dropdowns. Some device actions have more options or fields to populate. Select **Next**.
1. On the **Devices** page, select up to the maximum number of devices that the action supports. Select **Next**.
1. On the **Review + create** page, select **Create**.

<!--links-->

[RA-ACTLOCK]: device-activation-lock-disable.md
[RA-APPCON]: remove-apps-config.md
[RA-APRESET]: /windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset
[RA-BL]: device-rotate-bitlocker-keys.md
[RA-CELLULAR]: update-cellular-data-plan.md
[RA-DEFAV]: /windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus
[RA-DELETE]: device-delete.md
[RA-DEPR]: device-deprovision.md
[RA-DIAG]: collect-diagnostics.md
[RA-FRESHSTART]: device-fresh-start.md
[RA-FV]: rotate-filevault-recovery-key.md
[RA-LOCATE]: device-locate.md
[RA-LOCK]: device-remote-lock.md
[RA-LOGOUT]: device-logout-user.md
[RA-LOSTMODE]: device-lost-mode.md
[RA-NOTIFY]: custom-notifications.md
[RA-PAUSECR]: pause-config-refresh.md
[RA-PLAY]: device-play-lost-mode-sound.md
[RA-PREST]: device-passcode-reset.md
[RA-REN]: device-rename.md
[RA-RESTART]: device-restart.md
[RA-REMED]: device-run-remediation.md
[RA-REMOVEUSER]: device-remove-user.md
[RA-RETIRE]: device-retire.md
[RA-ROTLAP]: ../protect/windows-laps-policy.md#manually-rotate-passwords
[RA-SCAN]: device-scan-defender.md
[RA-SYNC]: device-sync.md
[RA-TVIEW]: ../fundamentals/teamviewer-support.md
[RA-WIPE]: device-wipe.md

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/BulkActionWizardBlade
