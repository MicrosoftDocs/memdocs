---
# required metadata

title: Manage devices with Microsoft Intune
description: Review the devices you manage with Microsoft Intune, including exporting a devices list into csv format, view your Azure Active Directory-joined devices, review a change log of actions on the device, use TeamViewer Connector to allow IT admins remotely troubleshoot Android devices, and view all the actions you can run on your devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 12/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# What is Microsoft Intune device management?

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

As an IT admin, you must ensure that managed devices are providing the resources that your users need to do their work, while protecting that data from risk.

The **Devices** workload gives you insights into the devices you manage, and lets you activate remote tasks on those devices.

Not all device actions are available for every platform or device. Available actions are shown on the device's overview page (**Devices** > **All devices** > choose a device).

## Get to your devices

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices**. This view shows detailed information about the individual devices, and what you can do with them, including:

   - **Overview**: The Overview page shows a visual snapshot of the enrolled devices, how many devices are using the different platforms, and more.
   - **All devices**: The All devices page shows a list of the enrolled devices you manage.

     Use the **Export** feature to create a .zip list of all the devices, in increments of 10,000 (Internet Explorer) or 30,000 (Microsoft Edge, Chrome).

     Select any device to [view additional details about that device](device-inventory.md), like hardware details, installed apps, policies, which remote actions are available for the device, and more.

   - **By platform**: The items under By platform let you view lists of devices by the specific platform.
   - **Device enrollment**: This option takes you to the enrollment page.
   - **Policy**: These options let you set various policies for your organization's devices.
   - **Other**:
       - **Device cleanup rules**: This option lets you automatically remove inactive devices from Intune. For more information, see [Automatically delete devices with cleanup rules](devices-wipe.md#delete-devices-from-the-intune-portal).
       - **Device categories**: This option lets you create [device categories](../enrollment/device-group-mapping.md).
   - **Help and Support** provides a shortcut on troubleshooting tips, requesting support, or checking the status of Intune.

## Available device actions

The available actions depend on the device platform and the device configuration. The following list includes some common device actions. For a complete list of what can be done on your devices, select **All devices**, and select a specific device. The available actions are shown at the top.

- [View device inventory](device-inventory.md): To see a full inventory of all the devices, select **Devices** > **All devices**.
- To run - [bulk device actions](bulk-device-actions.md) on multiple devices at the same time, select **Devices** > **All devices** > **Bulk Device Actions**.
- To run remote actions on a single device, select the device from the **All devices** page and then select the specific remote action at the top of the individual device page. Not all actions are available for all devices.
  - [Autopilot reset](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (Windows Only)
  - [BitLocker key rotation](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) (Windows only)
  - [Collect diagnostics](collect-diagnostics.md) (Windows 10 only)
  - [Delete](devices-wipe.md#delete-devices-from-the-intune-portal)
  - [Disable Activation Lock](device-activation-lock-disable.md) (iOS only)
  - [Erase](./device-erase.md) (macOS Only)
  - [Fresh Start](device-fresh-start.md) (Windows only)
  - [Full Scan](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (Windows 10 only)
  - [Locate device](device-locate.md) (iOS only)
  - [Lost mode](device-lost-mode.md) (iOS only)
  - [Quick Scan](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (Windows 10 only)
  - [Remote control for Android](teamviewer-support.md)
  - [Remote lock](device-remote-lock.md)
  - [Rename device](device-rename.md)
  - [Reset passcode](device-passcode-reset.md)
  - [Restart](device-restart.md) (Windows only)
  - [Retire](devices-wipe.md#retire)
  - [Update Windows Defender Security Intelligence](/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus)
  - [Windows 10 PIN reset](device-windows-pin-reset.md)
  - [Wipe](devices-wipe.md#wipe)
  - [Send custom notification](custom-notifications.md#send-a-custom-notification-to-a-single-device) (Android, iOS/iPadOS)
  - [Synchronize device](device-sync.md)
  - [Update cellular data plan](update-cellular-data-plan.md) (iOS/iPadOS)


## Next steps

[Remotely run device actions with Intune](./index.yml)