---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 4 of 10 - Create and distribute package for JSON file in Configuration Manager
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 4 of 10 - Create and distribute package for JSON file in Configuration Manager.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Create and distribute package for JSON file in Configuration Manager

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
- Step 2: [Install required modules to obtain Autopilot profiles from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profiles](create-json-file.md)

> [!div class="checklist"]
>
> - **Step 4: Create and distribute package for JSON file in Configuration Manager**

- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Create packages for JSON files in Configuration Manager

Once the JSON files are created for the Autopilot profiles, a package needs to be created in Configuration Manager that contains the contents of the JSON files.

> [!IMPORTANT]
>
> The JSON files used by Windows Autopilot deployment for existing devices only support [Windows Autopilot user-driven Microsoft Entra join](../user-driven/azure-ad-join-workflow.md) and [Windows Autopilot user-driven Microsoft Entra hybrid join](../user-driven/hybrid-azure-ad-join-workflow.md) Autopilot profiles. When creating the packages for JSON files in Configuration Manager, make sure the JSON files are only for user-driven Microsoft Entra join and user-driven Microsoft Entra hybrid join Autopilot profiles.

To create a package containing the JSON file in Configuration Manager, follow these steps:

1. Copy the folders containing the JSON files created in the [Create JSON file for Autopilot profiles](create-json-file.md) step to a new empty folder in the organization's UNC network path. The UNC network path should be the path that contains package sources for Configuration Manager packages.

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Application Management**.

1. Select **Packages** and then on the ribbon, select **Create Package**. Alternatively, right-click **Packages** and select **Create Package**.

1. The **Create Package and Program Wizard** window appears:

   1. In the **Specify information about this package** page, enter the following details for the package:

      1. Next to **Name**, enter an identifiable name for the Autopilot scenario that the JSON file is for.

      1. Next to **Description**, enter a description for the Autopilot scenario that the JSON file is for.

      1. Select the checkbox **This package contains source files**, and then select **Browse** next to **Source folder:**.

      1. The **Set Source Folder** window appears. In the **Set Source Folder** window:

         1. Select **Browse** and navigate to the folder containing the individual **`AutopilotConfigurationFile.json`** JSON file from the UNC path in Step 1.

         1. Once in the folder containing the **`AutopilotConfigurationFile.json`** JSON file, select **Select Folder**.

         1. Confirm the path under **Source folder** is correct, and then select **OK**.

            > [!IMPORTANT]
            >
            > If multiple Autopilot profiles were copied to a UNC network path, make sure to select the folder that contains the individual  **`AutopilotConfigurationFile.json`** JSON file and not the parent folder that contains all of the different Autopilot profiles. Each Autopilot JSON file requires an individual package in Configuration Manager.

   1. Select the **Next >** button.

   1. In the **Choose the program type that you want to create** page, select the **Do not create a program** option, and then select the **Next >** button.

   1. In the **Confirm the settings** page, verify all settings are correct, and then select the **Next >** button.

   1. When the **Create Package and Program Wizard** completes with **The task "Create Package and Program Wizard" completed successfully** message, select the **Close** button.

1. If there are multiple Autopilot JSON files, repeat the above steps for any additional supported Autopilot profile JSON files that were exported as part of the [Create JSON file for Autopilot profiles](create-json-file.md) step. Make sure that each package has a unique identifiable name.

## Distribute packages for JSON files in Configuration Manager

Once the package containing the Autopilot profile JSON file is created, the package needs to be distributed to Configuration Manager distribution points. To distribute the package containing the Autopilot profile JSON file in Configuration Manager, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Application Management**.

1. Expand **Packages** and locate the Autopilot profile JSON packages created in the section [Create packages for JSON files in Configuration Manager](#create-packages-for-json-files-in-configuration-manager).

1. Select the Autopilot profile JSON package and in the ribbon select **Distribute Content**. As an alternative, right-click the Autopilot profile JSON package and select **Distribute Content**.

1. The **Distribute Content Wizard** appears:

   1. In the **Review selected content** page, verify the correct package is selected and then select the **Next >** button.

   1. In the **Specify the content destination** page, select **Add**, and then select either **Distribution Point** or **Distribution Point Group**.

      - The **Add Distribution Points** or **Add Distribution Point Groups** window appears. Select the desired distribution points or distribution point groups to distribute the package to and then select **OK**.

   1. Select the **Next >** button.

   1. In the **Confirm the settings** page, verify all settings are correct, and then select the **Next >** button.

   1. When the **Distribute Content Wizard** completes with **The task "Distribute Content Wizard" completed successfully** message, select the **Close** button.

1. With the package still selected under **Packages**, in the lower pane of the Configuration Manager console under **Related Objects**, select **Content Status** .

1. Monitor the distribution of the package until it successfully distributes to all distribution points. For details of the distribution status to each distribution point, under **Completion Statistics** in the lower pane of the Configuration Manager console, select the **View Status** option.

1. If there are multiple Autopilot JSON file packages, repeat the above steps for any additional Autopilot profile JSON file packages created in the section [Create packages for JSON files in Configuration Manager](#create-packages-for-json-files-in-configuration-manager).

## Next step: Create Autopilot task sequence in Configuration Manager

> [!div class="nextstepaction"]
> [Step 5: Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)

## Related content

For more information on creating and distributing the JSON package in Configuration Manager, see the following articles:

- [Create a package containing the JSON file](../../existing-devices.md#create-a-package-containing-the-json-file).
- [Packages and programs in Configuration Manager](/mem/configmgr/apps/deploy-use/packages-and-programs).
- [Distribute content to distribution points](../../existing-devices.md#distribute-content-to-distribution-points).
