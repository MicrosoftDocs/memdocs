---
title: Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 4 of 6 - Create a Windows Autopilot device preparation policy
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 4 of 6 - Create a Windows Autopilot device preparation policy.
ms.date: 06/11/2025
ms.topic: tutorial
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365 (preview): Create a Windows Autopilot device preparation policy

Windows Autopilot device preparation in automatic mode for Windows 365 steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
- Step 2: [Create an assigned device group](automatic-device-group.md)
- Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)

> [!div class="checklist"]
>
> - **Step 4: Create Windows Autopilot device preparation policy**

- Step 5: [Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md)
- Step 6: [Monitor the deployment](automatic-monitor.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 overview](automatic-workflow.md#workflow).

## Create an automatic mode for Windows 365 Windows Autopilot device preparation policy

The Windows Autopilot policy specifies how the device is configured during Windows Setup and what is shown during the out-of-box experience (OOBE).

To create an automatic mode for Windows 365 Windows Autopilot device preparation policy, follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot device preparation**, select **Device preparation policies**.

1. In the **Device preparation policies** screen, select **Create**, and then select **Automatic (Preview)**.

1. The **Create profile** screen opens. In the **Introduction** page, select **Next**.

1. In the **Basics** page:

   1. In the **Name** text box, enter a name for the Windows Autopilot device preparation policy.

   1. In the **Description** text box, if desired, enter a description for the Windows Autopilot device preparation policy.

   1. Once a name and description is entered, select **Next**.

1. In the **Device group** page, select the **Search by group name..** box, and then either select or search for the device group created in [Step 3: Create an assigned device group](automatic-device-group.md). Once the correct device group is selected, select **Next**.

1. In the **Configuration settings** page:

   1. The **Apps** section allows selection of up to 10 managed applications reference with the deployment. The applications specified here should be the essential applications that should be installed on the device before the end-user can start using the device. Under the **Apps** section:

      1. Select **Add**. The **Select Apps** pane opens.

         1. In the **Select Apps** pane:

         1. Scroll through the list of applications or use the **Search** box to search for desired applications.

         1. Once a desired application is found, select the **Add** button next to the application. The application is added to the list under **Selected Apps**.

         1. Once all of the desired applications are selected, select **Save**.

        All of the selected applications should display under **Allowed Applications**.

      > [!IMPORTANT]
      >
      > The applications selected in this setting should be assigned to the device security group previously specified in the **Device group** page. If applicable, the applications should also be configured to install in the **System** context since it's installed during OOBE when no user is signed in.

      > [!NOTE]
      >
      > The following types of applications are supported for use with Windows Autopilot device preparation:
      >
      > - [Line-of-business (LOB)](/mem/intune-service/apps/lob-apps-windows).
      > - [Win32](/mem/intune-service/apps/apps-win32-prepare).
      > - [Microsoft Store](/mem/intune-service/apps/store-apps-microsoft) - only Microsoft Store apps that support WinGet are supported.
      > - [Microsoft 365](/mem/intune-service/apps/apps-add-office365).
      >
      > In addition, Windows Autopilot device preparation supports deploying both Win32 and line-of-business (LOB) applications in the same deployment.

   1. The **Scripts** section allows selection of up to 10 PowerShell scripts to install during the deployment. The PowerShell scripts specified here should be the essential PowerShell scripts that should run on the device before the end-user can start using the device. Under the **Scripts** section:

      1. Select **Add**. The **Select Scripts** pane opens.

      1. In the **Select Scripts** pane:

         1. Scroll through the list of PowerShell scripts or use the **Search** box to search for desired PowerShell scripts.

         1. Once a desired PowerShell script is found, select the **Add** button next to the PowerShell script. The PowerShell script is added to the list under **Selected Scripts**.

         1. Once all of the desired PowerShell scripts are selected, select **Save**.

        All of the selected PowerShell scripts should display under **Allowed Scripts**.

   > [!IMPORTANT]
   >
   > The PowerShell scripts selected in this setting should be assigned to the device security group previously specified in the **Device group** page. The PowerShell script should also be configured to run in the **System** context since the PowerShell scripts run during OOBE when no user is signed in. The PowerShell script can be set to run in the **System** context by setting the option **Run this script using the logged on credentials** to **No** in the properties of the PowerShell script.

   1. Once all of the desired **Apps** and **Scripts** are selected, select **Next**.

1. In the **Scope tags** page, select **Next**.

    > [!NOTE]
    >
    > **Scope tags** are optional. For this tutorial, scope tags are being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune-service/fundamentals/scope-tags).

1. In the **Review + create** page, review all settings to make sure they're all correct. Once everything is verified, select **Save** to finish creating the Windows Autopilot device preparation policy.

> [!TIP]
>
> When a Windows Autopilot device preparation policy for automatic mode is created, there's no **Assignments** page for assigning the policy. Instead, the assignment is taken care of when creating the Cloud PC provisioning policy during [Step 5: Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md).

## Next step: Create a Cloud PC provisioning policy

> [!div class="nextstepaction"]
> [Step 5: Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md)
