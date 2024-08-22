---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 5 of 10 - Create Autopilot task sequence in Configuration Manager
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 5 of 10 - Create Autopilot task sequence in Configuration Manager.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/27/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices: Create Autopilot task sequence in Configuration Manager

Autopilot user-driven Microsoft Entra join steps:

- Step 1: [Set up a Windows Autopilot profile](setup-autopilot-profile.md)
- Step 2: [Install required modules to obtain Autopilot profiles from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profiles](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)

> [!div class="checklist"]
>
> - **Step 5: Create Autopilot task sequence in Configuration Manager**

- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md#workflow).

## Create Autopilot task sequence for existing devices in Configuration Manager

Once the packages containing the Autopilot profile JSON files are created and distributed in Configuration Manager, the next step is to create a task sequence that performs the following functions:

- Wipes the device.
- Installs a fresh copy of Windows on the device.
- Copies the Autopilot profile JSON file to the device.

Copying of the Autopilot profile JSON file is done in WinPE when the newly installed Windows OS is offline. When the task sequence completes, the device boots into the newly installed Windows OS for the first time and runs the out-of-box experience (OOBE). The OOBE process then processes the Autopilot profile JSON file, which initiates the Autopilot deployment.

> [!NOTE]
>
> If using multiple Autopilot profiles and multiple Autopilot profile JSON files were created, a separate task sequence is needed for each of the Autopilot profiles.

To create the Autopilot for existing devices task sequence in Configuration Manager, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

1. Select **Task Sequences** and then on the ribbon, select **Create Task Sequence**. Alternatively, right-click **Task Sequences** and select **Create Task Sequence**.

1. The **Create Task Sequence Wizard** window appears:

   1. In the **Create new task sequence** page, select the option to **Deploy Windows Autopilot for existing devices**, and then select the **Next >** button.

   1. In the **Specify task sequence information** page:

      1. Next to **Name**, enter an identifiable name for the Autopilot scenario for the task sequence. For example, **Autopilot user-driven Microsoft Entra join**.

      1. Next to **Description**, enter a description for the Autopilot scenario for the task sequence.

      1. Next to **Boot image:**, select the **Browse** button.

         - In the **Select a Boot Image** windows that appears, under **Boot images:**, select a boot image, and then select the **OK** button.

      1. Select the **Next >** button.

   1. In the **Install the Windows operating system** page:

      1. Next to **Image package:**, select the **Browse** button. In the **Select an Operating System Image** window that appears, under **Operating system images:**, locate and select the desired Windows operating system image, and then select the **OK** button.

      1. Next to **Image index:**, select the desired Windows version. For example, **Enterprise**.

      1. Make sure the option **Partition and format the target computer before installing the operating system** is selected and enabled.

      1. Make sure the option **Configure task sequence for use with BitLocker** isn't selected. If BitLocker encryption is desired, Microsoft recommends enabling via Intune policies that are applied during the Windows Autopilot deployment.

          > [!NOTE]
          >
          > Although BitLocker encryption could technically be enabled via the task sequence, it might result in undesired outcomes. For example, instead of saving BitLocker recovery keys to Intune or Microsoft Entra ID, they might be saved to:
          >
          > - Configuration Manager BitLocker Management.
          > - On-premises Active Directory.
          >
          > Additionally, if BitLocker settings specified in the task sequence don't match the BitLocker policy settings in Intune, then this mis-match could cause the device to show as non-compliant. Resolving issues like this could mean having to decrypt and then re-encrypt the drive to resolve. Therefore Microsoft recommends not enabling BitLocker as part of the task sequence and instead enabling BitLocker as part of Intune policies deployed during Windows Autopilot.

      1. Leave **Product key** blank. The Autopilot for existing devices task sequence runs the [Windows System Preparation Tool (Sysprep)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview) at the end of the task sequence. Sysprep clears any product key that is specified.

      1. Leave the option of **Randomly generate the local administrator password and disable the account on all support platforms (recommended)** selected. Alternatively, the option of **Enable the account and specify the local administrator password** can be selected and a password specified. However, the password specified will only be useful after the **Setup Windows and ConfigMgr** task and if the task sequence fails and doesn't complete successfully. If the task sequence completes successfully, the password is cleared at the end of the task sequence by Sysprep.

      1. Once all options are configured in the **Install the Windows operating system** page, select the **Next >** button.

      > [!NOTE]
      >
      > If using the alternate [Speed up the deployment process (optional)](speed-up-deployment.md) step later in this tutorial, Sysprep never runs as part of the task sequence. However, the product key and local administrator password never get processed since the `unattend.xml` file that contains the product key and local administrator password is deleted as part of this optional step. For this reason, when using the alternate [Speed up the deployment process (optional)](speed-up-deployment.md) step, the settings specified for these two options are irrelevant since they're never processed.

   1. In the **Install the Configuration Manager client** page, add any necessary Configuration Manager client installation properties for the environment. For example, since the device is a Workgroup device and not domain joined during the Windows Autopilot for existing devices task sequence, the [SMSMP](/mem/configmgr/core/clients/deploy/about-client-installation-properties#smsmp) or [SMSMPLIST](/mem/configmgr/core/clients/deploy/about-client-installation-properties#smsmplist) parameters might be needed to run certain tasks such as the **Install Application** or **Install Software Updates** tasks. Once finished adding any Configuration Manager client installation properties, select the **Next >** button.

   1. In the **Install software updates** page, select the desired option to install software updates during the task sequence. For the  Autopilot for existing devices task sequence, Microsoft recommends leaving the option to the default of **Do not install any software updates** and not install any software updates during the task sequence. Once the desired option is selected, select the **Next >** button.

      > [!TIP]
      >
      > Microsoft recommends not installing software updates during the Autopilot for existing devices task sequence because doing so significantly increases the time for the task sequence to complete. Instead, consider installing updates using one of the following two options:
      >
      > - The Configuration Manager offline image servicing feature of [Scheduled Updates](/mem/configmgr/osd/get-started/manage-operating-system-images#apply-software-updates-to-an-image)
      > - Every month, download the latest monthly ISO for the version of Windows that's being installing and then update the **Operating System Images** package in Configuration Manager with the new updated `install.wim` image from the ISO. The ISOs are updated monthly and have the latest updates in them.

   1. In the **Install applications** page, select the desired applications to install during the task sequence. Once the desired applications are added, select the **Next >** button. If no applications need to be installed, then select the **Next >** button without selecting any applications.

      > [!TIP]
      >
      > Instead of installing applications during the task sequence, Microsoft recommends installing all applications and configurations from Microsoft Intune or Configuration Manager co-management. This process provides a consistent experience between users receiving new devices and those using Windows Autopilot for existing devices.

   1. On the **Prepare System for Windows Autopilot** page, select the package that includes the Autopilot JSON file created in the step [Create and distribute package for JSON file in Configuration Manager](create-json-package.md). Once the package with the Autopilot JSON file is selected, select the **Next >** button.

      > [!NOTE]
      >
      > Leave the option **Shutdown computer after this task sequence completes** unchecked. This option is configured later in the section [Modify the task sequence to account for Sysprep command line configuration](#modify-the-task-sequence-to-account-for-sysprep-command-line-configuration).

   1. On the **Confirm the settings** page, verify that all settings are correct, and then select the **Next >** button.

   1. When the **Create Task Sequence Wizard** completes with **The task "Create Task Sequence Wizard" completed successfully** message, select the **Close** button.

1. If using multiple Autopilot profiles and multiple Autopilot profile JSON files were created, repeat the above steps to create additional task sequences. Each Autopilot profile JSON file needs its own separate task sequence.

> [!NOTE]
>
> For Windows Autopilot for existing devices task sequence, the **Create Task Sequence Wizard** purposely skips configuring and adding the **Apply Network Settings** task. If the **Apply Network Settings** task isn't specified in a task sequence, it uses Windows default behavior, which is to join a workgroup.
>
> The Windows Autopilot for existing devices task sequence runs the **Prepare Windows for capture** step, which uses the Windows System Preparation Tool (Sysprep). If the device is joined to a domain, Sysprep fails, so therefore the Windows Autopilot for existing devices task sequence joins a workgroup. For this reason, it isn't necessary to add the **Apply Network Settings** task to a Windows Autopilot for existing devices task sequence.

## Modify the task sequence to account for Sysprep command line configuration

The Autopilot for existing devices task sequence adds the **Prepare Windows for Capture** task to the task sequence. The **Prepare Windows for Capture** task is the task that runs Sysprep. Sysprep needs to run so that on the next boot, OOBE runs and processes the Autopilot profile JSON file. However, the **Prepare Windows for Capture** task adds the `/Generalize` parameter to the Sysprep command line. The `/Generalize` parameter causes Sysprep to delete the Autopilot profile JSON file. The `/Generalize` parameter for Sysprep is normal for traditional build and capture task sequences not associated with Autopilot, but it breaks Autopilot deployments since the Autopilot profile JSON file is deleted. Deletion of the Autopilot profile JSON file causes Autopilot to never run during Windows Setup and OOBE.

To resolve the issue, the **Prepare Windows for Capture** task needs to be removed from the task sequence and replaced with a **Run Command Line** task that runs Sysprep without the `/Generalize` parameter. This resolution can be accomplished by following these steps:

> [!NOTE]
>
> If the optional step of [Speed up the deployment process (optional)](speed-up-deployment.md) is going to be followed, then skip this section and proceed to the next step of [Step 6: Create collection in Configuration Manager](create-collection.md).

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems**.

1. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence created in the [Create Autopilot task sequence for existing devices in Configuration Manager](#create-autopilot-task-sequence-for-existing-devices-in-configuration-manager) section.

1. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Edit**. Alternatively, right-click on the Autopilot for existing devices task sequence and select **Edit**.

1. In the **Task Sequence Editor** window that opens:

   1. Select the **Prepare Windows for Capture** task.

   1. Select the **Add** drop down menu in the top left of the task sequence editor and then select **General** > **Run Command Line**. A **Run Command Line** task is added immediately after the **Prepare Windows for Capture** task.

   1. Select the **Run Command Line** task and then configure with the following settings:

      - **Name**: Sysprep

      - **Command Line**: Based on the desired behavior, select one of the following two Sysprep command lines by selecting **Copy** at the top right corner of the desired **Windows Command Prompt** code block and then pasting the copied Sysprep command line into the **Command Line** text box:

        - Restart device after running Sysprep. OOBE and that Autopilot deployment will start immediately after the task sequence completes and the device restarts:

          ```cmd
          C:\Windows\System32\Sysprep\Sysprep.exe /oobe /reboot
          ```

        - Shut down device after running Sysprep. After the device shuts down, OOBE and the Autopilot deployment won't start until the device is turned on for the first time by the end-user:

          ```cmd
          C:\Windows\System32\Sysprep\Sysprep.exe /oobe /shutdown
          ```

      > [!NOTE]
      >
      > Sysprep can either shut down or restart the device when it finishes running:
      >
      > - **Restarting** the device causes the device to restart as soon as the task sequence completes and then immediately boots into Windows for the first time and runs Windows Setup and OOBE. When Windows Setup and OOBE run, the Autopilot JSON file is processed and the Autopilot deployment starts.
      >
      > - **Shutting down** the device shuts down and powers off the device as soon as the task sequence completes. Shutting down and powering off the device give the option to further prepare the device and then deliver it to an end-user. Windows Setup, OOBE, and the Autopilot deployment then start when the end-user turns on the device for the first time.

   1. Select the **Prepare Windows for Capture** task again and then select the **Remove** option in the top left of the task sequence editor. A confirmation dialog box appears confirming to delete the step. Select the **Yes** button to remove the **Prepare Windows for Capture** task.

   1. Select the **OK** button in the **Task Sequence Editor** to save the changes to the task sequence.

## Next step: Create collection in Configuration Manager

> [!div class="nextstepaction"]
> [Step 6: Create collection in Configuration Manager](create-collection.md)

## Related content

For more information on creating an Autopilot task sequence in Configuration Manager, see the following articles:

- [Create a task sequence](../../existing-devices.md#create-a-task-sequence).
- [Windows System Preparation Tool (Sysprep)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview).
- [Windows Autopilot for existing devices doesn't work](../../known-issues.md#windows-autopilot-for-existing-devices-doesnt-work).
