---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 8 of 10 - Speed up the deployment process (optional)
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 8 of 10 - Speed up the deployment process (optional).
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

# Windows Autopilot deployment for existing devices: Speed up the deployment process (optional)

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
- Step 2: [Install required modules to obtain Autopilot profiles from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profiles](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)

> [!div class="checklist"]
>
> - **Step 8: Speed up the deployment process (optional)**

- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Windows Autopilot for existing devices task sequence process

When the Windows Autopilot for existing devices task sequence runs on a device, the Autopilot deployment doesn't run when the device boots into Windows for the first time during the **Setup Windows and ConfigMgr** task of the task sequence. Instead, the Autopilot deployment doesn't run until after the task sequence completes.

The Autopilot deployment normally runs when Windows boots for the first time and Windows Setup and the out-of-box experience (OOBE) run. However, during a Windows Autopilot for existing devices task sequence, even though the task sequence injected an Autopilot profile JSON file into the offline Windows installation, the file isn't processed when Windows first boots because the task sequence also creates and injects an `unattend.xml` file. When there's both an `unattend.xml` file and an Autopilot profile JSON file during Windows Setup, Windows Setup ignores the Autopilot profile JSON file, and it only processes the `unattend.xml` file.

After Windows Setup is done, the task sequence resumes and deletes the existing `unattend.xml`. Later in the task sequence when the task sequence runs Sysprep on the device, it doesn't specify or add a new `unattend.xml` file. Once the task sequence finishes running Sysprep, the task sequence completes and the device is rebooted. When the device reboots, Windows starts and Windows Setup runs for a second time. Since there's no `unattend.xml` file and only the Autopilot profile JSON file exists, Windows Setup processes the Windows Autopilot profile JSON file and the Autopilot deployment starts.

An overview of the Windows Autopilot for existing devices task sequence process is as follows:

1. Task sequence starts in Windows PE.
1. Task sequence formats and partitions the disk.
1. Task sequence applies the Windows OS and creates the `unattend.xml` file.
1. Task sequence injects the Autopilot profile JSON file.
1. Task sequence boots into Windows for the first time.
1. Windows setup runs for the first time and processes the `unattend.xml` file. Windows Autopilot profile JSON file is ignored.
1. Task sequence resumes in the newly installed Windows OS.
1. Task sequence deletes the unattend.xml file.
1. Task sequence installs the Configuration Manager client.
1. Task sequence runs additional tasks (**Install Application**, **Install Software Updates**, **Install Package**, **Enable BitLocker**, etc.)
1. Task sequence uninstalls the Configuration Manager client.
1. Task sequence Syspreps the device.
1. Task sequence completes and device reboots.
1. Windows setup runs for the second time and processes the Autopilot profile JSON file since there's no `unattend.xml` file.
1. Autopilot deployment starts.

## Additional tasks running during a Windows Autopilot for existing devices task sequence

When using the **Create Task Sequence Wizard** in Configuration Manager to create the Windows Autopilot for existing devices task sequence, it assumes that additional tasks need to be run via the task sequence before the Autopilot deployment runs. Examples of additional tasks running via the task sequence before the Autopilot deployment runs include:

- Installing applications via the **Install Application** task.
- Installing software updates via the **Install Software Updates** task.
- Installing packages via the **Install Package** task.
- Enabling BitLocker via the **Enable BitLocker** task.
- Other customizations.

In order for these additional tasks to run, the task sequence deployment process performs the following processes after it boots out of Windows PE:

- Boots into the Windows OS for the first time and runs Windows Setup and OOBE.
- Continues the task sequence in the full Windows OS.
- Installs the Configuration Manager client to support running tasks such as the **Install Application** or **Install Software Updates** tasks.
- Runs the additional tasks.
- Removes the Configuration Manager client.
- Syspreps the device so that after the task sequence completes and the device reboots, it can rerun Windows Setup and OOBE, which then launches the Autopilot deployment.

The above steps are necessary if additional tasks need to run during the task sequence. However, if additional tasks don't need to run during the task sequence, then several of the above steps aren't needed. Running the above steps when they aren't needed can potentially cause several issues including:

- Needlessly adding time to the deployment process.
- Needlessly installing the Configuration Manager client on the device. It's best practice to avoid installing the Configuration Manager client if not needed during the task sequence and if it's eventually going to be uninstalled.
- Needlessly running Windows Setup and OOBE multiple times.
- Needlessly running Sysprep.

## Speed up the deployment process

> [!TIP]
>
> If a task sequence is needed to run additional tasks before running the Autopilot deployment, then skip to the next step of [Run Autopilot task sequence on device](run-autopilot-task-sequence.md).
>
> However, even if additional tasks are needed, instead of using the task sequence to run these tasks, consider running the additional tasks using alternate methods. For example:
>
> - Install applications via Intune.
> - Enable BitLocker via Intune.
> - Install software updates via offline servicing and [Configuration Manager Scheduled Updates](/mem/configmgr/osd/get-started/manage-operating-system-images#apply-software-updates-to-an-image).
>
> When possible, Microsoft recommends using the above methods to run the additional tasks instead of running them via the task sequence. Using the above methods allows using this solution to speed up the deployment.

If no additional tasks are needed via a task sequence before running the Autopilot deployment, then the Windows Autopilot for existing devices task sequence can be modified to eliminate unneeded tasks and processes. Eliminating unneeded tasks and processes speeds up the deployment process and the time it takes for the deployment to finish. Examples of processes that can be eliminated to speed up the deployment include:

- Running Windows Setup additional times via the **Setup Windows and ConfigMgr** task.
- Installing the Configuration Manager client via the **Setup Windows and ConfigMgr**.
- Uninstalling the Configuration Manager client via the **Prepare ConfigMgr Client for Capture** task.
- Running Sysprep via the **Prepare Windows for Capture**/**Sysprep** tasks.

The solution to speed up the deployment deletes the `unattend.xml` file and eliminates the unnecessary tasks so that the Autopilot profile JSON file is processed during the first boot into Windows. After the solution is applied, the updated overview of the Windows Autopilot for existing devices task sequence process is as follows:

1. Task sequence starts in Windows PE.
1. Task sequence formats and partitions the disk.
1. Task sequence applies the Windows OS and creates the unattend.xml file.
1. Task sequence injects the Autopilot profile JSON file.
1. Task sequence deletes the `unattend.xml` file.
1. Task sequence boots into Windows for the first time.
1. Windows setup runs for the first time and processes the Autopilot profile JSON file since there's no `unattend.xml` file.
1. Autopilot deployment starts.

The solution to speed up the deployment reduces the number of steps in the deployment process from 15 to 8.

> [!NOTE]
>
> The steps for the solution to speed up the deployment are optional. The out-of-box Windows Autopilot for existing devices task sequence still works without any modification. The below steps are only designed to reduce the time it takes to run the deployment and potentially avoid some issues. If the preference is to not modify the existing Windows Autopilot for existing devices task sequence, then skip to the next step of [Run Autopilot task sequence on device](run-autopilot-task-sequence.md).

To modify the Windows Autopilot for existing devices task sequence to speed up the deployment process, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

1. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence created in the [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md) step.

1. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Edit**. Alternatively, right-click on the Autopilot for existing devices task sequence and select **Edit**.

1. In the **Task Sequence Editor** window that opens:

   1. Select the **Prepare device for Windows Autopilot** group and then select the **Remove** option in the top left of the task sequence editor. A confirmation dialog box appears confirming to delete the step. Select the **Yes** button to remove the **Prepare device for Windows Autopilot** group.

   1. Select the **Setup Operating System** group and then select the **Remove** option in the top left of the task sequence editor. A confirmation dialog box appears confirming to delete the step. Select the **Yes** button to remove the **Setup Operating System** group.

      > [!NOTE]
      >
      > If there were any additional tasks or groups after the **Setup Windows and Configuration Manager** task, then also remove those tasks and groups by selecting the **Remove** option in the top left of the task sequence editor for each one of those tasks or groups. For each removal, a confirmation dialog box appears confirming to delete the step or group. Select the **Yes** button to remove each additional task or group.

   1. Select the last task in the task sequence.

   1. Select the **Add** drop down menu in the top left of the task sequence editor and then select **General** > **Run Command Line**. A **Run Command Line** task is added as the last task in the task sequence.

   1. Select the **Run Command Line** task and then configure with the following settings:

      - **Name**: Remove unattend.xml from Panther

      - **Command Line**: Select **Copy** at the top right corner of the below **Windows Command Prompt** code block and then paste into the **Command Line** text box:

          ```cmd
          cmd.exe /c del %OSDTargetSystemDrive%\Windows\Panther\unattend.xml /s
          ```

   1. Select the **OK** button in the **Task Sequence Editor** to save the changes to the task sequence.

1. If there are multiple Windows Autopilot for existing devices task sequences, then repeat the above steps for each task sequence.

## Shut down device after the task sequence completes (optional)

When the task sequence modified to speed up the deployment process finishes running and is complete, the device restarts and then immediately boot into Windows for the first time. After booting into Windows for the first time, it will run Windows Setup and OOBE. When Windows Setup and OOBE run, the Autopilot JSON file is processed and the Autopilot deployment begins.

However, the device can be shut down instead of restarting when the task sequence completes. Shutting down the device instead of restarting it when the task sequence completes can be useful, for example,  to give the option to further prepare the device and then deliver it to an end-user. Windows Setup, OOBE, and the Autopilot deployment then instead starts when the end-user turns on the device for the first time.

If the default behavior of restarting the device when the task sequence completes is desired, then skip this section and proceed to the next step of [Run Autopilot task sequence on device](run-autopilot-task-sequence.md). Otherwise, to shut down the device instead of restarting it when the task sequence completes, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

1. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence modified in the [Speed up the deployment process](#speed-up-the-deployment-process) section.

1. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Edit**. Alternatively, right-click on the Autopilot for existing devices task sequence and select **Edit**.

1. In the **Task Sequence Editor** window that opens:

   1. Select the last task in the task sequence.

   1. Select the **Add** drop down menu in the top left of the task sequence editor and then select **General** > **Run Command Line**. A **Run Command Line** task is added as the last task in the task sequence.

   1. Select the **Run Command Line** task and then configure with the following settings:

      - **Name**: Shutdown

      - **Command Line**: Select **Copy** at the top right corner of the below **Windows Command Prompt** code block and then paste into the **Command Line** text box:

         ```cmd
         wpeutil.exe shutdown

   1. Select the **OK** button in the **Task Sequence Editor** to save the changes to the task sequence.

1. If there are multiple Windows Autopilot for existing devices task sequences, then repeat the above steps for each task sequence.

## Next step: Run Autopilot task sequence on device

> [!div class="nextstepaction"]
> [Step 9: Run Autopilot task sequence on device](run-autopilot-task-sequence.md)

## Related content

For more information on speeding up the deployment process, see the following articles:

- [Speeding up Windows Autopilot for existing devices](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices)
