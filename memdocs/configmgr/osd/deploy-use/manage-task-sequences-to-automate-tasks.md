---
title: Manage task sequences
titleSuffix: Configuration Manager
description: Configure the settings of task sequences.
ms.date: 03/28/2022
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: overview
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Manage task sequences

*Applies to: Configuration Manager (current branch)*

After you create a task sequence, there are additional settings that you can configure. Task sequences are located in the Configuration Manager console. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**. The **Task Sequences** node, including subfolders that you create, is replicated throughout the Configuration Manager hierarchy. For planning information, see [Planning considerations for automating tasks](../plan-design/planning-considerations-for-automating-tasks.md).

## Edit

Modify a task sequence by adding or removing steps, adding or removing groups, or by changing the order of the steps. For more information, see [Use the task sequence editor](../understand/task-sequence-editor.md).

## Properties

The task sequence editor configures the steps of the task sequence. There are additional settings available on the **Properties** of the task sequence, which control other aspects of how the task sequence runs and behaves.

In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**. Select the task sequence to configure, and then in the ribbon select **Properties**.

The following sections provide more details about each tab of the task sequence properties.

### **General** tab: Software Center properties

On the **General** tab, the following settings for Software Center are available:

#### Restart required

Lets the user know whether a restart is required during the installation.

#### Download size (MB)

Specifies how many megabytes are displayed in Software Center for the task sequence.

#### Estimated run time (minutes)

Specifies the estimated run time in minutes that's displayed in Software Center for the task sequence.

### **Advanced** tab

On the **Advanced** tab, the following settings are available:

#### Run another program first

Select this option to run a program in another package before the task sequence runs. By default, this option isn't enabled. You don't need to separately deploy the program that you specify to run first.

> [!IMPORTANT]
> This setting applies only to task sequences that run in the full OS. If you start the task sequence by using PXE or boot media, Configuration Manager ignores this setting.
>
> It also doesn't apply to task sequences that run on clients that communicate via a cloud management gateway (CMG). This option uses the UNC network path of the package, which isn't accessible via CMG.<!-- 8674270 -->

- **Package**: Browse for the package that contains the program to run before this task sequence.

- **Program**: Select the program to run before this task sequence.

  > [!NOTE]
  > If the selected program fails to run on a client, the task sequence doesn't run. If the selected program runs successfully, it doesn't run again, even if the task sequence is rerun on the same client.

#### Suppress task sequence notifications

Select this option to hide the **New Software is available** toast notification. You still see the **New software** icon from Software Center in the notification area. By default, this option is disabled.

#### Disable this task sequence on computers where it is deployed

If you select this option, Configuration Manager temporarily disables all deployments that contain this task sequence. It also removes the task sequence from the list of deployments available to run. The task sequence doesn't run until you enable it. By default, this option is disabled.

#### Maximum allowed run time

Specifies the maximum time in minutes that you expect the task sequence to run on the destination computer. Use a whole number equal to or greater than zero. By default, this value is 120 minutes.

> [!IMPORTANT]  
> If you're using maintenance windows for the collection to which you deploy this task sequence, a conflict might occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If you set the maximum run time to **0**, the task sequence starts during the maintenance window. It continues to run until it completes or fails after the maintenance window is closed. As a result, task sequences with a maximum run time set to **0** might run past the end of their maintenance windows. If you set the maximum run time to a specific period (non-zero) that exceeds the length of any available maintenance window, then that task sequence doesn't run. For more information, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).

If you set the value as **0**, Configuration Manager evaluates the maximum allowed run time as **12** hours (720 minutes) for monitoring progress. However, the task sequence starts as long as the countdown duration doesn't exceed the maintenance window value.

> [!NOTE]
> When it reaches the maximum run time, if you don't allow users to interact with a required deployment, then Configuration Manager stops the task sequence. If the task sequence itself isn't stopped, Configuration Manager stops monitoring the task sequence after it reaches the maximum allowed run time.

#### Use a boot image

Use the selected boot image when the task sequence is run. Select **Browse** to select a different boot image. Clear this option to disable the use of the selected boot image when the task sequence runs.

#### This task sequence can run on any platform

If you select this option, Configuration Manager doesn't check the platform type of the destination computer when the task sequence runs. This option is selected by default.

#### This task sequence can only run on the specified client platforms

This option specifies the processors, OS versions, and service packs on which this task sequence can run. When you select this option, select at least one platform from the list. By default, no platforms are selected. Configuration Manager uses this information when is evaluates which destination computers in a collection receive the deployed task sequence.

> [!NOTE]
> When you run a task sequence from boot media or PXE, Configuration Manager ignores this option. The task sequence runs as though the option **This program can run on any platform** is selected.

### **User Notification** tab for high-impact settings

Configure a task sequence as high-impact and customize the messages that users receive when they run the task sequence. For more information, see [High-impact task sequence settings](high-impact-task-sequence-settings.md).

Any task sequence that meets certain conditions is automatically defined as high-impact. For more general information, see [Manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### **More Options** tab

> [!NOTE]
> In version 2111 and earlier, this tab is named **Performance**.

To improve the overall speed of the task sequence, run it with the high-performance power plan. It configures Windows to use its built-in high-performance power plan, which delivers maximum performance at the expense of higher power consumption. For more information, see [Task sequence performance](task-sequence-performance.md).

#### Custom icons for task sequences

<!--12486335-->

Starting in version 2203, add custom icons for task sequences. These icons appear in Software Center when you deploy the task sequence. Instead of a default icon, a custom icon can improve the user experience to better identify the software.

On the **More Options** tab of task sequence properties, in the section for the icon, select **Browse**. Select an icon from the default shell library, or browse to another file in a local or network path.

- It supports the following file types:
  - Programs (`.exe`)
  - Libraries (`.dll`)
  - Icons (`.ico`)
  - Images (`.png`, `.jpeg`, `.jpg`)
- The file doesn't need to be on clients that you target with the deployment. Configuration Manager includes the image with the deployment policy.
- The maximum file size for an image is 256 KB.
- Icons can have pixel dimensions of up to 512 x 512.

When clients receive the deployment policy, they'll display the icon in Software Center.

> [!NOTE]
> To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

## Additional actions

You can manage task sequences by using additional actions when you select a task sequence.

### Edit action

For more information, see [Use the task sequence editor](../understand/task-sequence-editor.md#bkmk_edit).

### Enable

Enables the task sequence so that clients can run it. You don't need to redeploy a task sequence after it's enabled.

### Disable

Disables the task sequence so that it can't run on computers. You can deploy a disabled task sequence, but computers don't run the task sequence until you enable it.

### Export

For more information, see [Export and import task sequences](export-import-task-sequences.md).

### Copy

Makes a copy of the selected task sequence. This action is useful to create a new task sequence that's based on an existing task sequence.

When you make a copy of a task sequence in a folder, the copy is listed in that folder until you refresh the task sequence node. After the refresh, the copy appears in the root folder.

### Refresh

Refreshes the details for the selected task sequence.

### Delete

Deletes the selected task sequence.

### Create Phased Deployment

For more information, see [Create phased deployments](create-phased-deployment-for-task-sequence.md).

### Deploy

For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).

### Distribute Content

Starts the Distribute Content Wizard to send the referenced content to distribution points.

### Create Prestaged Content File

Starts the Create Prestaged Content File Wizard to prestage the task sequence content. For information about how to create a prestaged content file, see [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### Move

Moves the selected task sequence to another folder in the **Task Sequences** node.

### Set Security Scopes

Select the security scopes for the selected task sequence. For more information, see [Security scopes](../../core/understand/fundamentals-of-role-based-administration.md#security-scopes).

### Properties action

For more information, see [Properties](#properties).

### View

<!--3633146-->
The **View** action on task sequences is the default. This action lets you see the steps of the task sequence without locking it for editing. For more information, see [Use the task sequence editor](../understand/task-sequence-editor.md#bkmk_view).

## Next steps

- [Distribute referenced content](distribute-task-sequence-referenced-content.md)

- [Reduce the size of task sequence policy](reduce-task-sequence-policy-size.md)

- [Deploy a task sequence](deploy-a-task-sequence.md)

- [How to use task sequence variables](../understand/using-task-sequence-variables.md)
