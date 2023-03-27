---
title: Local Windows Autopilot Reset in Intune
description: Local Windows Autopilot Reset in Intune.
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

# Enable local Windows Autopilot Reset

To enable a local Windows Autopilot Reset, the **DisableAutomaticReDeploymentCredentials** policy must be configured. This policy is documented in the [Policy CSP](/windows/client-management/mdm/policy-csp-credentialproviders#disableautomaticredeploymentcredentials). By default, local Windows Autopilot Reset is disabled. This default ensures that a local Autopilot Reset isn't triggered by accident.

## Enable local Windows Autopilot Reset in Intune

To create a configuration profile that sets the **DisableAutomaticReDeploymentCredentials** policy policy and enables local Windows Autopilot Reset in Intune, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **Policy**, select **Configuration Profiles**.

1. In the **Devices | Configuration profiles** screen, make sure **Profiles** is selected at the top, and then select **Create profile**.

1. In the **Create profile** window that opens:

   1. Under **Platform**, select **Windows 10 and later**.

   1. Under **Profile type**, select **Templates**.

   1. When the templates appear, under **Template name**, select **Device restrictions**. If **Device restrictions** is not visible, scroll through the **Template name** list until **Device restrictions** is visible. The list is in alphabetical order.

   1. Select **Create** to close the **Create profile** window.

1. The **Create profile** screen will open. In the **Basics** page:

   1. Next to **Name**, enter a name for the domain join profile.

   1. Next to **Description**, enter a description for the domain join profile.

   1. Select **Next**.

1. In the **Configuration settings** page:

   1. Select **General** to expand it.

   1. Under **General**, scroll down to **Autopilot Reset**.

   1. Next to **Autopilot Reset**, select **Allow**.

   1. Select **Next**.

1. In the **Assignments** page:

   1. Under **Included groups**, choose **Add groups**.

      > [!NOTE]
      >
      > Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** will result in those devices being excluded and they won't receive the Autopilot profile.

   1. In the **Select groups to include** window that opens, select the groups that the configuration profile should be assigned to. This device group(s) is normally the same device group(s) created when implementing the different [Autopilot scenarios](../autopilot-scenarios.md).

   1. Under **Included groups** > **Groups**, ensure the correct group(s) are selected, and then select **Next**.

1. In the **Applicability Rules** page, select **Next**. For the purpose of this tutorial, applicability rules is being skipped. However if applicability rules are needed, do so at this screen. For more information about scope tags, see [Applicability rules](/mem/intune/configuration/device-profile-create#applicability-rules).

1. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the domain join profile.

## Trigger local Windows Autopilot Reset

To trigger a local Windows Autopilot Reset on a device, follow the below steps:

1. Make sure that the [Windows Recovery Environment (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) is correctly configured and enabled on the device. WinRE can be enabled with the [REAgentC.exe tool](/windows-hardware/manufacture/desktop/reagentc-command-line-options) via the following command:

  ```cmd
  reagentc.exe /enable
  ```

1. Make sure that the device is in the device group where the Windows Autopilot Reset configuration profile was assigned to.

1. If you created a provisioning package that should be applied during the local Windows Autopilot Reset, plug in the USB drive that contains the provisioning package.

1. From the Windows device lock screen, enter the keystroke: **CTRL + ![Windows key](../../images/windows_glyph.png) + R**.

1. To trigger the local Autopilot Reset, sign into the device with an account that has local admin credentials.

Once the local Autopilot Reset is triggered, the reset process starts. Once provisioning is complete, the device is again ready for use.

## More information

For more information on Windows Autopilot Reset, see the following article(s):

- [Reset devices with local Windows Autopilot Reset](../../windows-autopilot-reset.md#reset-devices-with-local-windows-autopilot-reset)
