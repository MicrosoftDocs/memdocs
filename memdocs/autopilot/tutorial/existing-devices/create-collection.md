---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 6 of 10 - Create collection in Configuration Manager
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 6 of 10 - Create collection in Configuration Manager.
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

# Windows Autopilot deployment for existing devices: Create collection in Configuration Manager

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
> [!div class="checklist"]
> - **Step 6: Create collection in Configuration Manager**
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow)

## Create collection in Configuration Manager

Once the Autopilot for existing devices task sequence has been created, the next step is to create a collection in Configuration Manager to deploy the task sequence to the target devices.

> [!NOTE]
>
> If a collection with the desired devices to target already exists, then this step can be skipped. Proceed to the step [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md).

To create the Autopilot for existing devices task sequence in Configuration Manager, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Assets and Compliance** > **Overview**.

1. Select **Device Collections**.

1. In the ribbon, select **Create**, and then select **Create Device Collection**. As an alternative, right-click on **Device Collections**, and then select **Create Device Collection**.

1. In the **Create Device Collection Wizard** window that appears:

   1. In the **Specify details for this collection** page, configure the following settings:

      1. Next to **Name:**, enter a desired name for the collection. For example, **Autopilot for existing devices**.

      1. Next to **Comment:**, if desired, add an optional comment to further describe the collection

      1. Next to **Limiting collection:**, select the **Browse** button. In the **Select Collection** window that appears, select a desired collection to limit this collection to. To not limit this collection, select the **All Systems** collection. Once the desired collection is selected, select the **OK** button.

      1. Select the **Next >** button.

   1. In the **Define membership rules for this collection** page, via the **Add Rule** drop-down menu, create a rule(s) that includes the desired devices to run the Autopilot for existing devices task sequence. For more information on creating rules for a collection to include the desired devices, see [How to create collections in Configuration Manager](/mem/configmgr/core/clients/manage/collections/create-collections). Once the appropriate rules have been created that include the desired devices, select the **Next >** button.

   1. In the **Confirm the settings** page, verify that everything is configured as desired, and then select the **Next >** button.

   1. When the **Create Device Collection Wizard** completes with **The task "Create Device Collection Wizard" completed successfully** message, select the **Close** button.

1. With **Device Collections** still selected, select <kbd>F5</kbd> on the keyboard to refresh the list of collections in the right pane. Verify that the newly created collection appears. If it doesn't appear, wait a few minutes, and then try to refresh again. Depending on the environment, it may take some time for the newly created collection to appear.

1. Once the newly created collection appears, open it by double-clicking on it. Alternatively, to open the collection, right-click on the collection and then select **Show Members**. The members of the collection appear in the right pane.

1. Verify that the listed devices are the expected devices for the collection that should receive the Autopilot for existing devices task sequence.

## Next step: Deploy Autopilot task sequence to collection in Configuration Manager

> [!div class="nextstepaction"]
> [Step 7: Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)

## More information

For more information on creating a collection in Configuration Manager, see the following article(s):

- [Deploy the Autopilot task sequence](/mem/autopilot/existing-devices#deploy-the-autopilot-task-sequence)
- [How to create collections in Configuration Manager](/mem/configmgr/core/clients/manage/collections/create-collections)
