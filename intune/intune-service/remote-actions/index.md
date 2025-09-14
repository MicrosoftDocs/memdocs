---
title: Remote Device Actions In Microsoft Intune
description: Use Microsoft Intune to run remote actions on Android, iOS/iPadOS, macOS, and Windows devices. You can reset the password, lock the device, wipe or reset the OS, scan for viruses, and more. Use this feature to remotely manage devices and have help desk run common tasks.
ms.date: 08/27/2025
ms.topic: overview

ms.reviewer: ankitanangia
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Remote device actions in Intune

In today's hybrid work environment, IT professionals are expected to manage and secure devices across diverse locations and platforms—often without physical access. Microsoft Intune's remote device actions provide a powerful toolkit to meet this challenge. These actions enable IT pros to respond quickly to incidents, enforce compliance, and maintain productivity, all from the cloud. Whether it's locking a lost device, resetting a password, or triggering a malware scan, remote actions help ensure that users stay protected and supported—wherever they are.

## When remote actions are useful

Remote actions are especially valuable in scenarios where time and access are limited. For example:

- A device is reported lost or stolen—IT can remotely wipe or lock it to protect sensitive data.
- A device is malfunctioning—IT can restart it or run diagnostics without needing to be on-site.
- A device hasn't checked in for a while—IT can trigger a sync to apply the latest policies.
- A malware alert is raised—security teams can initiate a Defender Antivirus scan remotely.

These capabilities reduce downtime, improve security posture, and streamline support operations.

## Prerequisites

Each remote action has its own prerequisites, which are detailed in the respective documentation. In general:

- Devices must be enrolled in Intune.
- Devices must be connected to the Internet to receive remote commands.
- Some actions might require specific Intune roles or permissions.

## Available remote actions

Microsoft Intune supports remote device actions across multiple platforms. The availability of specific actions depends on the platform and the device's configuration. This cross-platform support ensures that IT pros can manage a diverse device ecosystem with consistent tools and workflows.

Select one of the following tabs to learn more about the available remote actions for each platform:

# [:::image type="icon" source="../media/icons/platforms/windows.svg"::: **Windows**](#tab/windows)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="../media/icons/remote-actions/autopilot-reset.svg" border="false"::: | [Autopilot reset][RA-APRESET] | Restores a device to its original settings and removes personal files, apps, and settings. |
| :::image type="icon" source="../media/icons/remote-actions/bitlocker-key-rotation.svg" border="false"::: | [BitLocker key rotation][RA-BL] | Rotates the BitLocker recovery key for a device. |
| :::image type="icon" source="../media/icons/remote-actions/collect-diagnostics.svg" border="false"::: | [Collect diagnostics][RA-DIAG] | Collects diagnostic logs from a device and uploads the logs to Intune. |
| :::image type="icon" source="../media/icons/remote-actions/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, any company data is removed, and the device is retired. |
| :::image type="icon" source="../media/icons/remote-actions/fresh-start.svg" border="false"::: | [Fresh Start][RA-FRESHSTART] | Reinstalls the latest version of Windows on a device and removes apps that the manufacturer installed. |
| :::image type="icon" source="../media/icons/remote-actions/full-scan.svg" border="false"::: | [Full Scan][RA-SCANF] | Initiates a full scan of the device by Microsoft Defender Antivirus. |
| :::image type="icon" source="../media/icons/remote-actions/locate-device.svg" border="false"::: | [Locate device][RA-LOCATE] | Shows the approximate location of a device on a map. |
| :::image type="icon" source="../media/icons/remote-actions/pause-config-refresh.svg" border="false"::: | [Pause Config Refresh][RA-PAUSECR] | Pause ConfigRefresh to run remediation on a device for troubleshooting or maintenance or to make changes. |
| :::image type="icon" source="../media/icons/remote-actions/quick-scan.svg" border="false"::: | [Quick Scan][RA-SCANQ] | Initiates a quick scan of the device by Microsoft Defender Antivirus. |
| :::image type="icon" source="../media/icons/remote-actions/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="../media/icons/remote-actions/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="../media/icons/remote-actions/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="../media/icons/remote-actions/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="../media/icons/remote-actions/rotate-local-admin-password.svg" border="false"::: | [Rotate Local admin password][RA-ROTLAP] | Changes the local administrator password for a device and stores the password in Intune. |
| :::image type="icon" source="../media/icons/remote-actions/run-remediation.svg" border="false"::: | [Run remediation][RA-REMED] | Initiates on demand Proactive Remediation |
| :::image type="icon" source="../media/icons/remote-actions/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="../media/icons/remote-actions/update-windows-defender-security-intelligence.svg" border="false"::: | [Update Windows Defender security intelligence][RA-DEFAV] | Updates the security intelligence files for Microsoft Defender Antivirus. |
| :::image type="icon" source="../media/icons/remote-actions/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | This action restores a device to its factory settings and removes all data and settings. |

> [!TIP]
> For Intel vPro devices, Intune also integrates with Intel vPro Fleet Services to provide hardware-level remote management capabilities, including out-of-band management that works even when the operating system is unresponsive or the device is powered off.

# [:::image type="icon" source="../media/icons/platforms/ios-ipados.svg"::: **iOS/iPadOS**](#tab/ios-ipados)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="../media/icons/remote-actions/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, any company data is removed, and the device is retired. |
| :::image type="icon" source="../media/icons/remote-actions/disable-activation-lock.svg" border="false"::: | [Disable Activation Lock][RA-ACTLOCK] | Removes the Activation Lock from a device that is enrolled with a device enrollment manager (DEM) account. |
| :::image type="icon" source="../media/icons/remote-actions/locate-device.svg" border="false"::: | [Locate device][RA-LOCATE] | Shows the approximate location of a device on a map. |
| :::image type="icon" source="../media/icons/remote-actions/logout-current-user.svg" border="false"::: | [Logout current user][RA-LOGOUT] | Signs out the current user from a Shared iPad. |
| :::image type="icon" source="../media/icons/remote-actions/lost-mode.svg" border="false"::: | [Lost mode][RA-LOSTMODE] | Locks a device with a custom message and disables sound and vibration. |
| :::image type="icon" source="../media/icons/remote-actions/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="../media/icons/remote-actions/play-lost-mode-sound.svg" border="false"::: | [Play Lost Mode sound][RA-PLAY] | Plays Lost Mode sound on a lost device to help locate it. |
| :::image type="icon" source="../media/icons/remote-actions/remote-lock.svg" border="false"::: | [Remote lock][RA-LOCK] | Locks a device and resets its password. |
| :::image type="icon" source="../media/icons/remote-actions/remove-apps-and-configuration.svg" border="false"::: | [Remove apps and configuration][RA-APPCON] | Temporarily remove applications and configuration from a device.|
| :::image type="icon" source="../media/icons/remote-actions/remove-user.svg" border="false"::: | [Remove user][RA-REMOVEUSER] | Deletes a user from the cache of a Shared iPad. |
| :::image type="icon" source="../media/icons/remote-actions/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="../media/icons/remote-actions/reset-passcode.svg" border="false"::: | [Remove passcode][RA-PREM] | Removes the device passcode. |
| :::image type="icon" source="../media/icons/remote-actions/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="../media/icons/remote-actions/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="../media/icons/remote-actions/send-custom-notification.svg" border="false"::: | [Send custom notification][RA-NOTIFY] | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| :::image type="icon" source="../media/icons/remote-actions/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="../media/icons/remote-actions/update-cellular-data-plan.svg" border="false"::: | [Update cellular data plan][RA-CELLULAR] | Updates the cellular data plan settings for a device that uses an eSIM profile. |
| :::image type="icon" source="../media/icons/remote-actions/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | This action restores a device to its factory settings and removes all data and settings. |

# [:::image type="icon" source="../media/icons/platforms/macos.svg"::: **macOS**](#tab/macos)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="../media/icons/remote-actions/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, any company data is removed, and the device is retired. |
| :::image type="icon" source="../media/icons/remote-actions/disable-activation-lock.svg" border="false"::: | [Disable Activation Lock][RA-ACTLOCK] | Removes the Activation Lock from a device that is enrolled with a device enrollment manager (DEM) account. |
| :::image type="icon" source="../media/icons/remote-actions/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="../media/icons/remote-actions/remote-lock.svg" border="false"::: | [Remote lock][RA-LOCK] | Locks a device and resets its password. |
| :::image type="icon" source="../media/icons/remote-actions/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="../media/icons/remote-actions/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="../media/icons/remote-actions/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="../media/icons/remote-actions/rotate-filevault-recovery.svg" border="false"::: | [Rotate FileVault recovery key][RA-FV] | Rotates the FileVault recovery key for a device. |
| :::image type="icon" source="../media/icons/remote-actions/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="../media/icons/remote-actions/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | This action restores a device to its factory settings and removes all data and settings. |

# [:::image type="icon" source="../media/icons/platforms/android.svg"::: **Android**](#tab/android)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="../media/icons/remote-actions/delete.svg" border="false"::: | [Delete][RA-DELETE] | Removes a device from Intune management, any company data is removed, and the device is retired. |
| :::image type="icon" source="../media/icons/remote-actions/locate-device.svg" border="false"::: | [Locate device][RA-LOCATE] | Shows the approximate location of a device on a map. |
| :::image type="icon" source="../media/icons/remote-actions/new-remote-assistance-session.svg" border="false"::: | [New remote assistance session][RA-ASSIST]| Allows you to remotely control a device using [Remote Help][RA-HELP] or [TeamViewer][RA-TVIEW]. |
| :::image type="icon" source="../media/icons/remote-actions/play-lost-mode-sound.svg" border="false"::: | [Play lost device sound][RA-PLAY] | Plays a sound on a lost device to help locate it. |
| :::image type="icon" source="../media/icons/remote-actions/remote-lock.svg" border="false"::: | [Remote lock][RA-LOCK] | Locks a device and resets its password. |
| :::image type="icon" source="../media/icons/remote-actions/remove-apps-and-configuration.svg" border="false"::: | [Remove apps and configuration][RA-APPCON] | Temporarily remove applications and configuration from a device.|
| :::image type="icon" source="../media/icons/remote-actions/rename-device.svg" border="false"::: | [Rename device][RA-REN] | Changes the device name in Intune. |
| :::image type="icon" source="../media/icons/remote-actions/reset-passcode.svg" border="false"::: | [Reset passcode][RA-PREST] | Resets the device passcode. |
| :::image type="icon" source="../media/icons/remote-actions/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="../media/icons/remote-actions/retire.svg" border="false"::: | [Retire][RA-RETIRE] | Removes company data and settings from a device, and leaves personal data intact. |
| :::image type="icon" source="../media/icons/remote-actions/send-custom-notification.svg" border="false"::: | [Send custom notification][RA-NOTIFY] | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| :::image type="icon" source="../media/icons/remote-actions/sync.svg" border="false"::: | [Sync][RA-SYNC] | Syncs a device with Intune to apply the latest policies and configurations. |
| :::image type="icon" source="../media/icons/remote-actions/wipe.svg" border="false"::: | [Wipe][RA-WIPE] | This action restores a device to its factory settings and removes all data and settings. |

# [:::image type="icon" source="../media/icons/platforms/chromeos.svg"::: **ChromeOS**](#tab/chromeos)

> [!NOTE]
> To manage ChromeOS devices with Intune, you must first [set up the Chrome Enterprise connector](../enrollment/chrome-enterprise-connector-configure.md) and enroll devices using the Google Admin console. This integration allows you to manage ChromeOS devices alongside other platforms in Intune.

# [:::image type="icon" source="../media/icons/platforms/android.svg"::: **Android**](#tab/android)

| Icon | Action | Description |
|--|--|--|
| :::image type="icon" source="../media/icons/remote-actions/retire.svg" border="false"::: | [Deprovision][RA-DEPR] | . |
| :::image type="icon" source="../media/icons/remote-actions/lost-mode.svg" border="false"::: | [Lost mode][RA-LOSTMODE] | . |
| :::image type="icon" source="../media/icons/remote-actions/restart.svg" border="false"::: | [Restart][RA-RESTART] | Restarts a device. |
| :::image type="icon" source="../media/icons/remote-actions/retire.svg" border="false"::: | [Retire][RA-WIPE] | . |

---

## Execute a remote device action from the Intune admin center

Every remote device action has its own steps, which are detailed in the respective documentation. In general:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, a row displays available remote actions. Each icon represents a specific action (such as **Restart**, **Wipe**, or **Remove user**). Depending on your screen resolution or window size, some actions might be hidden under the overflow menu (**...**).
1. Select the desired action.
1. Complete any required fields, and then confirm the action.

> [!NOTE]
> The **Retire**, **Wipe**, and **Delete** actions take precedence over all other actions. A device with multiple pending actions only carry out a Retire, Wipe, or Delete. All other pending actions are ignored.

## Check the status of the remote action

To check the status of the remote action, select **Devices** > [**Device actions**][INT-AC].

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/DeviceActionList.ReactView


## Next steps

Remote device actions in Intune empower IT pros to manage devices efficiently and securely—whether individually or at scale. Explore the documentation linked in this article to learn more about each action and how to integrate them into your device management workflows.

Some remote actions can also be executed in bulk. To learn more, see [Bulk device actions in Microsoft Intune](bulk-device-actions.md).

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
[RA-SCANF]: device-quick-scan.md
[RA-SCANQ]: device-quick-scan.md
[RA-SYNC]: device-sync.md
[RA-HELP]: ../fundamentals/remote-help.md
[RA-TVIEW]: teamviewer-support.md
[RA-WIPE]: device-wipe.md

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-AC2]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/BulkActionWizardBlade