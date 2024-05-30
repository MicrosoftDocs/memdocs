---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 5 of 7 - Assign applications and PowerShell scripts to device group
description: How to - Windows Autopilot device preparation user-driven Microsoft Entra join - Step 5 of 7 - Assign applications and PowerShell scripts to device group.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/31/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Assign applications and PowerShell scripts to device group

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create a device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)

> [!div class="checklist"]
>
> - **Step 5: Assign applications and PowerShell scripts to device group**

- Step 6: [Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)
- Step 7: [Add Windows corporate identifier to device (optional)](entra-join-corporate-identifier.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

## Assign applications and PowerShell scripts to device group

During the out-of-box experience (OOBE) experience before the end-user is signed in for the first time, Windows Autopilot device preparation allows deployment of up to:

- 10 managed applications
- 10 PowerShell scripts

The applications and PowerShell scripts specified should be the essential applications to install and the essential PowerShell scripts to run before the end-user can start using the device.

Any applications installed or PowerShell scripts that run during a Windows Autopilot device preparation deployment should be configured to install in the **System** context since the applications are installed and the PowerShell scripts ran during OOBE when no user is signed in.

In order for applications to install and for PowerShell scripts to run successfully, they must be assigned to the device group created for Windows Autopilot device preparation in [Step 3: Create a device group](entra-join-device-group.md).

> [!NOTE]
>
> The below steps assume that the applications or PowerShell scripts that will be deployed during Windows Autopilot device preparation deployment are already added to Intune. For more information on how to add applications and PowerShell scripts to Intune if they aren't already created, see [Add apps to Microsoft Intune](/mem/intune/apps/apps-add) and [Use PowerShell scripts on Windows devices in Intune](/mem/intune/apps/intune-management-extension).

### Applications

The following types of applications are supported for use with Windows Autopilot device preparation:

- [Line-of-business](/mem/intune/apps/lob-apps-windows).
- [Win32](/mem/intune/apps/apps-win32-prepare).
- [WinGet (Microsoft Store)](/mem/intune/apps/store-apps-microsoft).
- [Microsoft 365](/mem/intune/apps/apps-add-office365).

In addition, Windows Autopilot device preparation supports deploying both Win32 and line-of-business (LOB) applications in the same deployment.

To assign the desired applications to the device group created for Windows Autopilot device preparation:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Apps** in the left hand pane.

3. In the **Apps | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows apps** screen, scroll through the list of applications and then select the desired application that will be installed during the Windows Autopilot device preparation deployment. Alternatively, use the **Search by name or publisher** box to search for the application, and then select it.

5. Once the application is selected, a new screen opens showing the application. Under **Manage**, select **Properties**.

6. In the **Properties** screen, next to **Assignments**, select **Edit**.

7. In the **Edit application** screen:

   1. Under the **Required** section, select **+ Add group**. The **Select groups** pane opens.

   2. In the **Select groups** pane:

      1. Scroll through the list of groups. Once the Windows Autopilot device preparation device security group is located, select it. Alternatively, use the **Search** box to locate the Windows Autopilot device preparation device security group and then select it.

      2. Once the Windows Autopilot device preparation device security group is selected, select the **Select** button.

   3. Verify that the Windows Autopilot device preparation device security group is listed under the **Required** section. Additionally, verify that **Group mode** is set to **Included**. When applicable, also verify that **Install Context** is set to **Device context**.

   4. Once everything is verified, select the **Review + save** button.

   5. In the **Review + save** screen, select the **Save** button.

8. Repeat the steps for any additional applications that need to be installed during the Windows Autopilot device preparation deployment.

### PowerShell scripts

To assign the desired PowerShell scripts to the device group created for Windows Autopilot device preparation:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left hand pane.

3. In the **Devices | Overview** screen, under **manage devices**, select **Scripts and remediations**.

4. In the **Devices | Scripts and remediations** screen:

   1. Select **Platform scripts**.

   2. Scroll through the list of PowerShell scripts and then select the desired PowerShell script that will run during the Windows Autopilot device preparation deployment. Alternatively, use the **Search** box to search for the PowerShell script, and then select it.

5. Once the PowerShell script is selected, a new screen opens showing the PowerShell script. Under **Manage**, select **Properties**.

6. In the **Properties** screen, next to **Assignments**, select **Edit**.

7. In the **Edit PowerShell script** screen:

   1. Under the **Included groups** section, select **Add groups**. The **Select groups to include** pane opens.

   2. In the **Select groups to include** pane:

      1. Scroll through the list of groups. Once the Windows Autopilot device preparation device security group is located, select it. Alternatively, use the **Search** box to locate the Windows Autopilot device preparation device security group and then select it.

      2. Once the Windows Autopilot device preparation device security group is selected, select the **Select** button.

   3. Verify that the Windows Autopilot device preparation device security group is listed under the **Included groups** section. Make sure that the Windows Autopilot device preparation device security group wasn't accidentally added under the **Excluded groups** section.

   4. Once everything is verified, select the **Review + save** button.

   5. In the **Review + save** screen, select the **Save** button.

## Next step: Create Windows Autopilot device preparation policy

> [!div class="nextstepaction"]
> [Step 6: Create Windows Autopilot device preparation policy](entra-join-autopilot-policy.md)

## More information

- [Add apps to Microsoft Intune](/mem/intune/apps/apps-add).
- [Use PowerShell scripts on Windows devices in Intune](/mem/intune/apps/intune-management-extension).
- [Assign apps to groups with Microsoft Intune](/mem/intune/apps/apps-deploy).
- [Win32 app management in Microsoft Intune](/mem/intune/apps/apps-win32-app-management).
- [Add a Windows line-of-business app to Microsoft Intune](/mem/intune/apps/lob-apps-windows).
