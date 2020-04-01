---
title: User experiences for OS deployment
titleSuffix: Configuration Manager
description: Learn about user experiences like the task sequence progress and media wizard for operating system deployment in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# User experiences for OS deployment

*Applies to: Configuration Manager (current branch)*

After you [deploy a task sequence](/configmgr/osd/deploy-use/deploy-a-task-sequence), depending upon the scenario there are different ways for users to interact with the deployment. This article shows the main user experiences with OS deployments, and how you can configure them:

- Software Center user notification for a high-impact deployment
- A sample PXE boot experience
- Task sequence wizard from media
- Progress window when the task sequence runs
- Error window when the task sequence fails

## Software Center

For a high-impact deployment, you can customize the message that Software Center displays. When the user opens the OS deployment in Software Center, they see a message similar to the following window:

![Customized task sequence notification to the end user from Software Center](../media/user-notification-enduser.png)

For more information on how to customize the message in this window, see [Create a custom notification for high-risk deployments](/configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks#create-a-custom-notification-for-high-risk-deployments).

You can also customize the organization name at the top of the window. (The above example shows the default value, `IT Organization`). Change the **Organization name** client setting in the **Computer Agent** group. For more information, see [About client settings](/configmgr/core/clients/deploy/about-client-settings#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

For more information, see [Use Software Center to deploy Windows over the network](/configmgr/osd/deploy-use/use-software-center-to-deploy-windows-over-the-network).

## PXE

Different hardware models have different experiences for PXE. To boot to the network, UEFI-based devices typically use the `Enter` key, and BIOS-based devices use the `F12` key.

The following example shows the Hyper-V Gen1 (BIOS) PXE experience:

![Example BIOS PXE screen from a Hyper-V virtual machine](media/hyperv-pxe.png)

After the device successfully boots via PXE, it behaves similarly to bootable media. For more information, see the next section on the [Task sequence wizard](#task-sequence-wizard).

For more information, see [Use PXE to deploy Windows over the network](/configmgr/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).

> [!WARNING]
> If you use PXE deployments, and configure device hardware with the network adapter as the first boot device, these devices can automatically start an OS deployment task sequence without user interaction. Deployment verification doesn't manage this configuration. While this configuration may simplify the process and reduce user interaction, it puts the device at greater risk for accidental reimage.

## Task sequence wizard

When you use [task sequence media](/configmgr/osd/deploy-use/create-task-sequence-media), the task sequence wizard runs to guide the process.

### Welcome to the task sequence wizard

![Screenshot of main page of the Task Sequence Wizard](media/welcome-task-sequence-wizard.png)

- If you password-protect the media, the user has to enter the password on this welcome page.

- Select **Configure Network Settings** to specify a static IP address or other custom network settings. Otherwise, the device uses DHCP by default.

- If your network requires a proxy, select **Configure Proxy Settings**.

### Select a task sequence to run

If you deploy more than one task sequence to the device, you see this page to select a task sequence. Make sure to use a name and description for your task sequence that users can understand.

![Screenshot of the task sequence selection page of the Task Sequence Wizard](media/task-sequence-wizard-select.png)

### Edit task sequence variables

If any task sequence variables have empty values, the wizard shows a page to edit the variable values.

![Screenshot of the edit task sequence variables page of the Task Sequence Wizard](media/task-sequence-wizard-variables.png)

## Prestart commands

You can customize task sequence media or boot images to run a prestart command. A prestart command runs before the task sequence starts. The following actions are some of the more common ones:

- Prompt the user for dynamic values, like the computer name
- Specify network configuration
- Set user device affinity

The prestart command is a command line that you specify with a script or program. The user experience is unique to that script or program.

For more information, see the following articles:

- [Prestart commands for task sequence media](/configmgr/osd/understand/prestart-commands-for-task-sequence-media)
- [Manage boot images](/configmgr/osd/get-started/manage-boot-images#customization)
- [Task sequence media](/configmgr/osd/deploy-use/create-task-sequence-media)

## Task sequence progress

When the task sequence runs, it displays the **Installation progress** window:

![Example of the Task Sequence Progress window](media/task-sequence-progress.png)

- This window is always on top; you can move it, but you can't close or minimize it.

- You can customize the organization name at the top of the window. (The above example shows the default value, `IT Organization`). Change the **Organization name** client setting in the **Computer Agent** group. For more information, see [About client settings](/configmgr/core/clients/deploy/about-client-settings#computer-agent).

    > [!TIP]
    > The task sequence stores this value in the read-only variable [_SMSTSOrgName](/configmgr/osd/understand/task-sequence-variables#_SMSTSOrgName).

- You can customize the subheading. (The above example shows the default value, `Running: <task sequence name>`.) On the properties of the task sequence, select the option to **Use custom text** for the progress notification text. It allows a maximum of 255 characters.

- **Running action**: The first line shows the name of the current task sequence step. The progress bar below it shows the overall completion of the task sequence.

- The second line only shows for some steps that provide more detailed progress.

- Use the task sequence variable [TSDisableProgressUI](/configmgr/osd/understand/task-sequence-variables#TSDisableProgressUI) to control when the task sequence displays progress.

    To completely disable the progress window, disable the option to **Show Task Sequence progress** on the **User Experience** page of the task sequence deployment.

Starting in version 2002, the task sequence progress window includes the following improvements:<!--5932692-->

- Shows the current step number, total number of steps, and percent completion

- Increased the width of the window to give you more space to better show the organization name in a single line

![Example task sequence progress window](media/2356386-task-sequence-progress.png)

By default, the task sequence progress window uses the existing text. If you make no changes, it continues to work the same as in version 1910 and earlier. To show the new progress information, specify the task sequence variable, [TSProgressInfoLevel](/configmgr/osd/understand/task-sequence-variables#TSProgressInfoLevel).

The count and percentage completed are intended for general guidance purposes only. These values are based on the total number of steps in the task sequence. For a more complex task sequence with steps that run conditionally based on task sequence logic, the progress may be non-linear.

The count of total steps doesn't include the following items in the task sequence:

- Groups. This item is a container for other steps, not a step itself.

- Instances of the **Run task sequence** step. This step is a container for other steps.

- Steps that you explicitly disable. A disabled step doesn't run during the task sequence.

    > [!NOTE]
    > Enabled steps in a disabled group are still included in the total count.

## Task sequence error

If the task sequence fails, it displays the **Task Sequence Error** window.

![Example task sequence error window](media/task-sequence-error.png)

- You customize the header information the same as the task sequence progress window.

- It displays the name of the task sequence, an error code, and a general message for users. For example: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- The window automatically closes after a timeout period. By default, this timeout is 15 minutes. You can customize this value with the task sequence variable [SMSTSErrorDialogTimeout](/configmgr/osd/understand/task-sequence-variables#SMSTSErrorDialogTimeout).
