---
title: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 5 of 10 - Create Autopilot task sequence in Configuration Manager
description: Windows Autopilot deployment for existing devices in Intune and Configuration Manager - Step 5 of 10 - Create Autopilot task sequence in Configuration Manager.
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

# Windows Autopilot deployment for existing devices: Create Autopilot task sequence in Configuration Manager

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up a Windows Autopilot deployment](setup-autopilot-deployment.md)
- Step 2: [Install required modules to obtain Autopilot profile(s) from Intune](install-modules.md)
- Step 3: [Create JSON file for Autopilot profile(s)](create-json-file.md)
- Step 4: [Create and distribute package for JSON file in Configuration Manager](create-json-package.md)
> [!div class="checklist"]
> - **Step 5: Create Autopilot task sequence in Configuration Manager**
- Step 6: [Create collection in Configuration Manager](create-collection.md)
- Step 7: [Deploy Autopilot task sequence to collection in Configuration Manager](deploy-autopilot-task-sequence.md)
- Step 8: [Speed up the deployment process (optional)](speed-up-deployment.md)
- Step 9: [Run Autopilot task sequence on device](run-autopilot-task-sequence.md)
- Step 10: [Register device for Windows Autopilot](register-device.md)

For an overview of the Windows Autopilot deployment for existing devices workflow, see [Windows Autopilot deployment for existing devices in Intune and Configuration Manager](existing-devices-workflow.md)

## Create Autopilot task sequence for existing devices in Configuration Manager

Once the packages containing the Autopilot profile JSON files have been created and distributed in Configuration Manager, the next step is to create a task sequence that wipes the device, installs a fresh copy of Windows on the device, and then copies the Autopilot profile JSON file to the device. Copying of the Autopilot profile JSON file is done in WinPE when the newly installed Windows OS is offline. When the task sequence completes, the device will boot into the newly installed Windows OS for the first time and run the out of box experience (OOBE). The OOBE process will then process the Autopilot profile JSON file which will initiate the Autopilot deployment.

> [!NOTE]
>
> If multiple Autopilot profiles are being used and multiple Autopilot profile JSON files were created, a separate task sequence is needed for each of the Autopilot profiles.

To create the Autopilot for existing devices task sequence in Configuration Manager, follow these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems***.

1. Select **Task Sequences** and then on the ribbon, select **Create Task Sequence**. Alternatively, right-click **Task Sequences** and select **Create Task Sequence**.

1. The **Create Task Sequence Wizard** window appears:

   1. In the **Create new task sequence** page, select the option to **Deploy Windows Autopilot for existing devices**, and then select the **Next >** button.

   2. In the **Specify task sequence information** page:

      1. Next to **Name**, enter an identifiable name for the Autopilot scenario that the task sequence is for.

      1. Next to **Description**, enter a description for the Autopilot scenario that the task sequence is for.

      1. Next to **Boot image:**, select the **Browse** button.

        - In the **Select a Boot Image** windows that appears, under **Boot images:**, select a boot image, and then select the **OK** button.

      1. Select the **Next >** button.

   3. In the **Install the Windows operating system** page:

      1. Next to **Image package:**, select the **Browse** button.

         - In the **Select an Operating System Image** window that appears:

            1. Under **Operating system images:**, locate and select the desired Windows operating system image. If necessary, navigate to the desired Windows operating system image using the **Folders:** left hand pane.

            2. Once the desired Windows operating system image is selected, select the **OK** button.
  
      2. Next to **Image index:**, select the desired Windows version. For example, **Enterprise**.

      3. Make sure the option **Partition and format the target computer before installing the operating system** is selected and enabled.

      4. Make sure the option **Configure task sequence for use with BitLocker** is not selected. If BitLocker encryption is desired, it's recommend to enabled via Intune policies that are applied during the Autopilot deployment.

          > [!NOTE]
          >
          > Although BitLocker encryption could technically be enabled via the task sequence, it may result in undesired outcomes. For example, BitLocker recovery keys being saved to Configuration Manager BitLocker Management or on-premise Active Directory instead of Intune or Azure AD. Additionally, if certain BitLocker settings specified in the task sequence, such as BitLocker encryption method and strength, doesn't match the BitLocker policy settings in Intune, then this could cause the device to show as non-compliant. Resolving issues like this could mean having to decrypt and then re-encrypt the drive to resolve. Therefore it's recommended not to enable BitLocker as part of the task sequence and instead enable BitLocker as part of Intune policies deployed during Autopilot.

      5. Leave **Product key** blank. The Autopilot for existing devices task sequence runs the [Windows System Preparation Tool (Sysprep)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview) at the end of the task sequence. Sysprep will clear any key that is specified.
  
      6. Leave the option of **Randomly generate the local administrator password and disable the account on all support platforms (recommended)** selected.

          > [!NOTE]
          >
          > Alternatively, the option of **Enable the account and specify the local administrator password** can be selected and a password specified, but the password selected will only be useful if there is a failure after the **Setup Windows and ConfigMgr** task and the task sequence doesn't end successfully. If the task sequence completes successfully and ends, the password will no longer be valid since the task sequence runs Sysprep at the end of the task sequence which clears the local administrator password.

      7. Select the **Next >** button.

      > [!NOTE]
      >
      > If using the alternate [Speed up the deployment process (optional)](speed-up-deployment.md) step later in this tutorial, Sysprep never runs as part of the task sequence. However, the product key and local administrator password never gets processed since the `unattend.xml` file that contains the product key and local administrator password is deleted as part of this optional step. For this reason, when using the alternate [Speed up the deployment process (optional)](speed-up-deployment.md) step, the settings specified for these two options are irrelevant since they're never processed.

   4. In the **Install the Configuration Manager client** page, add any necessary Configuration Manager client installation properties for the environment. For example, since the device will be a Workgroup device and not domain joined during the task sequence, the [SMSMP](/mem/configmgr/core/clients/deploy/about-client-installation-properties#smsmp) or [SMSMPLIST](/mem/configmgr/core/clients/deploy/about-client-installation-properties#smsmplist) parameters may be needed to run certain tasks such as the **Install Application** or **Install Software Updates** tasks. Once finished adding any Configuration Manager client installation properties, select the **Next >** button.

      > [!NOTE]
      >
      > The Configuration Manager client is installed as part of the Autopilot for existing devices task sequence to support running certain tasks such as the **Install Application** or **Install Software Updates** tasks later on in the task sequence. The Configuration Manager client though is uninstalled at the end of the task sequence. If no additional tasks are needed after the **Setup Windows and ConfigMgr** task, consider following the step [Speed up the deployment process (optional)](speed-up-deployment.md) later in the tutorial. This optional step will skip installing the Configuration Manager client which will save time and avoid potential problems with the Configuration Manager having been installed on the device (despite being uninstalled).

   5. In the **Install software updates** page, select the desired option to install software updates during the task sequence. For the  Autopilot for existing devices task sequence, it's recommend to leave the the option to the default of **Do not install any software updates** and not install any software updates during the task sequence. Once the desired option is selected, select the **Next >** button.

      > [!TIP]
      >
      > It's recommended not to install software updates during the Autopilot for existing devices task sequence because doing so will significantly increase the time for the task sequence to complete. Instead, consider installing updates using one of the following two options:
      >
      > - The Configuration Manager offline image servicing feature of [Scheduled Updates](/mem/configmgr/osd/get-started/manage-operating-system-images#apply-software-updates-to-an-image)
      > - Every month download the latest monthly ISO for the version of Windows that you're installing and then update the **Operating System Images** package in Configuration Manager with the new updated install.wim from the ISO. The ISOs are updated monthly and have the latest updates in them.

   6. In the **Install applications** page, select the desired applications to install during the task sequence. Once the desired applications have been added, select the **Next >** button. If no applications are desired to be installed, then select the **Next >** button.

      > [!TIP]
      >
      > Instead of installing applications during the task sequence, Microsoft recommends that you install all applications and configurations from Microsoft Intune or Configuration Manager co-management. This process provides a consistent experience between users receiving new devices and those using Windows Autopilot for existing devices.  

   7. On the **Prepare System for Windows Autopilot** page, select the package that includes the Autopilot JSON file created in the step [Create and distribute package for JSON file in Configuration Manager](create-json-package.md). Once the package with the Autopilot JSON file has been selected, select the **Next >** button.

      > [!NOTE]
      >
      > Leave the option **Shutdown computer after this task sequence completes** unchecked. This option will be configured later in the section [Modify the Autopilot for existing devices task sequence to account for Sysprep command line configuration](#modify-the-autopilot-for-existing-devices-task-sequence-to-account-for-sysprep-command-line-configuration)

   8. On the **Confirm the settings** page, verify that all settings are correct, and then select the **Next >** button.

   9. When the **Create Task Sequence Wizard** completes with **The task "Create Task Sequence Wizard" completed successfully** message, select the **Close** button.

1. If using multiple Autopilot profiles and multiple Autopilot profile JSON files were created, repeat the above steps to create additional task sequences. Each Autopilot profile JSON file needs its own separate task sequence.

## Modify the Autopilot for existing devices task sequence to account for Sysprep command line configuration

The Autopilot for existing devices task sequence adds the **Prepare Windows for Capture** task to the task sequence. The **Prepare Windows for Capture** task is the task that runs Sysprep. Sysprep runs so that on next boot, OOBE runs and processes the Autopilot profile JSON file. However, the **Prepare Windows for Capture** task adds the `/Generalize` parameter to the Sysprep command line. The `/Generalize` parameter causes Sysprep to delete the Autopilot profile JSON file. The `/Generalize` parameter for Sysprep is normal for traditional build and capture task sequences not associated with Autopilot, but it breaks Autopilot deployments since the Autopilot profile JSON file is deleted. This will cause Autopilot to never run during OOBE.

To resolve the issue, the **Prepare Windows for Capture** task needs to be removed from the task sequence and replaced with a **Run Command Line** task that runs Sysprep without the `/Generalize` parameter. This resolution can be accomplished by following these steps:

1. On a device where the Configuration Manager console is installed, such as a Configuration Manager site server, open the Configuration Manager console.

1. In the left hand pane of the Configuration Manager console, navigate to **Software Library** > **Overview** > **Operating Systems***.

1. Expand **Task Sequences** and then locate the Autopilot for existing devices task sequence created in the [Create Autopilot task sequence for existing devices in Configuration Manager](#create-autopilot-task-sequence-for-existing-devices-in-configuration-manager) section.

1. Once the Autopilot for existing devices task sequence is located, select it and then on the ribbon, select **Edit**. Alternatively, right-click on the the Autopilot for existing devices task sequence and select **Edit**.

1. The **Task Sequence Editor** window opens:

   1. Select the **Prepare Windows for Capture** task.

   2. Select the **Add** drop down menu in the top left of the task sequence editor and then select **General** > **Run Command Line**. This will add a **Run Command Line** task immediately after the **Prepare Windows for Capture** task.

   3. Select the **Run Command Line** task and configure it as follows based on the desired behavior:

        When Sysprep completes, it has the option to either shut down or restart the device:

         - Restarting the device will cause the device to restart as soon as the task sequence completes and then immediately boot into Windows for the first time and run OOBE. When OOBE runs, the Autopilot JSON file will be processed and the Autopilot deployment will start.

         - Shutting down the device instead of restarting the device gives the option to further prepare the device and then deliver it to a user. OOBE and the Autopilot deployment will then start when the end-user turns on the device for the first time.

      - **Name**: Sysprep

      - **Command Line**:

        Select one of the following two command lines based on desired behavior. Copy and paste the desired command line by selecting **Copy** at the top right corner of the below **Command Prompt** code block and then pasting into the **Command Line** text box:

        - Restart device after running Sysprep. OOBE and that Autopilot deployment will start immediately after the task sequence completes:

          ```cmd
          C:\Windows\System32\Sysprep\Sysprep.exe /oobe /reboot
          ```

        - Shut down device after running Sysprep. OOBE and the Autopilot deployment will start when the device is turned on for the first time by the end-user:

          ```cmd
          C:\Windows\System32\Sysprep\Sysprep.exe /oobe /shutdown
          ```

   4. Select the **Prepare Windows for Capture** task again and then select the **Remove** option in the top left of the task sequence editor. A confirmation dialog box will appear confirming to delete the step. Select the **Yes** button to remove the **Prepare Windows for Capture** task.

   5. Select the **OK** button in the **Task Sequence Editor** to save the changes to the task sequence.

## Next step: Create collection in Configuration Manager

> [!div class="nextstepaction"]
> [Step 6: Create collection in Configuration Manager](create-collection.md)

## More information

For more information on creating an Autopilot task sequence in Configuration Manager, see the following article(s):

- [Create a task sequence](/mem/autopilot/existing-devices#create-a-task-sequence)
- [Windows System Preparation Tool (Sysprep)](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview)
- [Windows Autopilot for existing devices doesn't work](/mem/autopilot/known-issues#windows-autopilot-for-existing-devices-doesnt-work-for-windows-10-version-1903-or-1909)
