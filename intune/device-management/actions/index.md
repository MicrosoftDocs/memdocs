---
title: Device Actions - Wipe, Lock, Locate, and More
description: Discover how to use Microsoft Intune to remotely manage, wipe, lock, restart, and secure Android, iOS/iPadOS, tvOS, visionOS, macOS, Windows, and ChromeOS devices. Learn about available device actions, prerequisites, and bulk actions for IT admins.
ms.date: 04/30/2026
ms.topic: overview
---

# Device actions

In today's hybrid work environment, IT professionals manage and secure devices across diverse locations and platforms—often without physical access. Microsoft Intune's device actions provide a powerful toolkit to meet this challenge. These actions enable IT pros to respond quickly to incidents, enforce compliance, and maintain productivity, all from the cloud. Whether it's locking a lost device, resetting a password, or triggering a malware scan, device actions help ensure that users stay protected and supported—wherever they are.

## When device actions are useful

Device actions are especially valuable in scenarios where time and access are limited. For example:

- A device is reported lost or stolen—IT can remotely wipe or lock it to protect sensitive data.
- A device is malfunctioning—IT can restart it or run diagnostics without needing to be on-site.
- A device needs to receive a payload immediately—IT can trigger a sync to apply the latest policies.
- A malware alert is raised—security teams can initiate a Defender Antivirus scan remotely.

These capabilities reduce downtime, improve security posture, and streamline support operations.

## Prerequisites

Each action has its own prerequisites, which the respective documentation details. In general:

- Devices must be enrolled in Intune.
- Devices must be connected to the Internet to receive remote commands.
- Some actions might require specific Intune roles or permissions.

## Available device actions

Microsoft Intune supports device actions across multiple platforms. The availability of specific actions depends on the platform and the device's configuration. This cross-platform support ensures that IT pros can manage a diverse device ecosystem with consistent tools and workflows.

Select one of the following tabs to learn more about the available device actions for each platform:

### [:::image type="icon" source="../../media/icons/16/windows.svg"::: **Windows**](#tab/windows)

| Icon                                          | Action                                          | Description                                                                                                |
|:---------------------------------------------:|-------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| ![autopilot-reset-icon]                       | [Autopilot reset]                               | Restores a device to its original settings and removes personal files, apps, and settings.                 |
| ![bitlocker-key-rotation-icon]                | [BitLocker key rotation]                        | Rotates the BitLocker recovery key for a device.                                                           |
| ![collect-diagnostics-icon]                   | [Collect diagnostics]                           | Collects diagnostic logs from a device and uploads the logs to Intune.                                     |
| ![delete-icon]                                | [Delete]                                        | Removes a device from Intune management, removes any company data, and retires the device.                 |
| ![fresh-start-icon]                           | [Fresh Start]                                   | Reinstalls the latest version of Windows on a device and removes apps that the manufacturer installed.     |
| ![full-scan-icon]                             | [Full Scan]                                     | Initiates a full scan of the device by Microsoft Defender Antivirus.                                       |
| ![locate-device-icon]                         | [Locate device]                                 | Shows the approximate location of a device on a map.                                                       |
| ![pause-config-refresh-icon]                  | [Pause Config Refresh]                          | Pauses ConfigRefresh to run remediation on a device for troubleshooting or maintenance or to make changes. |
| ![quick-scan-icon]                            | [Quick Scan]                                    | Initiates a quick scan of the device by Microsoft Defender Antivirus.                                      |
| ![new-remote-assistance-session-icon]         | [New remote assistance session]                 | Allows you to remotely control a device by using [Remote Help] or [TeamViewer].                            |
| ![rename-device-icon]                         | [Rename device]                                 | Changes the device name in Intune.                                                                         |
| ![restart-icon]                               | [Restart]                                       | Restarts a device.                                                                                         |
| ![retire-icon]                                | [Retire]                                        | Removes company data and settings from a device, and leaves personal data intact.                          |
| ![rotate-local-admin-password-icon]           | [Rotate Local admin password]                   | Changes the local administrator password for a device and stores the password in Intune.                   |
| ![run-remediation-icon]                       | [Run remediation]                               | Initiates on demand Proactive Remediation                                                                  |
| ![sync-icon]                                  | [Sync]                                          | Syncs a device with Intune to apply the latest policies and configurations.                                |
| ![update-defender-security-intelligence-icon] | [Update Windows Defender security intelligence] | Updates the security intelligence files for Microsoft Defender Antivirus.                                  |
| ![wipe-icon]                                  | [Wipe]                                          | Restores a device to its factory settings and removes all data and settings.                               |

> [!TIP]
> For Intel vPro devices, Intune also integrates with Intel vPro Fleet Services to provide hardware-level remote management capabilities, including out-of-band management that works even when the operating system is unresponsive or the device is powered off.

### [:::image type="icon" source="../../media/icons/16/apple-mobile.svg"::: **Apple mobile**](#tab/apple-mobile)

| Icon                                   | Action                           | Description                                                                                               | iOS          | iPadOS       | tvOS         | visionOS     |
|:--------------------------------------:|----------------------------------|-----------------------------------------------------------------------------------------------------------|:------------:|:------------:|:------------:|:------------:|
| ![delete-icon]                         | [Delete]                         | Removes a device from Intune management, removes any company data, and retires the device.                | ![Supported] | ![Supported] | ![Supported] | ![Supported] |
| ![disable-activation-lock-icon]        | [Disable Activation Lock]        | Removes the Activation Lock from a device that's enrolled with a device enrollment manager (DEM) account. | ![Supported] | ![Supported] |              |              |
| ![locate-device-icon]                  | [Locate device]                  | Shows the approximate location of a device on a map.                                                      | ![Supported] | ![Supported] |              |              |
| ![logout-current-user-icon]            | [Logout current user]            | Signs out the current user from a Shared iPad.                                                            |              | ![Supported] |              |              |
| ![lost-mode-icon]                      | [Lost mode]                      | Locks a device with a custom message and disables sound and vibration.                                    | ![Supported] | ![Supported] |              |              |
| ![new-remote-assistance-session-icon]  | [New remote assistance session]  | Allows you to remotely control a device by using [Remote Help] or [TeamViewer].                           | ![Supported] | ![Supported] |              |              |
| ![play-lost-mode-sound-icon]           | [Play Lost Mode sound]           | Plays Lost Mode sound on a lost device to help locate it.                                                 | ![Supported] | ![Supported] |              |              |
| ![remote-lock-icon]                    | [Remote lock]                    | Locks a device and resets its password.                                                                   | ![Supported] | ![Supported] |              | ![Supported] |
| ![remove-apps-and-configurations-icon] | [Remove apps and configurations] | Temporarily removes applications and configuration from a device.                                         | ![Supported] | ![Supported] |              |              |
| ![remove-user-icon]                    | [Remove user]                    | Deletes a user from the cache of a Shared iPad.                                                           |              | ![Supported] |              |              |
| ![rename-device-icon]                  | [Rename device]                  | Changes the device name in Intune.                                                                        | ![Supported] | ![Supported] | ![Supported] |              |
| ![remove-passcode-icon]                | [Remove passcode]                | Removes the device passcode.                                                                              | ![Supported] | ![Supported] |              | ![Supported] |
| ![restart-icon]                        | [Restart]                        | Restarts a device.                                                                                        | ![Supported] | ![Supported] | ![Supported] |              |
| ![retire-icon]                         | [Retire]                         | Removes company data and settings from a device, and leaves personal data intact.                         | ![Supported] | ![Supported] | ![Supported] | ![Supported] |
| ![send-custom-notification-icon]       | [Send custom notification]       | Sends a custom notification message to a device that can be viewed in the Company Portal app.             | ![Supported] | ![Supported] |              |              |
| ![shut-down-icon]                      | [Shut down]                      | Shuts down a device.                                                                                      | ![Supported] | ![Supported] |              |              |
| ![sync-icon]                           | [Sync]                           | Syncs a device with Intune to apply the latest policies and configurations.                               | ![Supported] | ![Supported] | ![Supported] | ![Supported] |
| ![update-cellular-data-plan-icon]      | [Update cellular data plan]      | Updates the cellular data plan settings for a device that uses an eSIM profile.                           | ![Supported] | ![Supported] |              |              |
| ![wipe-icon]                           | [Wipe]                           | Restores a device to its factory settings and removes all data and settings.                              | ![Supported] | ![Supported] | ![Supported] | ![Supported] |

### [:::image type="icon" source="../../media/icons/16/macos.svg"::: **macOS**](#tab/macos)

| Icon                                  | Action                          | Description                                                                                               |
|:-------------------------------------:|---------------------------------|-----------------------------------------------------------------------------------------------------------|
| ![delete-icon]                        | [Delete]                        | Removes a device from Intune management, removes any company data, and retires the device.                |
| ![disable-activation-lock-icon]       | [Disable Activation Lock]       | Removes the Activation Lock from a device that's enrolled with a device enrollment manager (DEM) account. |
| ![new-remote-assistance-session-icon] | [New remote assistance session] | Allows you to remotely control a device by using [Remote Help] or [TeamViewer].                           |
| ![remote-lock-icon]                   | [Remote lock]                   | Locks a device and resets its password.                                                                   |
| ![rename-device-icon]                 | [Rename device]                 | Changes the device name in Intune.                                                                        |
| ![restart-icon]                       | [Restart]                       | Restarts a device.                                                                                        |
| ![retire-icon]                        | [Retire]                        | Removes company data and settings from a device, and leaves personal data intact.                         |
| ![rotate-filevault-recovery-icon]     | [Rotate FileVault recovery key] | Rotates the FileVault recovery key.                                                                       |
| ![rotate-recovery-lock-icon]          | [Rotate Recovery Lock passcode] | Rotates the Recovery Lock passcode.                                                                       |
| ![sync-icon]                          | [Sync]                          | Syncs a device with Intune to apply the latest policies and configurations.                               |
| ![wipe-icon]                          | [Wipe]                          | Restores a device to its factory settings and removes all data and settings.                              |

### [:::image type="icon" source="../../media/icons/16/android.svg"::: **Android**](#tab/android)

| Icon                                   | Action                           | Description                                                                                   |
|:--------------------------------------:|----------------------------------|-----------------------------------------------------------------------------------------------|
| ![delete-icon]                         | [Delete]                         | Removes a device from Intune management, removes any company data, and retires the device.    |
| ![locate-device-icon]                  | [Locate device]                  | Shows the approximate location of a device on a map.                                          |
| ![new-remote-assistance-session-icon]  | [New remote assistance session]  | Allows you to remotely control a device by using [Remote Help] or [TeamViewer].               |
| ![play-lost-mode-sound-icon]           | [Play lost device sound]         | Plays a sound on a lost device to help locate it.                                             |
| ![remote-lock-icon]                    | [Remote lock]                    | Locks a device and resets its password.                                                       |
| ![remove-apps-and-configurations-icon] | [Remove apps and configurations] | Temporarily removes applications and configuration from a device.                             |
| ![rename-device-icon]                  | [Rename device]                  | Changes the device name in Intune.                                                            |
| ![reset-passcode-icon]                 | [Reset passcode]                 | Resets the device passcode.                                                                   |
| ![restart-icon]                        | [Restart]                        | Restarts a device.                                                                            |
| ![restore-managed-home-screen-icon]    | [Restore managed home screen]    | Restores the managed home screen on a device.                                                 |
| ![retire-icon]                         | [Retire]                         | Removes company data and settings from a device, and leaves personal data intact.             |
| ![send-custom-notification-icon]       | [Send custom notification]       | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| ![suspend-managed-home-screen-icon]    | [Suspend managed home screen]    | Suspends the managed home screen on a device.                                                 |
| ![sync-icon]                           | [Sync]                           | Syncs a device with Intune to apply the latest policies and configurations.                   |
| ![wipe-icon]                           | [Wipe]                           | Restores a device to its factory settings and removes all data and settings.                  |



### [:::image type="icon" source="../../media/icons/16/chromeos.svg"::: **ChromeOS**](#tab/chromeos)

> [!NOTE]
> To manage ChromeOS devices with Intune, you must first [set up the Chrome Enterprise connector](../../device-enrollment/configure-chrome-enterprise-connector.md) and enroll devices by using the Google Admin console. This integration allows you to manage ChromeOS devices alongside other platforms in Intune.

| Icon              | Action        | Description                                                                                                                                                                                     |
|:-----------------:|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![retire-icon]    | [Deprovision] | Removes Google Admin policies from a ChromeOS device that you no longer use.                                                                                                                    |
| ![lost-mode-icon] | [Lost mode]   | Locks a lost or stolen ChromeOS device and displays a custom message and contact info configured in the Google Admin Console. In Chrome Enterprise, this action is referred to as **Disabled**. |
| ![restart-icon]   | [Restart]     | Restarts a device.                                                                                                                                                                              |
| ![wipe-icon]      | [Wipe]        | Erases data from the device. You can choose to remove only user profiles or perform a full factory reset (Powerwash). A factory reset is required before re-enrollment.                         |

---

## Execute a device action from the Intune admin center

Every device action has its own steps, which the respective documentation details. In general:

1. In the [Microsoft Intune admin center], select **Devices** > [**All devices**].
1. From the devices list, select a device.
1. At the top of the device overview pane, a row displays available device actions. Each icon represents a specific action (such as **Restart**, **Wipe**, or **Locate device**). Depending on your screen resolution or window size, the overflow menu (**...**) might hide some actions.
1. Select the desired action.
1. Complete any required fields, then confirm the action.

> [!NOTE]
> The **Retire**, **Wipe**, and **Delete** actions take precedence over all other actions. A device with multiple pending actions only carries out a Retire, Wipe, or Delete. The system ignores all other pending actions.

## Check the status of the action

To check the status of the action, select **Devices** > [**Device actions**].

## Bulk device actions

Managing devices at scale is a common challenge for IT pros, especially in environments like schools, enterprises, or frontline operations. Microsoft Intune supports bulk device actions, so IT admins can perform tasks on up to 100 devices at the same time. This capability streamlines operations, reduces manual effort, and ensures consistent policy enforcement across large device fleets.

For example, at the end of a school year, IT admins can use bulk wipe to securely reset student devices before reassigning them for the next term. This approach saves time and ensures that sensitive data is removed efficiently across all devices.

Select one of the following tabs to learn more about the available bulk device actions for each platform:

### [:::image type="icon" source="../../media/icons/16/windows.svg"::: **Windows**](#tab/windows)

| Bulk action           | Description                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------|
| [Autopilot reset]     | Restores a device to its original settings and removes personal files, apps, and settings. |
| [Collect diagnostics] | Collects diagnostic logs from a device and uploads the logs to Intune.                     |
| [Delete]              | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename]              | Changes the device name in Intune.                                                         |
| [Restart]             | Restarts a device.                                                                         |
| [Retire]              | Removes company data and settings from a device, and leaves personal data intact.          |
| [Sync]                | Syncs a device with Intune to apply the latest policies and configurations.                |
| [Wipe]                | Restores a device to the factory settings and removes all data and settings.               |

### [:::image type="icon" source="../../media/icons/16/apple-mobile.svg"::: **Apple mobile**](#tab/apple-mobile)

| Bulk action                 | Description                                                                                   |
|-----------------------------|-----------------------------------------------------------------------------------------------|
| [Delete]                    | Removes a device from Intune management, removes any company data, and retires the device.    |
| [Rename]                    | Changes the device name in Intune.                                                            |
| [Restart]                   | Restarts a device.                                                                            |
| [Retire]                    | Removes company data and settings from a device, and leaves personal data intact.             |
| [Send custom notification]  | Sends a custom notification message to a device that can be viewed in the Company Portal app. |
| [Sync]                      | Syncs a device with Intune to apply the latest policies and configurations.                   |
| [Update cellular data plan] | Updates the cellular data plan settings for a device that uses an eSIM profile.               |
| [Wipe]                      | Restores a device to its factory settings and removes all data and settings.                  |

### [:::image type="icon" source="../../media/icons/16/macos.svg"::: **macOS**](#tab/macos)

| Bulk action     | Description                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| [Delete]        | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename device] | Changes the device name in Intune.                                                         |
| [Restart]       | Restarts a device.                                                                         |
| [Retire]        | Removes company data and settings from a device, and leaves personal data intact.          |
| [Sync]          | Syncs a device with Intune to apply the latest policies and configurations.                |
| [Wipe]          | Restores a device to its factory settings and removes all data and settings.               |

### [:::image type="icon" source="../../media/icons/16/android.svg"::: **Android**](#tab/android)

| Bulk action | Description                                                                                |
|-------------|--------------------------------------------------------------------------------------------|
| [Delete]    | Removes a device from Intune management, removes any company data, and retires the device. |
| [Rename]    | Changes the device name in Intune.                                                         |
| [Restart]   | Restarts a device.                                                                         |
| [Wipe]      | Restores a device to its factory settings and removes all data and settings.               |

### [:::image type="icon" source="../../media/icons/16/chromeos.svg"::: **ChromeOS**](#tab/chromeos)

| Bulk action   | Description                                                                                                                                                                                     |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Deprovision] | Removes Google Admin policies from a ChromeOS device that you no longer use.                                                                                                                    |
| [Lost mode]   | Locks a lost or stolen ChromeOS device and displays a custom message and contact info configured in the Google Admin Console. In Chrome Enterprise, this action is referred to as **Disabled**. |
| [Restart]     | Restarts a device.                                                                                                                                                                              |
| [Wipe]        | Erases data from the device. You can choose to remove only user profiles or perform a full factory reset (Powerwash). A factory reset is required before re-enrollment.                         |

---

## Execute a bulk device action

Each bulk action has its own steps. The documentation for each action provides detailed instructions. In general, follow these steps:

1. In the [Microsoft Intune admin center], select [**Devices**] > [**All devices**] > [**Bulk device actions**].
1. On the **Basics** page, select an **OS** and **Device action** from the dropdowns. Some device actions have more options or fields to fill in. Select **Next**.
1. On the **Devices** page, select up to the maximum number of devices that the action supports. Select **Next**.
1. On the **Review + create** page, select **Create**.

## Next steps

Device actions in Intune empower IT pros to manage devices efficiently and securely—whether individually or at scale. Explore the documentation linked in this article to learn more about each action and how to integrate them into your device management workflows.

<!--actions links-->

[Autopilot reset]: autopilot-reset.md
[BitLocker key rotation]: rotate-bitlocker-keys.md
[Collect diagnostics]: collect-diagnostics.md
[Delete]: /entra/identity/authentication/concept-authentication-passwordless
[Delete]: delete.md
[Deprovision]: deprovision.md
[Disable Activation Lock]: disable-activation-lock.md
[Disable Activation Lock]: disable-activation-lock.md
[Fresh Start]: fresh-start.md
[Full Scan]: full-scan.md
[Locate device]: locate.md
[Logout current user]: logout-user.md
[Lost mode]: lost-mode.md
[New remote assistance session]: remote-assist.md
[Pause Config Refresh]: pause-config-refresh.md
[Play lost device sound]: play-lost-mode-sound.md
[Play Lost Mode sound]: play-lost-mode-sound.md
[Quick Scan]: quick-scan.md
[Remote Help]: ../../remote-help/index.md
[Remote lock]: remote-lock.md
[Remove apps and configurations]: remove-apps-config.md
[Remove passcode]: remove-passcode.md
[Remove user]: remove-user.md
[Rename device]: rename.md
[Rename]: rename.md
[Reset passcode]: reset-passcode.md
[Restart]: restart.md
[Restore managed home screen]: restore-managed-home-screen.md
[Retire]: retire.md
[Rotate FileVault recovery key]: rotate-filevault-recovery-key.md
[Rotate Local admin password]: ../../device-security/laps/deploy-policy.md#manually-rotate-passwords
[Rotate Recovery Lock passcode]: rotate-recovery-lock-passcode.md 
[Run remediation]: run-remediation.md
[Send custom notification]: send-custom-notification.md
[Shut down]: shutdown.md
[Suspend managed home screen]: suspend-managed-home-screen.md
[Sync]: sync.md
[TeamViewer]: ../../device-management/tools/teamviewer-legacy.md
[Update cellular data plan]: update-cellular-data-plan.md
[Update Windows Defender security intelligence]: /windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus
[Wipe]: wipe.md

<!-- portal links -->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[**All devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/allDevices
[**Bulk device actions**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_Devices/BulkActionWizardBlade
[**Device actions**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/#view/Microsoft_Intune_Devices/DeviceActionList.ReactView
[**Devices**]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/overview

<!-- icons -->

[Supported]: ../../media/icons/16/check.svg

[autopilot-reset-icon]: icons/autopilot-reset.svg
[bitlocker-key-rotation-icon]: icons/bitlocker-key-rotation.svg
[collect-diagnostics-icon]: icons/collect-diagnostics.svg
[delete-icon]: icons/delete.svg
[disable-activation-lock-icon]: icons/disable-activation-lock.svg
[fresh-start-icon]: icons/fresh-start.svg
[full-scan-icon]: icons/full-scan.svg
[locate-device-icon]: icons/locate-device.svg
[logout-current-user-icon]: icons/logout-current-user.svg
[lost-mode-icon]: icons/lost-mode.svg
[new-remote-assistance-session-icon]: icons/new-remote-assistance-session.svg
[pause-config-refresh-icon]: icons/pause-config-refresh.svg
[play-lost-mode-sound-icon]: icons/play-lost-mode-sound.svg
[quick-scan-icon]: icons/quick-scan.svg
[remote-lock-icon]: icons/remote-lock.svg
[remove-apps-and-configurations-icon]: icons/remove-apps-and-configurations.svg
[remove-passcode-icon]: icons/remove-passcode.svg
[remove-user-icon]: icons/remove-user.svg
[rename-device-icon]: icons/rename-device.svg
[reset-passcode-icon]: icons/reset-passcode.svg
[restart-icon]: icons/restart.svg
[restore-managed-home-screen-icon]: icons/restore-managed-home-screen.svg
[retire-icon]: icons/retire.svg
[rotate-filevault-recovery-icon]: icons/rotate-filevault-recovery.svg
[rotate-local-admin-password-icon]: icons/rotate-local-admin-password.svg
[rotate-recovery-lock-icon]: icons/rotate-recovery-lock.svg
[run-remediation-icon]: icons/run-remediation.svg
[send-custom-notification-icon]: icons/send-custom-notification.svg
[shut-down-icon]: icons/shut-down.svg
[suspend-managed-home-screen-icon]: icons/suspend-managed-home-screen.svg
[sync-icon]: icons/sync.svg
[update-cellular-data-plan-icon]: icons/update-cellular-data-plan.svg
[update-defender-security-intelligence-icon]: icons/update-defender-intelligence.svg
[wipe-icon]: icons/wipe.svg