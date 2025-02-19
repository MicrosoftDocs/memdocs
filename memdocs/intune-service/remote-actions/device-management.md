---
# required metadata

title: Run remote actions on devices with Microsoft Intune
description: Use Microsoft Intune to run remote actions on Android, iOS/iPadOS, macOS, and Windows devices. You can reset the password, lock the device, wipe or reset the OS, scan for viruses, and more. Use this feature to remotely manage devices and have help desk run common tasks.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 03/12/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ankitanangia
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Use remote actions to manage devices using Microsoft Intune

In Microsoft Intune, you can remotely run and execute commands on devices.

:::image type="content" source="./media/device-management/remote-actions-steps.png" alt-text="Diagram that shows how remote actions and commands work in Microsoft Intune." lightbox="./media/device-management/remote-actions-steps.png":::

For example:

- If a device is lost or stolen, you can reset or wipe the device.
- Your help desk can reset a password, lock the device, or collect diagnostic data.
- You can synchronize devices that haven't checked-in to Intune for a while.
- Do a quick scan or full scan of a device using Microsoft Defender Antivirus.
- And more

Use remote device actions to help you manage your devices remotely, without having to physically touch the device. This feature is available for devices that are enrolled in Intune and devices that are enrolled in other mobile device management (MDM) services.

This feature applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

This article shows you how to see the available remote actions, and lists some of the common remote actions you can run on your devices.

## Prerequisites

- To run remote actions, at a minimum, sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an account that has the **Help Desk Operator** role. For more information on the different roles, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

- To receive the remote action, the device must be connected to the internet and powered on.

## Get to your devices

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices**. This view shows detailed information about the individual devices, and what you can do with them, including:

    - **Overview**: Shows a visual snapshot of the enrolled devices, how many devices are using the different platforms, and more.
    - **All devices**: Shows a list of the enrolled devices you manage.

      Use the **Export** feature to create a `.zip`` list of all the devices, in increments of 10,000 (Internet Explorer) or 30,000 (Microsoft Edge, Chrome).

      Select any device to [view more details about that device](device-inventory.md), like hardware details, installed apps, policies, which remote actions are available for the device, and more.

    - **By platform**: View lists of devices by the specific platform.
    - **Enrollment**: Opens the enrollment page and lists the different enrollment options for each platform.
    - **Configuration**, **Compliance**, **Conditional Access**: These options let you create new policies and view & update existing policies.
    - **Device cleanup rules**: Automatically removes inactive devices from Intune. For more information, go to [Automatically delete devices with cleanup rules](devices-wipe.md#delete-devices-from-the-intune-admin-center).
    - **Device categories**: Create [device categories](../enrollment/device-group-mapping.md) to help organize devices and build dynamic device groups.
    - **Help and Support** provides a shortcut on troubleshooting tips, requesting support, or checking the status of Intune.

## Available remote actions

The available device actions depend on the device platform and the device configuration. Not all actions are available for all devices.

For a complete list of what can be done on your devices, in the Intune admin center, select **Devices** > **All devices**, and select a specific device. The available device actions are shown at the top.

The following list includes some common device actions:

| Action | Description | Supported OS |
|--------|-------------|--------------|
| [Autopilot reset](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) | Restores a device to its original settings and removes personal files, apps, and settings. | Windows |
| [BitLocker key rotation](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) | Changes the BitLocker recovery key for a device and uploads the new key to Intune. | Windows |
| [Collect diagnostics](collect-diagnostics.md)  | Collects diagnostic logs from a device and uploads the logs to Intune. | Windows 10 |
| [Delete](devices-wipe.md#delete-devices-from-the-intune-admin-center) | Removes a device from Intune management, any company data is removed, and the device is retired. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |
| [Disable Activation Lock](device-activation-lock-disable.md) | Removes the Activation Lock from a device that is enrolled with a device enrollment manager (DEM) account. | - iOS/iPadOS <br/>- macOS|
| [Fresh Start](device-fresh-start.md) | Reinstalls the latest version of Windows on a device and removes apps that the manufacturer installed. | Windows |
| [Full Scan](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) | Initiates a full scan of the device by Microsoft Defender Antivirus. | Windows |
| [Locate device](device-locate.md) | Shows the approximate location of a device on a map. | - Android <br/>- iOS/iPadOS <br/>- Windows |
| [Lost mode](device-lost-mode.md) | Locks a device with a custom message and disables sound and vibration. | iOS/iPadOS |
| [Pause Config Refresh](pause-config-refresh.md)|Pause ConfigRefresh to run remediation on a device for troubleshooting or maintenance or to make changes.| (Windows 11 only)|
| [Quick Scan](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) | Initiates a quick scan of the device by Microsoft Defender Antivirus. | Windows |
| [Remote control with Team Viewer](teamviewer-support.md) | Allows you to remotely control a device using TeamViewer. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |
| [Remote lock](device-remote-lock.md) | Locks a device and resets its password. | - Android <br/>- iOS/iPadOS <br/>- macOS  |
| [Rename device](device-rename.md) | Changes the device name in Intune. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |
| [Reset passcode](device-passcode-reset.md) | Resets the device passcode. | - Android <br/>- iOS/iPadOS |
| [Restart](device-restart.md) | Restarts a device. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |
| [Retire](devices-wipe.md#retire) | Removes company data and settings from a device, and leaves personal data intact. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |
| [Rotate Local admin password](../protect/windows-laps-policy.md#manually-rotate-passwords) | Changes the local administrator password for a device and stores the password in Intune. | Windows |
| [Send custom notification](custom-notifications.md) | Sends a custom notification message to a device that can be viewed in the Company Portal app. | - Android <br/>- iOS/iPadOS |
| [Synchronize device](device-sync.md) | Syncs a device with Intune to apply the latest policies and configurations. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |
| [Update cellular data plan](update-cellular-data-plan.md) | Updates the cellular data plan settings for a device that uses an eSIM profile. | iOS/iPadOS |
| [Update Windows Defender Security Intelligence](/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus) | Updates the security intelligence files for Microsoft Defender Antivirus. | Windows |
| [Windows 10 PIN reset](device-windows-pin-reset.md) | Resets the PIN of a device that uses Microsoft Entra authentication. | Windows 10 Mobile |
| [Wipe](devices-wipe.md#wipe) | This action restores a device to its factory settings and removes all data and settings. | - Android <br/>- iOS/iPadOS <br/>- macOS <br/>- Windows |

> [!NOTE]
> The **Retire**, **Wipe**, and **Delete** actions take precendence over all other actions. A device with multiple pending actions only carry out a Retire, Wipe, or Delete. All other pending actions are ignored.

You can also:

- See a [full device inventory](device-inventory.md) of all the devices (**Devices** > **All devices**).
- Run [bulk device actions](bulk-device-actions.md) on multiple devices at the same time (**Devices** > **All devices** > **Bulk Device Actions**).

## Resources

- [Bulk device actions](bulk-device-actions.md)
- [Troubleshoot device actions](/troubleshoot/mem/intune/device-management/troubleshoot-device-actions)
