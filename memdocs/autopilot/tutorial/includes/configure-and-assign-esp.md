---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/11/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

azure-ad-join-esp.md
hybrid-azure-ad-join-esp.md
self-deploying-esp.md

Headings are driven by article context. -->

The main feature of the Enrollment Status Page (ESP) is to display progress and current status to the end user while the device is being set up and enrolled via the Autopilot process. The other main feature of the ESP is to block a user from signing in and using the device until all required policies and applications are installed. Multiple ESP profiles can be created with different settings and assigned appropriately based on different needs and scenarios.

Out of box there's a default ESP that is assigned to all devices. The default setting in the default ESP is to not show app and profile progress during the Autopilot process. However, it's highly recommended to change this default via a separate custom ESP to show app and profile progress. Enabling and configuring an ESP allows end users to properly see the progress of their device being set up and prevents them using the device until it's fully configured and provisioned. A user signing into the device before it's fully configured and provisioned can cause issues.

The ESP has two phases:

- Device ESP - ESP that runs during the OOBE process and applies device policies and installs device applications
- User ESP - ESP that runs after Device ESP that sets up user account, applies user policies, and installs user applications

The ESP can be configured to only display progress during the device ESP phase while disabling progress during the user ESP phase. Disabling of the user ESP is usually done to allow a user to sign into the device as soon as possible enabling them to reach the desktop quicker. However, the consequence is that not all of the user policies and applications may be installed. For this reason, it's recommended to show progress during both phases.

> [!TIP]
> For Configuration Manager admins, an ESP is similar and analogous to Configuration Manager client settings.

To configure and assign the Autopilot Enrollment Status Page (ESP) so that it shows progress during app and profile configurations, follow these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left pane.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **General**, select **Enrollment Status Page**.

6. In the **Enrollment Status Page** screen that opens, select **Create**.

7. The **Create profile** screen opens. In the **Basics** page:

   1. Next to **Name**, enter a name for the ESP profile.

   2. Next to **Description**, enter a description.

   3. Select **Next**.

8. In the **Settings** page, toggle the option **Show app and profile configuration progress** to **Yes**.

   1. After toggling the option **Show app and profile configuration progress** to **Yes**, several new options will appear. Configure these options based on the desired behavior for the ESP:

      - **Show an error when installation takes longer than specified number of minutes**: The default time-out is 60 minutes. Enter a higher value if you think more time is needed to install apps on the devices.

      - **Show custom message when time limit or error occur**:
        - **No**: The default message is shown to users when an error occurs. That message is: **Setup could not be completed. Please try again or contact your support person for help.**
        - **Yes**: A custom message is shown to users when an error occurs. Enter a custom message in the provided text box.

      - **Turn on log collection and diagnostics page for end users**:  
        - **No**: The collect logs button isn't shown to users when an installation error occurs. The Windows Autopilot diagnostics page isn't shown on devices running Windows 11.  
        - **Yes**: The collect logs button is shown to users when an installation error occurs. The Windows Autopilot diagnostics page is shown on devices running Windows 11. Logs and diagnostics may aid with troubleshooting. For this reason, it's recommended to enable this option.

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

   2. Once the different ESP options under the **Settings** page have been configured as desired, select **Next**.

9. In the **Assignments** page:

   1. Under **Included groups**, select **Add groups**.

   2. In the **Select groups to include** window that opens, select the device group(s) to target the ESP profile. The device group(s) selected would normally be the device group(s) created in the **Create device group** step.

   3. After selecting the device group, select **Select** to close the **Select groups to include** window.

    > [!TIP]
    >
    > After selecting the device group(s), you can select the **Edit filter** option on each device group added to the assignment to further refine what devices are targeted for the ESP profile. For example, this can be useful if you want to exclude some of the devices that are members in the device group(s) selected.

   4. Select **Next**.  

    > [!NOTE]
    >
    > ESPs are assigned to device groups and not directly to individual devices. To assign an ESP to a specific device, the device must be a member of a device group that has an ESP assigned to it.

10. In the **Scope tags** page, select **Next**.

    > [!NOTE]
    > **Scope tags** are optional and are a method to control who has access to the ESP configuration. For the purpose of this tutorial, scope tags is being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this screen. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune/fundamentals/scope-tags).

11. In the **Review + create** page, review the settings and verify everything is correct and configured as desired. Once verified, select **Create** to save the changes and assign the ESP profile.