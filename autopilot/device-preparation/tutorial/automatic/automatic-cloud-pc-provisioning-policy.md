---
title: Windows Autopilot device preparation in automatic mode for Windows 365 - Step 5 of 5 - Create a Cloud PC provisioning policy
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 - Step 5 of 5 - Create a Cloud PC provisioning policy.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: aaroncz
ms.date: 05/20/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365: Create a Cloud PC provisioning policy

Windows Autopilot device preparation in automatic mode for Windows 365 steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
- Step 2: [Create an assigned device group](automatic-device-group.md)
- Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 4: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)

> [!div class="checklist"]
>
> - **Step 5: Create a Cloud PC provisioning policy**

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 overview](automatic-workflow.md#workflow).

## Create a Cloud PC provisioning policy for use with Windows Autopilot device preparation in automatic mode for Windows 365

To create a Cloud PC provisioning policy for use with Windows Autopilot device preparation in automatic mode for Windows 365 , follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Windows 365**.

1. In the **Devices | Windows 365** screen, select **Provisioning policies**, and then select **Create policy**.
1. In the **Create a provisioning policy** screen:

   1. In the **General** page:

      1. In the **Name** text box, enter a name for the Windows 365 Cloud PC policy.

      1. In the **Description** text box, if desired, enter a description for the Windows 365 Cloud PC policy.

      1. Next to **License type**, select **Frontline**.

      1. Next to **Frontline type**, select **Shared (Preview)**.

      1. Under the **Join type details** section:

         1. Next to **Join type**, make sure **Microsoft Entra Join** is selected.

         1. Next to **Network**, make sure **Microsoft hosted network** is selected.

         1. Next to **Geography** and **Region**, make sure the appropriate geography and region settings are set as desired using the drop down menus.

         1. Select the option **Use Microsoft Entra single sign-on** to enable it.

      1. Once all settings are properly configured in the **General** page, select **Next**.

   1. In the **Image** page, select a [supported version of Windows](../../requirements.md#windows-365-cloud-pcs) from the **Gallery image** drop down menu, and then select **Next**.

   1. In the **Configuration** page:

      1. Next to **Language & Region** under **Windows Settings**, select the desired language and region setting using the drop down menu.

      1. If desired, select **Apply device name template** under **Cloud PC naming**.

      1. Under **Windows Autopilot**:

         1. Next to **Autopilot Device preparation policy**, use the drop down menu to select the Windows Autopilot device preparation policy created in [Step 4: Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md).

         1. Next to **Minutes allowed before device preparation fails**, enter a value in minutes that allows adequate time to install the apps and scripts defined in the Windows Autopilot device preparation policy. For example, enter **60** for 60 minutes. The recommended minimum value should be no lower than 30. If the apps and scripts aren't finished installing by this time, the device preparation fails. However, the provisioning continues.

         1. To prevent users from connecting to the Cloud PC is the deployment fails or times out, select the option **Prevent users from connection to Cloud PC upon installation failure or timeout**. To allow users to connect to the Cloud PC even when the deployment fails or times out, leave this option unchecked.

      1. Once all settings are properly configured in the **Configuration** page, select **Next**.

   1. In the **Scope tags** page, select **Next**.

      > [!NOTE]
      >
      > **Scope tags** are optional. For this tutorial, scope tags are being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune-service/fundamentals/scope-tags).

   1. In the **Assignments** page:

      1. Select **Add groups**. The **Select groups to include** pane opens. In the **Select groups to include** pane:

         1. In the **Search** text box, enter the name of the assigned device group created in [Step 2: Create an assigned device group](automatic-device-group.md).

         1. Once the device group is found, select it under **Name**.

         1. Select the **Select** button.

      1. Next to the selected device group, select the **Select one** link under **Cloud PC size**. The **Select Cloud PC size** pane opens. In the **Select Cloud PC size** pane:

         1. In the **Available Cloud PCs** drop down menu under the **Cloud PC size** section, select the desired Cloud PC configuration.

         1. Under the **Assignment** section:

            1. In the **Name** text box, enter a name for the assignment.

            1. In the **Remaining Cloud PCs** text box, enter the desired amount of Cloud PCs that should be provisioned. The number of available Cloud PC licenses is displayed next **Remaining Cloud PCs** and it decrements based on the number entered in the **Remaining Cloud PCs** text box.

         1. Once everything is configured as desired in the **Select Cloud PC size** pane, select **Select**.

      1. Once all settings are properly configured in the **Assignments** page, select **Next**.

   1. In the **Review + create** page, review all settings to make sure they're all correct. Once everything is verified, select **Create** to finish creating the Cloud PC provisioning policy.
