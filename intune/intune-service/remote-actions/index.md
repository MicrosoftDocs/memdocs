---
title: Remote Device Actions – Wipe, Lock, Locate, and More
description: Discover how to use Microsoft Intune to remotely manage, wipe, lock, restart, and secure Android, iOS/iPadOS, macOS, Windows, and ChromeOS devices. Learn about available remote actions, prerequisites, and bulk actions for IT admins.
ms.date: 09/22/2025
ms.topic: overview
---

# Remote device actions

In today's hybrid work environment, IT professionals manage and secure devices across diverse locations and platforms—often without physical access. Microsoft Intune's remote device actions provide a powerful toolkit to meet this challenge. These actions enable IT pros to respond quickly to incidents, enforce compliance, and maintain productivity, all from the cloud. Whether it's locking a lost device, resetting a password, or triggering a malware scan, remote actions help ensure that users stay protected and supported—wherever they are.

## When remote actions are useful

Remote actions are especially valuable in scenarios where time and access are limited. For example:

- A device is reported lost or stolen—IT can remotely wipe or lock it to protect sensitive data.
- A device is malfunctioning—IT can restart it or run diagnostics without needing to be on-site.
- A device needs to receive a payload immediately—IT can trigger a sync to apply the latest policies.
- A malware alert is raised—security teams can initiate a Defender Antivirus scan remotely.

These capabilities reduce downtime, improve security posture, and streamline support operations.

## Prerequisites

Each remote action has its own prerequisites, which the respective documentation details. In general:

- Devices must be enrolled in Intune.
- Devices must be connected to the Internet to receive remote commands.
- Some actions might require specific Intune roles or permissions.

## Available remote actions

Microsoft Intune supports remote device actions across multiple platforms. The availability of specific actions depends on the platform and the device's configuration. This cross-platform support ensures that IT pros can manage a diverse device ecosystem with consistent tools and workflows.

Select one of the following tabs to learn more about the available remote actions for each platform:

# [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="icons/autopilot-reset.svg" border="false"::: | [Autopilot reset][RA-APRESET] | Restores a device to its original settings and removes personal files, apps, and settings. |
| :::image type="icon" source="icons/bitlocker-key-rotation.svg" border="false"::: | [BitLocker key rotation][RA-BL] | Rotates the BitLocker recovery key for a device. |
| :::image type="icon" source="icons/collect-diagnostics.svg" border="false"::: | [Collect diagnostics][RA-DIAG] | Collects diagnostic logs from a device and uploads the logs to Intune. |
| :::image type="icon" source="icons/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, removes any company data, and retires the device. |
| :::image type="icon" source="icons/fresh-start.svg" border="false"::: | [Fresh Start][RA-FRESHSTART] | Reinstalls the latest version of Windows on a device and removes apps that the manufacturer installed. |
| :::image type="icon" source="icons/full-scan.svg" border="false"::: | [Full Scan][RA-SCANF] | Initiates a full scan of the device by Microsoft Defender Antivirus. |
| :::image type="icon" source="icons/locate-device.svg" border="false"::: | [Locate device][RA-LOCATE] | Shows the approximate location of a device on a map. |
| :::image type="icon" source="icons/pause-config-refresh.svg" border="false"::: | [Pause Config Refresh][RA-PAUSECR] | Pauses ConfigRefresh to run remediation on a device for troubleshooting or maintenance or to make changes. |
| :::image type="icon" source="icons/quick-scan.svg" border="false"::: | [Quick Scan][RA-SCANQ] | Initiates a quick scan of the device by Microsoft Defender Antivirus. |
| :::image type="icon" source="icons/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device by using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="icons/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="icons/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="icons/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="icons/rotate-local-admin-password.svg" border="false"::: | [Rotate Local admin password][RA-ROTLAP] | Changes the local administrator password for a device and stores the password in Intune. |
| :::image type="icon" source="icons/run-remediation.svg" border="false"::: | [Run remediation][RA-REMED] | Initiates on demand Proactive Remediation |
| :::image type="icon" source="icons/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="icons/update-windows-defender-security-intelligence.svg" border="false"::: | [Update Windows Defender security intelligence][RA-DEFAV] | Updates the security intelligence files for Microsoft Defender Antivirus. |
| :::image type="icon" source="icons/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | Restores a device to its factory settings and removes all data and settings. |

> [!TIP]
> For Intel vPro devices, Intune also integrates with Intel vPro Fleet Services to provide hardware-level remote management capabilities, including out-of-band management that works even when the operating system is unresponsive or the device is powered off.

# [:::image type="icon" source="../../media/icons/platforms/ios-ipados.svg"::: **iOS/iPadOS**](#tab/ios-ipados)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="icons/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, removes any company data, and retires the device. |
| :::image type="icon" source="icons/disable-activation-lock.svg" border="false"::: | [Disable Activation Lock][RA-ACTLOCK] | Removes the Activation Lock from a device that's enrolled with a device enrollment manager (DEM) account. |
| :::image type="icon" source="icons/locate-device.svg" border="false"::: | [Locate device][RA-LOCATE] | Shows the approximate location of a device on a map. |
| :::image type="icon" source="icons/logout-current-user.svg" border="false"::: | [Logout current user][RA-LOGOUT] | Signs out the current user from a Shared iPad. |
| :::image type="icon" source="icons/lost-mode.svg" border="false"::: | [Lost mode][RA-LOSTMODE] | Locks a device with a custom message and disables sound and vibration. |
| :::image type="icon" source="icons/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device by using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="icons/play-lost-mode-sound.svg" border="false"::: | [Play Lost Mode sound][RA-PLAY] | Plays Lost Mode sound on a lost device to help locate it. |
| :::image type="icon" source="icons/remote-lock.svg" border="false"::: | [Remote lock][RA-LOCK] | Locks a device and resets its password. |
| :::image type="icon" source="icons/remove-apps-and-configuration.svg" border="false"::: | [Remove apps and configuration][RA-APPCON] | Temporarily removes applications and configuration from a device.|
| :::image type="icon" source="icons/remove-user.svg" border="false"::: | [Remove user][RA-REMOVEUSER] | Deletes a user from the cache of a Shared iPad. |
| :::image type="icon" source="icons/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="icons/reset-passcode.svg" border="false"::: | [Remove passcode][RA-PREM] | Removes the device passcode. |
| :::image type="icon" source="icons/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="icons/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="icons/send-custom-notification.svg" border="false"::: | [Send custom notification][RA-NOTIFY] | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| :::image type="icon" source="icons/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="icons/update-cellular-data-plan.svg" border="false"::: | [Update cellular data plan][RA-CELLULAR] | Updates the cellular data plan settings for a device that uses an eSIM profile. |
| :::image type="icon" source="icons/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | Restores a device to its factory settings and removes all data and settings. |

# [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="icons/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, removes any company data, and retires the device. |
| :::image type="icon" source="icons/disable-activation-lock.svg" border="false"::: | [Disable Activation Lock][RA-ACTLOCK] | Removes the Activation Lock from a device that's enrolled with a device enrollment manager (DEM) account. |
| :::image type="icon" source="icons/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device by using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="icons/remote-lock.svg" border="false"::: | [Remote lock][RA-LOCK] | Locks a device and resets its password. |
| :::image type="icon" source="icons/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="icons/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="icons/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="icons/rotate-filevault-recovery.svg" border="false"::: | [Rotate FileVault recovery key][RA-FV] | Rotates the FileVault recovery key for a device. |
| :::image type="icon" source="icons/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="icons/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | Restores a device to its factory settings and removes all data and settings. |

# [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="icons/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, removes any company data, and retires the device. |
| :::image type="icon" source="icons/locate-device.svg" border="false"::: | [Locate device][RA-LOCATE] | Shows the approximate location of a device on a map. |
| :::image type="icon" source="icons/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device by using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="icons/play-lost-mode-sound.svg" border="false"::: | [Play lost device sound][RA-PLAY] | Plays a sound on a lost device to help locate it. |
| :::image type="icon" source="icons/remote-lock.svg" border="false"::: | [Remote lock][RA-LOCK] | Locks a device and resets its password. |
| :::image type="icon" source="icons/remove-apps-and-configuration.svg" border="false"::: | [Remove apps and configuration][RA-APPCON] | Temporarily removes applications and configuration from a device.|
| :::image type="icon" source="icons/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="icons/reset-passcode.svg" border="false"::: | [Reset passcode][RA-PREST] | Resets the device passcode. |
| :::image type="icon" source="icons/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="icons/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="icons/send-custom-notification.svg" border="false"::: | [Send custom notification][RA-NOTIFY] | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| :::image type="icon" source="icons/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="icons/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | Restores a device to its factory settings and removes all data and settings. |

# [:::image type="icon" source="../../media/icons/platforms/chromeos.svg"::: **ChromeOS**](#tab/chromeos)

> [!NOTE]
> To manage ChromeOS devices with Intune, you must first [set up the Chrome Enterprise connector](../enrollment/chrome-enterprise-connector-configure.md) and enroll devices by using the Google Admin console. This integration allows you to manage ChromeOS devices alongside other platforms in Intune.

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="icons/retire.svg" border="false"::: | [Deprovision][RA-DEPR] | Removes Google Admin policies from a ChromeOS device that you no longer use. |
| :::image type="icon" source="icons/lost-mode.svg" border="false"::: | [Lost mode][RA-LOSTMODE] | Locks a lost or stolen ChromeOS device and displays a custom message and contact info configured in the Google Admin Console. In Chrome Enterprise, this action is referred to as **Disabled**. |
| :::image type="icon" source="icons/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="icons/retire.svg" border="false"::: | [Retire][RA-WIPE] | Erases data from the device. You can choose to remove only user profiles or perform a full factory reset (Powerwash). A factory reset is required before re-enrollment. |

---

## Execute a remote device action from the Intune admin center

Every remote device action has its own steps, which the respective documentation details. In general:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, a row displays available remote actions. Each icon represents a specific action (such as **Restart**, **Wipe**, or **Locate device**). Depending on your screen resolution or window size, the overflow menu (**...**) might hide some actions.
1. Select the desired action.
1. Complete any required fields, then confirm the action.

> [!NOTE]
> The **Retire**, **Wipe**, and **Delete** actions take precedence over all other actions. A device with multiple pending actions only carries out a Retire, Wipe, or Delete. The system ignores all other pending actions.

## Check the status of the remote action

To check the status of the remote action, select **Devices** > [**Device actions**][INT-AC].

## Bulk device actions

Managing devices at scale is a common challenge for IT pros, especially in environments like schools, enterprises, or frontline operations. Microsoft Intune supports bulk remote actions, so IT admins can perform tasks on up to 100 devices at the same time. This capability streamlines operations, reduces manual effort, and ensures consistent policy enforcement across large device fleets.

For example, at the end of a school year, IT admins can use bulk wipe to securely reset student devices before reassigning them for the next term. This approach saves time and ensures that sensitive data is removed efficiently across all devices.

Select one of the following tabs to learn more about the available bulk remote actions for each platform:

# [:::image type="icon" source="../../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

| Bulk action                    | Description                                                                                |
|--------------------------------|--------------------------------------------------------------------------------------------|
| [Autopilot reset][RA-APRESET]  | Restores a device to its original settings and removes personal files, apps, and settings. |
| [Collect diagnostics][RA-DIAG] | Collects diagnostic logs from a device and uploads the logs to Intune.                     |
| [Delete][RA-DELETE]            | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename][RA-REN]               | Changes the device name in Intune.                                                         |
| [Restart][RA-RESTART]          | Restarts a device.                                                                         |
| [Retire][RA-RETIRE]            | Removes company data and settings from a device, and leaves personal data intact.          |
| [Sync][RA-SYNC]                | Syncs a device with Intune to apply the latest policies and configurations.                |
| [Wipe][RA-WIPE]                | Restores a device to the factory settings and removes all data and settings.               |

# [:::image type="icon" source="../../media/icons/platforms/ios-ipados.svg"::: **iOS/iPadOS**](#tab/ios-ipados)

| Bulk action                              | Description                                                                                   |
|------------------------------------------|-----------------------------------------------------------------------------------------------|
| [Delete][RA-DELETE]                      | Removes a device from Intune management, removes any company data, and retires the device.    |
| [Rename][RA-REN]                         | Changes the device name in Intune.                                                            |
| [Restart][RA-RESTART]                    | Restarts a device.                                                                            |
| [Retire][RA-RETIRE]                      | Removes company data and settings from a device, and leaves personal data intact.             |
| [Send custom notification][RA-NOTIFY]    | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| [Sync][RA-SYNC]                          | Syncs a device with Intune to apply the latest policies and configurations.                   |
| [Update cellular data plan][RA-CELLULAR] | Updates the cellular data plan settings for a device that uses an eSIM profile.               |
| [Wipe][RA-WIPE]                          | Restores a device to its factory settings and removes all data and settings.                  |

# [:::image type="icon" source="../../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

| Bulk action             | Description                                                                                |
|-------------------------|--------------------------------------------------------------------------------------------|
| [Delete][RA-DELETE]     | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename device][RA-REN] | Changes the device name in Intune.                                                         |
| [Restart][RA-RESTART]   | Restarts a device.                                                                         |
| [Retire][RA-RETIRE]     | Removes company data and settings from a device, and leaves personal data intact.          |
| [Sync][RA-SYNC]         | Syncs a device with Intune to apply the latest policies and configurations.                |
| [Wipe][RA-WIPE]         | Restores a device to its factory settings and removes all data and settings.               |

# [:::image type="icon" source="../../media/icons/platforms/android.svg"::: **Android**](#tab/android)

| Bulk action           | Description                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------|
| [Delete][RA-DELETE]   | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename][RA-REN]      | Changes the device name in Intune.                                                         |
| [Restart][RA-RESTART] | Restarts a device.                                                                         |
| [Wipe][RA-WIPE]       | Restores a device to its factory settings and removes all data and settings.               |

# [:::image type="icon" source="../../media/icons/platforms/chromeos.svg"::: **ChromeOS**](#tab/chromeos)

| Bulk action              | Description                                                                                                                                                                                     |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Deprovision][RA-DEPR]   | Removes Google Admin policies from a ChromeOS device that you no longer use.                                                                                                                    |
| [Lost mode][RA-LOSTMODE] | Locks a lost or stolen ChromeOS device and displays a custom message and contact info configured in the Google Admin Console. In Chrome Enterprise, this action is referred to as **Disabled**. |
| [Restart][RA-RESTART]    | Restarts a device.                                                                                                                                                                              |
| [Retire][RA-WIPE]        | Erases data from the device. You can choose to remove only user profiles or perform a full factory reset (Powerwash). A factory reset is required before re-enrollment.                         |

---

## Execute a bulk device action

Each bulk remote action has its own steps. The documentation for each action provides detailed instructions. In general, follow these steps:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **All devices** > [**Bulk device actions**][INT-AC2].
1. On the **Basics** page, select an **OS** and **Device action** from the dropdowns. Some device actions have more options or fields to fill in. Select **Next**.
1. On the **Devices** page, select up to the maximum number of devices that the action supports. Select **Next**.
1. On the **Review + create** page, select **Create**.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/DeviceActionList.ReactView


## Next steps

Remote device actions in Intune empower IT pros to manage devices efficiently and securely—whether individually or at scale. Explore the documentation linked in this article to learn more about each action and how to integrate them into your device management workflows.

<!--links-->

[RA-ACTLOCK]: device-activation-lock-disable.md
[RA-APPCON]: remove-apps-config.md
[RA-APRESET]: device-autopilot-reset.md
[RA-ASSIST]: device-remote-assist.md
[RA-BL]: device-rotate-bitlocker-keys.md
[RA-CELLULAR]: update-cellular-data-plan.md
[RA-DEFAV]: /windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus
[RA-DELETE]: device-delete.md
[RA-DEPR]: device-deprovision.md
[RA-DIAG]: collect-diagnostics.md
[RA-FRESHSTART]: device-fresh-start.md
[RA-FV]: device-rotate-filevault.md
[RA-HELP]: ../fundamentals/remote-help.md
[RA-LOCATE]: device-locate.md
[RA-LOCK]: device-remote-lock.md
[RA-LOGOUT]: device-logout-user.md
[RA-LOSTMODE]: device-lost-mode.md
[RA-NOTIFY]: custom-notifications.md
[RA-PAUSECR]: pause-config-refresh.md
[RA-PLAY]: device-play-lost-mode-sound.md
[RA-PREM]: device-remove-passcode.md
[RA-PREST]: device-passcode-reset.md
[RA-REMED]: device-run-remediation.md
[RA-REMOVEUSER]: device-remove-user.md
[RA-REN]: device-rename.md
[RA-RESTART]: device-restart.md
[RA-RETIRE]: device-retire.md
[RA-ROTLAP]: ../protect/windows-laps-policy.md#manually-rotate-passwords
[RA-SCAN]: device-scan-defender.md
[RA-SCANF]: device-full-scan.md
[RA-SCANQ]: device-quick-scan.md
[RA-SYNC]: device-sync.md
[RA-TVIEW]: ../fundamentals/teamviewer-support.md
[RA-WIPE]: device-wipe.md

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/BulkActionWizardBlade
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
