---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 8 of 10 - Speed up the deployment process (optional)
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 8 of 10 - Speed up the deployment process (optional).
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/11/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Speed up the deployment process (optional)

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
- Step 5: [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md)
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
> [!div class="checklist"]
> - **Step 8: Speed up the deployment process (optional)**
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md)

## Windows Autopilot for existing devices task sequence process

When using the **Create Task Sequence Wizard** in Configuration Manager to create the Windows Autopilot for existing devices task sequence, it assumes that additional tasks need to be run via the task sequence before the Autopilot deployment runs. Examples of additional tasks running via a task sequence before the Autopilot deployment runs include:

- Installing applications via the **Install Application** task.
- Installing software updates via the **Install Software Updates** task.
- Installing packages via the **Install Package** task.
- Enabling BitLocker via the **Enable BitLocker** task.
- Other customizations.

In order for these tasks to run, the task sequence deployment process performs the following tasks:

- Boots into the Windows OS and runs Windows Setup and OOBE.
- Continues the task sequence in the full OS.
- Installs the Configuration Manager client to support running tasks such as the **Install Application** or **Install Software Updates** tasks.
- Runs the additional tasks.
- Removes the Configuration Manager client.
- Syspreps the device so that after the task sequence completes and the device reboots, it can rerun Windows Setup and OOBE which then launches the Autopilot deployment.

All of the above steps are necessary if additional tasks are needed. However, if the additional tasks are not needed, then these tasks can potentially cause several issues including:

- Needlessly adding a lot of time to the deployment process.
- Needlessly installing the Configuration Manager client on the device - it's best practice to avoid installing the Configuration Manager client in the first place if it's eventually going to be uninstalled.
- Needlessly running Windows Setup and OOBE multiple times.
- Needlessly running Sysprep.

### When does the Autopilot deployment run during a Windows Autopilot for existing devices task sequence

When the Windows Autopilot for existing devices task sequence runs on a device, the Autopilot deployment doesn't run when the device first boots into Windows during the **Setup Windows and ConfigMgr** task. The Autopilot deployment would normally run during this time frame when Windows Setup and OOBE run. However, even though the task sequence injected the Autopilot profile JSON file into the offline Windows installation, the file is not processed because the task sequence also creates and injects an `unattend.xml` file. When there is both an `unattend.xml` and an Autopilot profile JSON file during Windows Setup and OOBE, the Autopilot profile JSON file is ignored by Windows Setup and only the `unattend.xml` file is processed.

The Autopilot deployment will run instead when Windows Setup and OOBE run for the second time after the task sequence Syspreps the device and the task sequence completes. During the **Setup Windows and ConfigMgr** task, the task sequence deletes the existing `unattend.xml` after it has been processed by Windows Setup. When the task sequence later Syspreps the device, it doesn't specify or add a new `unattend.xml` file. When the device reboots after the task sequence completes, there is no `unattend.xml` file and only the Autopilot profile JSON file exists, so therefore the Autopilot deployment starts.

## Speed up the deployment process

If a task sequence is needed to run additional tasks are needed before running the Autopilot deployment, the skip to the next step of [Run Autopilot task sequence on device](run-autopilot-task-sequence.md).

> [!TIP]
>
> Even if additional tasks are needed, instead of using the task sequence to run these tasks, consider running the additional tasks using alternate methods. For example:
>
> - Install applications via Intune.
> - Enable BitLocker via Intune.
> - Install software updates via offline servicing and [Configuration Manager Scheduled Updates](/mem/configmgr/osd/get-started/manage-operating-system-images#apply-software-updates-to-an-image).
>
> Microsoft recommends using the above methods to run the additional tasks instead of running them via the task sequence. Using the above methods will allow you to use the below steps to speed up the deployment.

If no additional tasks are needed via a task sequence before running the Autopilot deployment, to speed up the deployment, the Windows Autopilot for existing devices task sequence can be modified to eliminate tasks and processes that aren't needed. Examples of processes that can be eliminated to speed up the deployment include running Windows Setup an extra time and installing the Configuration Manager client via the **Setup Windows and ConfigMgr** task, uninstalling the Configuration Manager client via the **Prepare ConfigMgr Client for Capture** task, and running Sysprep via the **Prepare Windows for Capture**/**Sysprep** tasks. In addition, the `unattend.xml` file created by the task sequence needs to be deleted so that the Autopilot profile JSON file is processed by Windows Setup instead of the `unattend.xml` file.

The below solution deletes the `unattend.xml` file and eliminates the unnecessary tasks so that the Autopilot profile JSON file is processed during the first boot into Windows.

> [!NOTE]
>
> The below steps to speed up the deployment are optional. The out of box Windows Autopilot for existing devices task sequence will still work without any modification. The below steps are only designed to reduce the time it takes to run the deployment and potentially avoid some issues. If you don't want to modify the existing Windows Autopilot for existing devices task sequence, then skip to the next step of [Run Autopilot task sequence on device](run-autopilot-task-sequence.md).

To modify the Windows Autopilot for existing devices task sequence to speed up the deployment process, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

2. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

3. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence created in the [Create Autopilot task sequence in Configuration Manager](create-autopilot-task-sequence.md) step.

4. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Edit**. Alternatively, right-click on the the Autopilot for existing devices task sequence and select **Edit**.

5. In the **Task Sequence Editor** window that opens:

   1. Select the **Prepare device for Windows Autopilot** group and then select the **Remove** option in the top left of the task sequence editor. A confirmation dialog box will appear confirming to delete the step. Select the **Yes** button to remove the **Prepare device for Windows Autopilot** group.

   2. Select the **Setup Operating System** group and then select the **Remove** option in the top left of the task sequence editor. A confirmation dialog box will appear confirming to delete the step. Select the **Yes** button to remove the **Setup Operating System** group.

      > [!NOTE]
      >
      > If there were any additional tasks or groups after the **Setup Windows and Configuration Manager** task, then also remove those tasks and groups by selecting the **Remove** option in the top left of the task sequence editor for each one of those task or group. For each removal, a confirmation dialog box will appear confirming to delete the step or group. Select the **Yes** button to remove each additional task or group.

   3. Select the last task in the task sequence.

   4. Select the **Add** drop down menu in the top left of the task sequence editor and then select **General** > **Run Command Line**. This will add a **Run Command Line** task as the last task in the task sequence.

   5. Select the **Run Command Line** task and then configure with the following settings:

      - **Name**: Remove unattend.xml from Panther

      - **Command Line**: Select **Copy** at the top right corner of the below **Windows Command Prompt** code block and then paste into the **Command Line** text box:

          ```cmd
          cmd.exe /c del %OSDTargetSystemDrive%\Windows\Panther\unattend.xml /s
          ```

   6. Select the **OK** button in the **Task Sequence Editor** to save the changes to the task sequence.

6. If there are multiple Windows Autopilot for existing devices task sequences, then repeat the above steps for each task sequence.

## Shut down device after the task sequence completes

When the modified task sequence designed to speed up the deployment process finishes running and is complete, the device will restart and then immediately boot into Windows for the first time where it will run Windows Setup and OOBE. When Windows Setup and OOBE runs, the Autopilot JSON file will be processed and the Autopilot deployment will start. However, if it's preferred to have the device shut down instead of restarting when the task sequence completes, for example to give the option to further prepare the device and then deliver it to an end-user, the device can be shut down instead of restarting when the task sequence completes. Windows Setup, OOBE, and the Autopilot deployment will then start when the end-user turns on the device for the first time.

If a restart of the device is desired instead of shutting it down when the task sequence completes, then proceed to the next step of [Run Autopilot task sequence on device](run-autopilot-task-sequence.md). Otherwise, to shut down the device instead of restarting it when the task sequence completes, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

1. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence modified in the [Speed up the deployment process](#speed-up-the-deployment-process) section.

1. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Edit**. Alternatively, right-click on the the Autopilot for existing devices task sequence and select **Edit**.

1. In the **Task Sequence Editor** window that opens:

   1. Select the last task in the task sequence.

   1. Select the **Add** drop down menu in the top left of the task sequence editor and then select **General** > **Run Command Line**. This will add a **Run Command Line** task as the last task in the task sequence.

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

## More information

For more information on speeding up the deployment process, see the following article(s):

- [Speeding up Windows Autopilot for existing devices](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices)