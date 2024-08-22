---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-esp.md
pre-provisioning/hybrid-azure-ad-join-esp.md
self-deploying/self-deploying-esp.md
user-driven/azure-ad-join-esp.md
user-driven/hybrid-azure-ad-join-esp.md

Headings are driven by article context. -->

The main feature of the Enrollment Status Page (ESP) is to display progress and current status to the end user while the device is being set up and enrolled via the Autopilot process. The other main feature of the ESP is to block a user from signing in and using the device until all required policies and applications are installed. Multiple ESP profiles can be created with different settings and assigned appropriately based on different needs and scenarios.

Out of box there's a default ESP that is assigned to all devices. The default setting in the default ESP is to not show app and profile progress during the Autopilot process. However, Microsoft recommends changing this default via a separate custom ESP to show app and profile progress. Enabling and configuring an ESP allows end users to properly see the progress of their device being set up and prevents them using the device until the device is fully configured and provisioned. A user signing into the device before being fully configured and provisioned can cause issues.

The ESP has two phases:

- **Device ESP** - The portion of the ESP that runs during the OOBE process and applies device policies and installs device applications.
- **User ESP** - The portion of the ESP that sets up user account, applies user policies, and installs user applications.

Device ESP runs first followed by the User ESP.

> [!TIP]
>
> For Configuration Manager admins, an ESP is similar and analogous to Configuration Manager client settings.

## Autopilot Enrollment Status Page (ESP) configuration options

When the Enrollment Status Page (ESP) is configured, it has several options that can be configured to meet the needs of the organization. The following lists the different options and their possible configurations:

- **Show an error when installation takes longer than specified number of minutes**:

  - The default time-out is 60 minutes. Enter a higher value if more time is needed to install applications on the devices.

- **Show custom message when time limit or error occur**:

  - **No**: The default message is shown to users when an error occurs. That message is: **Setup could not be completed. Please try again or contact your support person for help.**

  - **Yes**: A custom message is shown to users when an error occurs. Enter a custom message in the provided text box.

- **Turn on log collection and diagnostics page for end users**:

  - **No**: The collect logs button isn't shown to users when an installation error occurs. The Windows Autopilot diagnostics page isn't shown on devices running Windows 11.

  - **Yes**: The collect logs button is shown to users when an installation error occurs. The Windows Autopilot diagnostics page is shown on devices running Windows 11. Logs and diagnostics might aid with troubleshooting. For this reason, Microsoft recommends enabling this option.

- **Only show page to devices provisioned by out-of-box experience (OOBE)**:

  - **No**: The enrollment status page (ESP) is shown during the device phase and the out-of-box experience (OOBE). The page is also shown during the user phase to every user who signs into the device for the first time.

  - **Yes**: The enrollment status page (ESP) is shown during the device phase and the OOBE. The page is also shown during the user phase, but only to the first user who signs into the device. It isn't shown to subsequent users who sign into the device.

- **Block device use until all apps and profiles are installed**:

  - **No**: Users can leave the ESP before Intune is finished setting up the device.

  - **Yes**: Users can't leave the ESP until Intune is done setting up the device. Enabling this option unlocks the following additional options:

    - **Allow users to reset device if installation error occurs**:

      - **No**: The ESP doesn't give users the option to reset theirs devices when an installation fails.

      - **Yes**: The ESP gives users the option to reset their devices when an installation fails.

    - **Allow users to use device if installation error occurs**:

      - **No**: The ESP doesn't give users the option to bypass the ESP when an installation fails.

      - **Yes**: The ESP gives users the option to bypass the ESP and use their devices when an installation fails.

    - **Block device use until these required apps are installed if they are assigned to the user/device**:

      - **All**: All assigned apps must be installed before users can use their devices.

      - **Selected**: Selected apps must be installed before users can use their devices. After enabling this option, select **Select apps** to select the managed apps from Intune that are required to be installed before users can use their device.

## Configure and assign the Enrollment Status Page (ESP)

To configure and assign the Autopilot Enrollment Status Page (ESP), follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1 In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Enrollment Status Page**.

1. In the **Enrollment Status Page** screen that opens, select **Create**.

1. The **Create profile** screen opens. In the **Basics** page:

   1. Next to **Name**, enter a name for the ESP profile.

   1. Next to **Description**, enter a description.

   1. Select **Next**.

1. In the **Settings** page, toggle the option **Show app and profile configuration progress** to **Yes**.

   1. After the option **Show app and profile configuration progress** is toggled to **Yes**, several new options will appear. Configure these options based on the desired behavior for the ESP as described in the section [Autopilot Enrollment Status Page (ESP) configuration options](#autopilot-enrollment-status-page-esp-configuration-options):

   1. Once the different ESP options under the **Settings** page are configured as desired, select **Next**.

1. In the **Assignments** page:

   1. Under **Included groups**, select **Add groups**.

   1. In the **Select groups to include** window that opens, select the device groups to target the ESP profile. The device groups selected would normally be the device groups created in the **Create device group** step.

   1. After selecting the device group, select **Select** to close the **Select groups to include** window.

      > [!TIP]
      >
      > After selecting the device groups, the **Edit filter** option can be selected on each device group added to the assignment to further refine what devices are targeted for the ESP profile. For example, further filtering can be useful if some of the devices that are members in the device groups selected need to be excluded.

   1. Select **Next**.

    > [!NOTE]
    >
    > An ESP is assigned to a device group and not directly to individual devices. To assign an ESP to a specific device, the device must be a member of a device group that has an ESP assigned to it.

1. In the **Scope tags** page, select **Next**.

    > [!NOTE]
    >
    > **Scope tags** are optional and are a method to control who has access to the ESP configuration. For this tutorial, scope tags are being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this screen. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune/fundamentals/scope-tags).

1. In the **Review + create** page, verify that the settings are correct and configured as desired. Once verified, select **Create** to save the changes and assign the ESP profile.
