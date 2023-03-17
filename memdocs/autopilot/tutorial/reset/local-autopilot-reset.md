---
title: Local Windows Autopilot reset in Intune
description: Local Windows Autopilot reset in Intune.
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

# Enable local Windows Autopilot reset

## Reset devices with local Windows Autopilot Reset

The Intune Service Administrator role is required for this task. For more information, see [Add users and grant administrative permission to Intune](/intune/users-add).

IT admins can use a local Windows Autopilot Reset to:

- Quickly remove personal files, apps, and settings.
- Reset Windows devices from the lock screen.
- Apply original settings and management enrollment (Azure Active Directory and device management)
The device is then ready to use. With a local Autopilot Reset, devices are returned to a fully configured or known IT-approved state.

To enable local Autopilot Reset in Windows 10:

1. [Enable the policy for the feature](#enable-local-windows-autopilot-reset)
2. [Trigger a reset for each device](#trigger-local-windows-autopilot-reset)

## Enable local Windows Autopilot reset in Intune

To enable a local Windows Autopilot Reset, the **DisableAutomaticReDeploymentCredentials** policy must be configured. This policy is documented in the [Policy CSP](/windows/client-management/mdm/policy-csp-credentialproviders), **CredentialProviders/DisableAutomaticReDeploymentCredentials**. By default, local Windows Autopilot Reset is disabled. This default ensures that a local Autopilot Reset isn't triggered by accident.




To create a configuration profile that enables local Windows Autopilot reset, follow the below steps:

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

   1. In the **Select groups to include** window that opens, select the groups that the configuration profile should be assigned to. This device group(s) is normally the device group(s) created in the step [Create device group](autopilot-reset-device-group.md). Once done, select **Select**.

   1. Under **Included groups** > **Groups**, ensure the correct group(s) are selected, and then select **Next**.

1. In the **Applicability Rules** page, select **Next**. For the purpose of this tutorial, applicability rules is being skipped. However if applicability rules are needed, do so at this screen. For more information about scope tags, see [Applicability rules](/mem/intune/configuration/device-profile-create#applicability-rules).

1. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the domain join profile.



### Trigger local Windows Autopilot Reset

A local Windows Autopilot Reset is a two-step process: trigger it and then authenticate. Once you've done these two steps, you can let the process execute and once it is done, the device is again ready for use.

**To trigger a local Autopilot Reset:**

1. From the Windows device lock screen, enter the keystroke: **CTRL + ![Windows key](images/windows_glyph.png) + R**.

    ![Enter CTRL+Windows key+R on the Windows lock screen](images/autopilot-reset-lockscreen.png)

    These keystrokes will open up a custom login screen for the local Autopilot Reset. The screen serves two purposes:
    1. Confirm/verify that the end user has the right to trigger Local Autopilot Reset
    2. Notify the user in case a provisioning package, created using Windows Configuration Designer, will be used as part of the process.

        ![Custom login screen for local Autopilot Reset](images/autopilot-reset-customlogin.png)

2. Sign in with the admin account credentials. If you created a provisioning package, plug in the USB drive and trigger the local Autopilot Reset.

 Once the local Autopilot Reset is triggered, the reset process starts. Once provisioning is complete, the device is again ready for use.


## More information

For more information on Windows Autopilot Reset, see the following article(s):

- [Windows Autopilot Reset](/mem/autopilot/windows-autopilot-reset)
