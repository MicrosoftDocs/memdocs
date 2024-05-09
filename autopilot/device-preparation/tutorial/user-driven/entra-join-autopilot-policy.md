---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 6 of 6 - Create a user-driven Microsoft Entra join Autopilot policy
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 6 of 6 - Create a user-driven Microsoft Entra join Autopilot policy.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/08/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation User-driven Microsoft Entra join: Create user-driven Microsoft Entra join Windows Autopilot device preparation policy

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create a device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and scripts to device group](entra-join-assign-apps-scripts.md)

> [!div class="checklist"]
> - **Step 6: Create Windows Autopilot device preparation policy**

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

## Create user-driven Microsoft Entra join Windows Autopilot device preparation policy

The Autopilot policy specifies how the device is configured during Windows Setup and what is shown during the out of box experience (OOBE).

To create a user-driven Microsoft Entra join Windows Autopilot device preparation policy, follow these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left hand pane.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **Windows Autopilot device preparation**, select **Device preparation policies**.

6. In the **Device preparation policies** screen, select **Create**.

7. The **Create profile** screen opens. In the **Introduction** page, select the **Next** button.

8. In the **Basics** page:

   1. In the **Name** text box, enter a name for the Windows Autopilot device preparation policy.
   2. In the **Description** text box, if desired, enter a description for the Windows Autopilot device preparation policy.
   3. Once a name and description have been entered, select the **Next** button.

9. In the **Device group** page, select the **Search by group name..** box, and then either select or search for the device group created in [Step 3: Create a device group](entra-join-device-group.md). Make sure to select the device group created in [Step 3: Create a device group](entra-join-device-group.md) and not the user group created in [Step 4: Create a user group](entra-join-user-group.md). Once the correct device group has been selected, select the **Next** button.

10. In the **Configuration settings** page:

    1. Expand the **Out-of-box experience settings** section by selecting it.

       1. Next to **Minutes allowed before showing installation error**, enter the number of minutes allowed before the installation fails and shows an error. The acceptable value is an integer between 15 and 720.

       2. For **Custom error message**, enter a message to display to the end-user if a failure or error occurs.

       3. For **Allow users to skip setup after multiple attempts**, select either **Yes** or **No** as desired by toggling the switch.

       4. For **Show link to diagnostics**, select either **Yes** or **No** as desired by toggling the switch. If set to **Yes**, this option will display a link to the end-user allowing them to retrieve diagnostic logs in case of a failure.

    2. Expand the **Apps** section by selecting it:

        The **Apps** section allows selection of up to ten managed applications reference with the deployment. The apps specified here should be the critical apps that should be installed on the device before the end-user can start using the device.

        > [!IMPORTANT]
        >
        > The applications selected in this setting should be assigned to the device security group previously specified in the **Device group** page. If applicable, the applications should also be configured to install in the **System** context since it is installed during OOBE when no user is signed in.

       1. Under **Allowed Applications**, select **Add**. The **Select Apps** pane opens.
       2. In the **Select Apps** pane:
          1. Scroll through the list of applications or use the **Search** box to search for desired applications.
          2. Once a desired application is found, select the **Add** button next to the application. The application will be added in the list under **Selected Apps**.
          3. Once all of the desired applications have been selected, select the **Save** button. All of the selected applications should display under **Allowed Applications**.

    3. Expand the **Deployment settings** section by selecting it:

       1. Next to **Deployment mode**, select **Single user** in the drop down menu.
       2. Next to **Deployment type**, select **User driven** in the drop down menu.
       3. Next to **Join type**, select **Azure Ad joined** in the drop down menu.
       4. Next to **User account type**, select either **Standard User** or **Administrator** as desired by toggling the switch.

    4. Expand the **Scripts** section by selecting it:

        The **Apps** section allows selection of up to 10 PowerShell scripts to install during the deployment. The scripts specified here should be the critical scripts that should run on the device before the end-user can start using the device.

        > [!IMPORTANT]
        >
        > The PowerShell scripts selected in this setting should be assigned to the device security group previously specified in the **Device group** page. The PowerShell script should also be configured to run in the **System** context since the scripts runs during OOBE when no user is signed in. The script can be set to run in the **System** context by setting the option **Run this script using the logged on credentials** to **No** in the properties of the script.

       1. Under **Allowed Scripts**, select **Add**. The **Select Scripts** pane opens.
       2. In the **Select Scripts** pane:
          1. Scroll through the list of scripts or use the **Search** box to search for desired scripts.
          2. Once a desired script is found, select the **Add** button next to the script. The script will be added in the list under **Selected Scripts**.
          3. Once all of the desired scripts have been selected, select the **Save** button. All of the selected scripts should display under **Allowed Scripts**.

    5. Once all of the configuration settings have been configured as desired, select the **Next** button.

11. In the **Scope tags** page, select **Next**.

    > [!NOTE]
    >
    > **Scope tags** are optional. For the purpose of this tutorial, scope tags is being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune/fundamentals/scope-tags).

12. In the **Assignments** page, select the **Search by group name..** box, and then either select or search for the user group created in [Step 4: Create a user group](entra-join-user-group.md). Make sure to select the user group created in [Step 4: Create a user group](entra-join-user-group.md) and not the device group created in [Step 3: Create a device group](entra-join-device-group.md). Once the correct user group has been selected, select the **Next** button.

13. In the **Review + create** page, review all settings to make sure they're all correct. Once everything is verified, select the **Save** button to finish creating the Windows Autopilot device preparation policy.

## More information
