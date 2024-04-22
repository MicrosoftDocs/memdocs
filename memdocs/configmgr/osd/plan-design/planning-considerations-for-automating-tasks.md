---
title: Plan for automating tasks
titleSuffix: Configuration Manager
description: Plan before you create task sequences to automate tasks with Configuration Manager.
ms.date: 03/10/2022
ms.service: configuration-manager
ms.subservice: osd
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Plan for automating tasks in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can create task sequences to automate tasks in your Configuration Manager environment. These tasks range from capturing an OS on a reference computer to deploying the OS to one or more destination computers. The actions of the task sequence are defined in the individual steps of the sequence. When the task sequence runs, it runs the actions of each step at the command-line level in the Local System context. This behavior means the task sequence runs fully automated with no user intervention.

## Task sequence steps and actions

Steps are the basic components of a task sequence. They can include commands such as:

- Configure and capture the OS of a reference computer
- Install Windows, hardware drivers, the Configuration Manager client, and software on the destination computer

The actions of the step define the commands of a task sequence step. There are two types of actions:

- An action that you define by using a command-line string is referred to as a *custom action*
- An action that's predefined by Configuration Manager is referred to as a *built-in action*.

A task sequence can do any combination of custom and built-in actions.

Task sequence steps can also include conditions that control how the step behaves. These behaviors include stopping the task sequence, or continuing the task sequence if an error occurs. One type of condition is a task sequence variable. For example, use the **SMSTSLastActionRetCode** variable to test the condition of the previous step. Add conditions to a single step or a group of steps.

The task sequence processes steps sequentially. This sequence includes the action of the step and any conditions on the step. When Configuration Manager starts to process a task sequence step, it doesn't start the next step until the previous action is complete.

A task sequence is considered complete when:

- All its steps are complete.
- A failed step causes Configuration Manager to stop running the task sequence before all its steps are completed.

For example, if the step of a task sequence can't locate a referenced image or package on a distribution point, the task sequence includes a broken reference. Configuration Manager stops running the task sequence at that point, unless the failed step has a condition to continue when an error occurs.

> [!IMPORTANT]
> By default, a task sequence fails after one step or action fails. If you want the task sequence to continue even when a step fails, edit the task sequence, switch to the **Options** tab, and then select **Continue on error**.

For more information about the steps that can be added to a task sequence, see [Task sequence steps](../understand/task-sequence-steps.md).

## Task sequence groups

You can group multiple steps within a task sequence. A task sequence group consists of a name, an optional description, and any optional conditions. The task sequence evaluates the group conditions as a unit before it continues with the next step. Nest groups within each other, or include a mixture of steps and subgroups. Groups are useful for combining multiple steps that share a common condition.

Assign a name to task sequence groups. It doesn't have to be unique. You can also provide an optional description for the task sequence group.

> [!IMPORTANT]
> By default, a task sequence group fails when any step or embedded group within the group fails. If you want the task sequence to continue when a step or embedded group fails, set the **Continue on error** option on the step or group.

The following table shows how the **Continue on error** option works when you group steps.

In this example, there are two groups of task sequences that include three task sequence steps each.

|Task sequence group or step|Continue on error setting|
|---------------------------------|-------------------------------|
|**Task sequence group 1**|**Continue on error** selected.|
|Task sequence step 1|**Continue on error** selected.|
|Task sequence step 2|Not set.|
|Task sequence step 3|Not set.|
|**Task sequence group 2**|Not set.|
|Task sequence step 4|Not set.|
|Task sequence step 5|Not set.|
|Task sequence step 6|Not set.|

- If task sequence step 1 fails, the task sequence continues with task sequence step 2.

- If task sequence step 2 fails, the task sequence doesn't run task sequence step 3. Because task sequence group 1 is configured to **Continue on error**, the task sequence continues to task sequence group 2. It runs task sequence step 4 next.

- If task sequence step 4 fails, no more steps are run. The task sequence fails because the **Continue on error** setting isn't configured for task sequence group 2.

## Add child task sequences to a task sequence

<!--1261338-->

Add a new task sequence step that runs another task sequence. This step creates a parent-child relationship between the task sequences. Using this step allows you to create more modular task sequences that you can reuse.

For more information, see [Run Task Sequence](../understand/task-sequence-steps.md#child-task-sequence).

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../core/servers/manage/optional-features.md).<!--505213-->

## Task sequence variables

Task sequence variables are a set of name and value pairs. They supply configuration and OS deployment settings for computer, OS, and user state configuration tasks on a Configuration Manager client. Task sequence variables provide a mechanism to configure and customize the steps in a task sequence.

When you run a task sequence, it stores many of the task sequence settings as environment variables. You can access or change the values of built-in task sequence variables. You can also create new task sequence variables to customize the way a task sequence runs on a destination computer.

Use task sequence variables to do the following actions:

- Configure settings for a task sequence action

- Supply command-line arguments for a task sequence step

- Evaluate a condition that determines whether a task sequence step or group runs

- Provide values for custom scripts used in a task sequence

For example, you have a task sequence that includes a **Join Domain or Workgroup** task sequence step. Deploy the task sequence to different collections, where the membership of the collection is determined by domain membership. Specify a per-collection task sequence variable for each collection's domain name. Then use that task sequence variable to supply the appropriate domain name in the task sequence.

For more information, see [How to use task sequence variables](../understand/using-task-sequence-variables.md).

## Create a task sequence

Create task sequences by using the Create Task Sequence Wizard. The wizard can create built-in task sequences that do specific tasks or custom task sequences that can do many different tasks. The wizard lets you create the following types of task sequences:

- Install an existing OS image on a destination computer

- Build and capture an OS image of a reference computer

- Upgrade Windows with an OS upgrade package on a destination computer

- Create a custom task sequence that does a customized task or specialized OS deployment

For more information, see [Create a task sequence to install an OS](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).

## Edit a task sequence

Edit the task sequence by using the **Task Sequence Editor**. The editor can make the following changes to the task sequence:

- Add or remove steps from the task sequence

- Change the order of the steps of the task sequence

- Add or remove groups of steps

- Specify whether the task sequence continues when an error occurs

- Add conditions to the steps and groups of a task sequence

> [!IMPORTANT]
> If the task sequence has any unassociated references to an object as a result of the edit, the editor requires you fix the reference before it can close. Possible actions include:
>
> - Correct the reference
> - Delete the unreferenced object from the task sequence
> - Temporarily disable the failed task sequence step until the broken reference is corrected or removed

For more information about how to edit task sequences, see [Use the task sequence editor](../understand/task-sequence-editor.md).

## Deploy a task sequence

Deploy a task sequence to destination computers that are in any Configuration Manager collection. Use the built-in **All Unknown Computers** collection to deploy operating systems to unknown computers. You can't deploy a task sequence to user collections.

> [!IMPORTANT]
> Don't deploy task sequences that install operating systems to inappropriate collections. Be sure that the collection to which you deploy the task sequence includes only those computers where you want to install the OS. To help prevent unwanted OS deployments, configure settings for high-risk deployments. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

Each destination computer that receives the task sequence runs the task sequence according to the settings specified in the deployment. The task sequences itself doesn't contain associated files or programs. Any files that a task sequence references must already be present on the destination computer or stored on a distribution point that clients can access.

> [!NOTE]
> The task sequence installs packages that are referenced by programs, even if the program or package is already installed on the destination computer.
>
> If the task sequence installs an application, the application installs only if the requirement rules for the application are met, and the application isn't already installed, based on the detection method that's specified for the application.

The Configuration Manager client runs a task sequence deployment when it downloads client policy. To trigger this action rather than wait until the next polling cycle, see [Initiate policy retrieval for a Configuration Manager client](../../core/clients/manage/manage-clients.md#start-policy-retrieval).

When you deploy task sequences to Windows Embedded devices that are enabled with a write filter, you can specify whether to disable the write filter on the device during the deployment and then restart the device after the deployment. If the write filter isn't disabled, the task sequence is deployed to a temporary overlay and it won't be available when the device restarts.

> [!NOTE]
> When you deploy a task sequence to a Windows Embedded device, ensure that the device is a member of a collection that has a configured maintenance window. This allows you to manage when the write filter is disabled and enabled, and when the device restarts.
>
> If clients download task sequences outside of a maintenance window, the task sequence is downloaded twice. In this scenario, the client downloads the task sequence, disables the write filter, restarts the computer, and then downloads the task sequence again. This behavior is because the task sequence was originally downloaded to the temporary overlay, which is cleared when the device restarts.

For more information about how to deploy task sequences, see the [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md).

## Export and import

Configuration Manager lets you export and import task sequences. When you export a task sequence, you can include the objects that are referenced by the task sequence.

For more information, see [Export and import task sequences](../deploy-use/export-import-task-sequences.md).

## Run a task sequence

Task sequences always run by using the Local System account. When the task sequence runs, the Configuration Manager client first checks for any referenced packages before it starts the steps of the task sequence. If it can't validate or download a referenced package, the task sequence returns an error for the associated task sequence step.

> [!NOTE]
> The task sequence step **Run Command Line** provides the ability to run a command as a different account.

If you configure a task sequence deployment to download and run, the Configuration Manager client downloads all dependent content to its cache. If the client cache size is too small or the content can't be found, the task sequence fails. The client generates a status message.

You can also specify that the client downloads the content only when it's required. To do this action, select **Download content locally when needed by running task sequence** in the task sequence deployment. Another option is to **Run program from distribution point**. With this option, the client installs the files directly from the distribution point without downloading them into the cache first.

When you configure the task sequence deployment as **Available**, if the client can't locate dependent content for the task sequence, it immediately sends an error. For a **Required** deployment, the Configuration Manager client waits in this situation. It retries to download the content until the deadline, in case the content isn't yet replicated to a content location that the client can access.

When a task sequence completes successfully or fails, Configuration Manager records this state in the client history.

Once a task sequence starts on a computer, you can't cancel or stop it.

> [!IMPORTANT]
> If a task sequence step requires the computer to restart, the client must be able to boot to a formatted disk partition. Otherwise, the task sequence fails regardless of any error handling that you specify in the task sequence.

When a dependent object of a task sequence is updated to a newer version, any task sequence that references the package is automatically updated. It references the newest version, no matter how many updates you've deployed.

## Use maintenance windows

You can specify when the task sequence can run by defining a maintenance window for the device collection. You configure maintenance windows with a start date, a start and finish time, and a recurrence pattern. When you set the schedule for the maintenance window, you can specify that the maintenance window applies only to task sequences. For more information, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).

> [!IMPORTANT]
> When you configure a maintenance window to run a task sequence, once the task sequences starts it continues to run even if the maintenance window closes.

If a device has more than one maintenance window applied, the client may ignore an **All deployments** maintenance window. Starting in version 1810, use the following client setting to control this behavior: **Enable installation of software updates in "All deployments" maintenance window when "Software Update" maintenance window is available**. For more information, see [About client settings](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)<!-- SCCMDocs-pr #4596 -->

## Task sequences and the network access account

> [!IMPORTANT]
> Some OS deployment scenarios don't require use of the network access account. For more information, see [Enhanced HTTP](#enhanced-http).

Although task sequences run only in the context of the Local System account, you might need to configure the [network access account](../../core/plan-design/hierarchy/accounts.md#network-access-account) in the following circumstances:

- If the task sequence tries to access Configuration Manager content on distribution points. Correctly configure the network access account, or the task sequence will fail.

- When you use a boot image to initiate an OS deployment. In this case, Configuration Manager uses the Windows PE environment, which isn't a full OS. The Windows PE environment uses an automatically generated, random name that isn't a member of any domain. If you don't correctly configure the network access account, the computer can't access the required content for the task sequence.

> [!NOTE]
> The network access account is never used as the security context for running programs, installing applications, installing updates, or running task sequences. The network access account is only used to access the associated resources on the network.

For more information about the network access account, see [Network access account](../../core/plan-design/hierarchy/accounts.md#network-access-account).

### Enhanced HTTP
<!--1358278-->

When you enable **Enhanced HTTP**, the following scenarios don't require a network access account to download content from a distribution point:

- Task sequences running from boot media or PXE
- Task sequences running from Software Center

These task sequences can be for OS deployment or custom. It's also supported for workgroup computers.

For more information, see [Enhanced HTTP](../../core/plan-design/hierarchy/enhanced-http.md).

> [!NOTE]
> The following OS deployment scenarios still require the use of a network access account:
>
> - The task sequence [deployment option](../deploy-use/deploy-a-task-sequence.md), **Access content directly from a distribution point when needed by the running task sequence**
> - The [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) step option, **If computer account fails to connect to a state store, use the network access account**
> - When connecting with an untrusted domain or across Active Directory forests
> - The [Apply OS Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) step option, **Access content directly from the distribution point**
> - The task sequence [advanced setting](../deploy-use/manage-task-sequences-to-automate-tasks.md#advanced-tab) to **Run another program first**
> - [Multicast](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)

## Create media

You can write task sequences and their related files and dependencies to several types of media. Configuration Manager supports removable media such as a DVD or a USB flash drive for capture, stand-alone, and bootable media. Prestaged media uses a Windows image (WIM) file.

When you create media, specify a password to control access. Then a person must enter the password at the target computer to run the task sequence.

When you run a task sequence from media, the specified processor architecture of the media isn't recognized. If the specified architecture doesn't match the target computer, the task sequence still attempts to run. If the architecture of the media doesn't match the architecture of the target computer, the task sequence fails.

For more information, see [Create task sequence media](../deploy-use/create-task-sequence-media.md).

### Media types

Configuration Manager supports the following types of media:

#### Capture media

This media captures an OS image that you configure and create outside of the Configuration Manager infrastructure. Capture media can contain custom programs that can run before a task sequence runs. The custom program can interact with the desktop, prompt the user for input values, or create variables to be used by the task sequence.

For more information, see [Create capture media](../deploy-use/create-capture-media.md).

#### Stand-alone media

Stand-alone media contains the task sequence and all associated objects that are necessary for the task sequence to run. Stand-alone media task sequences can run when Configuration Manager has limited or no connectivity to the network. Run stand-alone media in the following ways:

- If the destination computer isn't booted, the Windows PE image associated with the task sequence is used from the stand-alone media, and the task sequence begins.

- Manually start the stand-alone media. If a user is signed in to the computer, they can initiate the task sequence from the media.

> [!IMPORTANT]
> The steps of a stand-alone media task sequence must be able to run without retrieving any data from the network. Otherwise, the task sequence step that tries to retrieve the data fails. For example, a task sequence step that requires a distribution point to obtain a package fails. If the stand-alone media contains the necessary package, the task sequence step succeeds.

For more information, see [Create stand-alone media](../deploy-use/create-stand-alone-media.md).

#### Bootable media

Bootable media contains the required files to start a destination computer so that it can connect to the Configuration Manager infrastructure. It then determines which task sequences to run based on its collection memberships. This media doesn't include the task sequence or dependent objects. Instead, the client downloads the content over the network. This method is useful for new computers or bare-metal deployments, when no OS is on the destination computer.

For more information, see [Create bootable media](../deploy-use/create-bootable-media.md).

#### Prestaged media

Prestaged media deploys an OS image to a destination computer that isn't provisioned. The prestaged media is stored as a Windows image (WIM) file. This file can be installed on a bare-metal computer by the manufacturer or at an enterprise staging center. A benefit of prestaged media is that these locations don't require a connection to your Configuration Manager environment.

For more information, see [Create prestaged media](../deploy-use/create-prestaged-media.md).

## Next steps

- [Security and privacy for OS deployment](security-and-privacy-for-operating-system-deployment.md)

- [Prepare site system roles for OS deployments](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
