---
title: Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 5 of 6 - Create a Cloud PC provisioning policy
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 (preview) - Step 5 of 6 - Create a Cloud PC provisioning policy.
ms.date: 06/11/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365 (preview): Create a Cloud PC provisioning policy

Windows Autopilot device preparation in automatic mode for Windows 365 steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
- Step 2: [Create an assigned device group](automatic-device-group.md)
- Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 4: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)

> [!div class="checklist"]
>
> - **Step 5: Create a Cloud PC provisioning policy**

- Step 6: [Monitor the deployment](automatic-monitor.md)

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 overview](automatic-workflow.md#workflow).

## Create a Cloud PC provisioning policy for use with Windows Autopilot device preparation in automatic mode for Windows 365

To create a Cloud PC provisioning policy for use with Windows Autopilot device preparation in automatic mode for Windows 365, follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **Device onboarding**, select **Windows 365**.

1. At the top of the **Devices | Windows 365** screen, select **Provisioning policies**, and then select **Create policy**.

1. In the **Create a provisioning policy** screen:

   1. In the **General** page:

      1. In the **Name** text box, enter a name for the Windows 365 Cloud PC policy.

      1. In the **Description** text box, if desired, enter a description for the Windows 365 Cloud PC policy.

      1. Next to **Experience**, select **Access a full Cloud PC desktop**.

      1. Next to **License type**, select **Frontline**.

      1. Next to **Frontline type**, select **Shared**.

      1. Under the **Join type details** section:

         1. Next to **Join type**, make sure **Microsoft Entra Join** is selected.

         1. Next to **Network**, make sure **Microsoft hosted network** is selected.

         1. Next to **Geography** and **Region**, make sure the appropriate geography and region settings are set as desired using the drop-down menus.

         1. If desired, select the option **Use Microsoft Entra single sign-on** to enable it. This option allows the use of a single prompt to authenticate users for Windows 365 and their Cloud PC.

      1. Once all settings are properly configured in the **General** page, select **Next**.

   1. In the **Image** page, make sure a [supported version of Windows](../../requirements.md#windows-365-cloud-pcs) is selected.

       - To change to a different version of Windows, select the **Change** or **Change selected image** link, select a [supported version of Windows](../../requirements.md#windows-365-cloud-pcs) from the **Select an image** pane, and then select **Select**.

           > [!TIP]
           >
           > The Windows images in the image gallery are updated with the latest updates already installed.

       - To use a custom image, use the drop-down menu to select **Custom image**, select a custom image with a [supported version of Windows](../../requirements.md#windows-365-cloud-pcs) from the **Select an image** pane, and then select **Select**. For more information on custom images, see [Device images overview](/windows-365/enterprise/device-images).

      Once the desired Windows image is selected, select **Next**.

   1. In the **Configuration** page:

      1. Next to **Language & Region** under **Windows Settings**, select the desired language and region setting using the drop-down menu.

      1. If unique names for Cloud PCs are desired, select **Apply device name template** under **Cloud PC naming**, and then follow the instructions to create a name template.

      1. Under **Windows Autopilot (Preview)**:

         1. Next to **Autopilot Device preparation policy**, use the drop-down menu to select the automatic Windows Autopilot device preparation policy created in [Step 4: Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md).

         1. Next to **Minutes allowed before device preparation fails**, enter a value between 10 - 360 minutes that allows adequate time to install the apps and scripts defined in the Windows Autopilot device preparation policy. For example, enter **60** for 60 minutes. The recommended minimum value should be no lower than 30. If the apps and scripts aren't finished installing by the time specified, the device preparation fails.

         1. To prevent users from connecting to the Cloud PC if the deployment fails or times out, select the option **Prevent users from connection to Cloud PC upon installation failure or timeout**. When this option is checked, deployments that fail are marked as **Failed**. For more information, see the next step [Step 6: Monitor the deployment - View status of the deployment](automatic-monitor.md#view-status-of-the-deployment).

         To allow users to connect to the Cloud PC even when the deployment fails or times out, leave the option **Prevent users from connection to Cloud PC upon installation failure or timeout** unchecked. When this option is unchecked, deployments that fail are marked as **Provisioned with warnings**. For more information, see the next step [Step 6: Monitor the deployment - View status of the deployment](automatic-monitor.md#view-status-of-the-deployment).

      1. Once all settings are properly configured in the **Configuration** page, select **Next**.

   1. In the **Scope tags** page, select **Next**.

      > [!NOTE]
      >
      > **Scope tags** are optional. For this tutorial, scope tags are being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune-service/fundamentals/scope-tags).

   1. In the **Assignments** page:
   
      1. Select **Add groups**. The **Select groups to include** pane opens. In the **Select groups to include** pane:
      
         1. In the **Search** text box, enter the name of the user group the policy will be assigned to.
                  
         1. Once the device group is found, select it under **Name**.

         1. Select the **Select** button.

      1. Next to the selected device group, select the **Select one** link under **Cloud PC size**. The **Select Cloud PC size** pane opens. In the **Select Cloud PC size** pane:

         1. In the **Available Cloud PCs** drop down menu under the **Cloud PC size** section, select the desired Cloud PC configuration. For more information, see [Cloud PC size recommendations](/windows-365/enterprise/cloud-pc-size-recommendations).

         1. Under the **Assignment** section:

            1. In the **Name** text box, enter a name for the assignment.

            1. In the **Remaining Cloud PCs** text box, enter the desired number between 0 - 900 of Cloud PCs that should be provisioned. The number of available Cloud PC licenses is displayed next **Remaining Cloud PCs** and it decrements based on the number entered in the **Remaining Cloud PCs** text box.

         1. Once everything is configured as desired in the **Select Cloud PC size** pane, select **Select**.

      1. Once all settings are properly configured in the **Assignments** page, select **Next**.

   1. In the **Review + create** page, review all settings to make sure they're all correct. Once everything is verified, select **Create** to finish creating the Cloud PC provisioning policy.

## Next step: Monitor the deployment

> [!div class="nextstepaction"]
> [Step 6: Monitor the deployment](automatic-monitor.md)
