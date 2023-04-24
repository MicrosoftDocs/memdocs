---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 7 of 10 - Deploy Autopilot task sequence to collection in Configuration Manager
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 7 of 10 - Deploy Autopilot task sequence to collection in Configuration Manager.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Deploy Autopilot task sequence to collection in Configuration Manager

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
> [!div class="checklist"]
> - **Step 7: Deploy Autopilot task sequence to collection in Configuration Manager**
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow)

## Deploy Autopilot task sequence to collection in Configuration Manager

Once the Autopilot for existing devices task sequence and the collection with devices to deploy the task sequence to are created, the next step is to deploy the task sequence to the collection. To deploy the task sequence to the collection, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

1. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence created in the [Create Autopilot task sequence for existing devices in Configuration Manager](create-autopilot-task-sequence.md) step.

1. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Deploy**. Alternatively, right-click on the Autopilot for existing devices task sequence and select **Deploy**.

1. In the **Deploy Software Wizard** window that appears:

   1. In the **General**/**Specify general information for this deployment** page, configure the following settings:

      1. Next to **Task Sequence:**, the Autopilot for existing devices task sequence should already be selected.

      1. Next to **Collection:**, select the **Browse** button. In the **Select Collection** window that appears, under **Select a collection:**, select the collection created in the step [Create collection in Configuration Manager](create-collection.md), and then select the **OK** button.

      1. Select the **Next >** button.

   1. In the **Deployment Settings**/**Specify settings to control this deployment** page, configure the settings as desired:

      1. For **Purpose:**, normally **Available** is selected. Making the deployment available usually means that someone such as an admin or end-user has to manually trigger and start the deployment by selecting the task sequence through methods such:

         - The Configuration Manager Software Center.
         - Booting from a PXE enabled distribution point
         - Booting from task sequence bootable media.

          > [!WARNING]
          >
          > The deployment can instead be set to **Required** which will cause the deployment to start automatically without any end-user intervention when the deployment assignment time is reached. However, it's not recommended to make a deployment required due to the potential destructive behavior that a required task sequence can have. For example, if a required task sequence is accidentally deployed to the wrong collection, or the wrong devices are added to the collection that the task sequence is deployed to, it can wipe those devices without any user interaction. If using the option of **Required**, do so with extreme caution making sure the task sequence is deployed to the correct collection that contains expected devices.

      1. Under **Make available to the following:**, select where the task sequence appears and when the task sequence can run:

         - **Only Configuration Manager clients**: The task sequence appears in the Configuration Manager Software Center on existing devices that has Windows already installed and has the Configuration Manager client installed. The task sequence doesn't appear when booting from a PXE enabled distribution point or when booting from task sequence bootable media.

         - **Only media and PXE**: The task sequence appears when booting from a PXE enabled distribution point or when booting from task sequence bootable media. The task sequence doesn't appear in the Configuration Manager Software Center on existing devices that has Windows already installed and has the Configuration Manager client installed.

         - **Configuration Manager clients, media and PXE**: The task sequence appears when booting from a PXE enabled distribution point or when booting from task sequence bootable media, and it also appears in the Configuration Manager Software Center on existing devices that has Windows already installed and has the Configuration Manager client installed.

          > [!WARNING]
          >
          > When the deployment is set to **Required**, the above options are the scenarios when the deployment can automatically run when the deployment assignment time is reached. For example, if the deployment is set to **Required** and **Only media and PXE**, the task sequence won't ever run automatically while in Windows. However, it will run automatically when the device is booted from a PXE enabled distribution point or when booted from task sequence bootable media.

      1. Select the **Next >** button.

   1. In the **Scheduling**/**Specify the schedule for this deployment** page, schedule when the deployment should occur:

      1. Select the checkbox next to **Schedule when this deployment will become available:** and then select a date and time. This date and time is the date and time that the task sequence starts to appear in the Configuration Manager Software Center, when booting from a PXE enabled distribution point, or when booting from task sequence bootable media.

      1. If the deployment is required, next to **Assignment schedule:**, select the **New** button. In the **Assignment Schedule** window that appears, configure the settings as needed. The settings selected here determine when the task sequence runs automatically without end-user intervention. Once complete. Once complete, select the **OK** button.

      1. Select the **Next >** button.

   1. In the **User Experience**/**Specify the user experience for the installation of this software** page, select the options as desired, and then select the **Next >** button.

   1. In the **Alerts**/**Specify Configuration Manager and Operations Manager** page, select the options as desired, and then select the **Next >** button.

   1. In the **Distribution Points**/**Specify how to run the content for this program** page, select the options as desired, and then select the **Next >** button.

   1. In the **Summary**/**Confirm the settings for this new deployment** page, verify that everything is configured as desired, and then select the **Next >** button.

   1. When the **Deploy Software Wizard** completes with **The task "Deploy Software Wizard" completed successfully** message, select the **Close** button.

1. If there are multiple task sequences with different Autopilot profiles, repeat the above steps for each task sequence.

> [!NOTE]
>
> The instructions in this step doesn't fully go into detail all of the options available when running the **Deploy Software Wizard**. For full details on the options available, see [Deploy a task sequence](/mem/configmgr/osd/deploy-use/deploy-a-task-sequence).

## Next step: Speed up the deployment process (optional)

> [!div class="nextstepaction"]
> [Step 8: Speed up the deployment process (optional)](speed-up-deployment.md)

If you rather use an unmodified out of box Autopilot task sequence created by the **Create Task Sequence Wizard** in Configuration Manager, then skip to [Step 9: Run Autopilot task sequence on device](run-autopilot-task-sequence.md).

> [!div class="nextstepaction"]
> [Step 9: Run Autopilot task sequence on device](run-autopilot-task-sequence.md)

## More information

For more information on deploying the Autopilot task sequence, see the following article(s):

- [Deploy the Autopilot task sequence](/mem/autopilot/existing-devices#deploy-the-autopilot-task-sequence)
- [Deploy a task sequence](/mem/configmgr/osd/deploy-use/deploy-a-task-sequence)
