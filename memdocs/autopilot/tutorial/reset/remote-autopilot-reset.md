---
title: Remote Windows Autopilot Reset in Intune
description: Remote Windows Autopilot Reset in Intune.
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

# Reset devices with remote Windows Autopilot Reset

You can use Intune to start the remote Windows Autopilot Reset process. Resetting in this way avoids the need for someone to visit each device that needs to be reset to start the Windows Autopilot Reset process. Unlike [local Windows Autopilot reset](local-autopilot-reset.md), a configuration profile doesn't need to be configured or assigned for remote Windows Autopilot Reset to work. Remote Windows Autopilot Reset is available on any Azure AD join device that is an Autopilot device without any additional configuration.

## Triggering a remote Windows Autopilot Reset

To trigger a remote Windows Autopilot Reset via Intune, follow these steps:

1. Make sure that the [Windows Recovery Environment (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) is correctly configured and enabled on the device. WinRE can be enabled with the [REAgentC.exe tool](/windows-hardware/manufacture/desktop/reagentc-command-line-options) via the following command:

  ```cmd
  reagentc.exe /enable
  ```

1. Make sure the Intune admin initiating the remote Windows Autopilot Reset is a member of the Intune Service Administrator role. For more information, see [Add users and grant administrative permission to Intune](../../../intune/fundamentals/users-add.md).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device name** select the targeted devices to perform the Windows Autopilot Reset.

1. In the page that opens that displays the properties of the device, select **Autopilot Reset** in the toolbar at the top of the window to start the Autopilot reset.

1. An Autopilot Reset warning message will be displayed. Select **Yes** to continue.

1. A message should display confirming that the Autopilot reset has been initiated.

Once the Autopilot Reset is complete, the device is again ready for use.

## Forcing a device to start the remote Windows Autopilot Reset

Unlike [local Windows Autopilot reset](local-autopilot-reset.md), when the remote Autopilot reset is initiated for a device, the reset may not start immediately. Instead, the reset will occur when the device next checks in with Intune and gets updated policy. For more information, see [Policy refresh intervals](../../../intune/configuration/device-profile-troubleshoot.md#policy-refresh-intervals)

An Autopilot Reset can be forced to start sooner on a device by forcing the device to obtain the latest Intune policy. This can be done either remotely or locally on the device.

### Remotely force a device to start the remote Windows Autopilot Reset

To force the device to obtain the latest Intune policy remotely, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device name** select the devices where the remote Windows Autopilot Reset was initiated.

1. In the page that opens that displays the properties of the device, select **Sync** in the toolbar at the top of the window to start the Autopilot reset.

1. A Sync warning message will be displayed. Select **Yes** to continue.

This should force the device to obtain the latest Intune policy. The Autopilot Reset should start shortly thereafter.

### Locally force a device to start the remote Windows Autopilot Reset

To force the device to obtain the latest Intune policy locally on the device, follow the below steps:

1. Sign into the device where the remote Autopilot Reset was initiated.

2. Open **Settings** from the Start Menu.

3. In **Settings**, select **Accounts** in the left hand pane.

4. In the **Accounts** page, select **Access work or school**.

5. In the **Accounts > Access work or school** page, select **Connected by <user@domain>** to open a new section.

6. In the new section, next to **Managed by <organization>**, select the **Info** button.

7. In the **Accounts > Access work or school > Managed by <organization>** page, under **Device sync status**, select the **Sync** button.

This should force the device to obtain the latest Intune policy. The Autopilot Reset should start shortly thereafter.

## More information

For more information on local Windows Autopilot Reset, see the following article(s):

- [Reset devices with remote Windows Autopilot Reset](../../windows-autopilot-reset.md#reset-devices-with-remote-windows-autopilot-reset)
- [Windows Recovery Environment (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
- [REAgentC.exe tool](/windows-hardware/manufacture/desktop/reagentc-command-line-options)
- [Add users and grant administrative permission to Intune](../../../intune/fundamentals/users-add.md)
- [Policy refresh intervals](../../../intune/configuration/device-profile-troubleshoot.md#policy-refresh-intervals)
