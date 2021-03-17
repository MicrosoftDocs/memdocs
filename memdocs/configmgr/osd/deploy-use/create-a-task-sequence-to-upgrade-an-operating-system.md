---
title: Create an OS upgrade task sequence
titleSuffix: Configuration Manager
description: Use a task sequence to automatically upgrade from Windows 7 or later to Windows 10
ms.date: 03/26/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create a task sequence to upgrade an OS in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use task sequences in Configuration Manager to automatically upgrade an OS on a destination computer. This upgrade can be from Windows 7 or later to Windows 10, or from Windows Server 2012 or later to Windows Server 2016 or later. Create a task sequence that references an OS upgrade package or feature update and any other content to install, such as applications or software updates. The task sequence to upgrade an OS is part of the [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md) scenario.  

Starting in version 2103, you can upgrade by using a feature update deployed with the task sequence. This integration combines the simplicity of Windows servicing with the flexibility of task sequences. Servicing uses a single ESD file that you synchronize through the software update point. This process simplifies the need to manually get, import, and maintain the Windows image content used with a standard task sequence to upgrade Windows. The size of the ESD file is generally smaller than the WIM image file.<!--3555906-->

## Prerequisites

Before you create the task sequence, make sure the following requirements are in place:

### Required

- An [OS upgrade package](../get-started/manage-operating-system-upgrade-packages.md) is available in the Configuration Manager console.

    Starting in version 2103, you can also use a feature update. In this case, the OS upgrade package isn't required. For more information, see [Requirements for a feature update in a task sequence](#requirements-for-a-feature-update-in-a-task-sequence).

- When upgrading to Windows Server 2016 or later, select the **Ignore any dismissable compatibility messages** setting in the Upgrade Operating System task sequence step. Otherwise the upgrade fails.

### Required (if used)

- Synchronize [software updates](../../sum/get-started/synchronize-software-updates.md) in the Configuration Manager console.

- Add [applications](../../apps/deploy-use/create-applications.md) to the Configuration Manager console.

### Requirements for a feature update in a task sequence

<!--3555906-->

- Synchronize the software update point to include the **Upgrades** classification. For more information, see [Configure classifications and products](../../sum/get-started/configure-classifications-and-products.md).

- For a deployment package that contains the feature update, distribute it to a distribution point that the client can access. For more information, see [Download software updates](../../sum/deploy-use/download-software-updates.md).

    > [!NOTE]
    > If the feature update isn't already downloaded, you can manage the deployment package when you deploy the task sequence.
    >
    > When you deploy the task sequence, you can also select the option of **No deployment package** for the feature update. When clients run the task sequence, they download the feature update from peers or the Microsoft cloud.
    >
    > The option to **Pre-download content for this task sequence** doesn't apply to feature updates.

- Review the configuration of the following client settings in the [Software Updates](../../core/clients/deploy/about-client-settings.md#software-updates) group, which are applicable to this scenario:

  - **Specify thread priority for feature updates**: In most instances, set this value to **Normal**.

  - **Enable Dynamic Update for feature updates**: Use this setting to use dynamic update to install language packs, features on demand, drivers, and cumulative updates during Windows Setup. Clients download these other updates from the internet.

  - **Allow clients to download delta content when available**: If you use Windows Delivery Optimization, the content that the client downloads may be much smaller.

#### Known issue with feature update in a task sequence

<!-- bug 8976935 -->
If you need to create a new task sequence, you need an OS upgrade package to complete the Create Task Sequence Wizard.

> [!NOTE]
> To create a task sequence to upgrade an OS to Windows 10, you typically use the steps in the section to [Create a task sequence to upgrade an OS](#create-a-task-sequence-to-upgrade-an-os). The task sequence includes the **Upgrade OS** step, as well as additional recommended steps and groups to handle the end-to-end upgrade process.
>
> You can create a custom task sequence and add the [Upgrade OS](../understand/task-sequence-steps.md#BKMK_UpgradeOS) step. If you choose this method, also add the [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) step after the **Upgrade OS** step. Make sure to use the setting for **The currently installed default operating system** to restart the computer into the installed OS and not Windows PE.

If you have an existing Windows 10 in-place upgrade task sequence, [edit](../understand/task-sequence-editor.md#bkmk_edit) or [copy](manage-task-sequences-to-automate-tasks.md#copy) it. Then change the [Upgrade OS](../understand/task-sequence-steps.md#BKMK_UpgradeOS) task sequence step to install the feature update.

## Create a task sequence to upgrade an OS

To upgrade the OS on clients, create a task sequence and select **Upgrade an operating system from upgrade package** in the Create Task Sequence Wizard. The wizard adds the task sequence steps to upgrade the OS, apply software updates, and install applications.

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select **Task Sequences**.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Task Sequence**.

1. On the **Create a New Task Sequence** page of the Create Task Sequence Wizard, select **Upgrade an operating system from an upgrade package**, and then select **Next**.

1. On the **Task Sequence Information** page, specify the following settings:

    - **Task sequence name**: Specify a name that identifies the task sequence.

    - **Description**: Optionally specify a description.

1. On the **Upgrade the Windows Operating System** page, specify the following settings:

    - **Upgrade package**: Specify the upgrade package that contains the OS upgrade source files. Verify that you've selected the correct upgrade package by looking at the information in the **Properties** pane. For more information, see [Manage OS upgrade packages](../get-started/manage-operating-system-upgrade-packages.md).

    - **Edition index**: If there are multiple OS edition indexes available in the package, select the edition index you want. By default, the wizard selects the first index.

    - **Product key**: Specify the Windows product key for the OS to install. Specify encoded volume license keys or standard product keys. If you use a standard product key, separate each group of five characters by a dash (`-`). For example: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. When the upgrade is for a volume license edition, the product key may not be required.

        > [!NOTE]
        > This product key can be a multiple activation key (MAK), or a generic volume licensing key (GVLK). A GVLK is also referred to as a key management service (KMS) client setup key. For more information, see [Plan for volume activation](/windows/deployment/volume-activation/plan-for-volume-activation-client). For a list of KMS client setup keys, see [KMS client setup keys](/windows-server/get-started/kmsclientkeys) in the Windows Server activation guide.

    - **Ignore any dismissable compatibility messages**: Select this setting if you're upgrading to Windows Server 2016 or later. If you don't select this setting, the task sequence fails to complete because Windows Setup is waiting for the user to select **Confirm** on a Windows app compatibility dialog.

1. On the **Include Updates** page, specify whether to install required, all, or no software updates. Then select **Next**. If you specify to install software updates, Configuration Manager installs only those updates targeted to the collections of which the destination computer is a member.

1. On the **Install Applications** page, specify the applications to install on the destination computer, and then select **Next**. If you select more than one application, also specify whether the task sequence should continue if the installation of a specific application fails.

1. Complete the wizard.

> [!IMPORTANT]
> When the task sequence runs on a device, the Configuration Manager client creates several scripts to control the task sequence behavior in various scenarios. When the task sequence completes, the client doesn't remove these scripts until the computer restarts. These script files don't contain sensitive information.

The default task sequence template for Windows 10 in-place upgrade includes other groups with recommended actions to add before and after the upgrade process. These actions are common among many customers who are successfully upgrading devices to Windows 10. For more information, see the following sections later in this article on recommended task sequence steps:

- [To prepare for upgrade](#recommended-task-sequence-steps-to-prepare-for-upgrade)
- [For post-processing](#recommended-task-sequence-steps-for-post-processing)
- [On failure](#recommended-task-sequence-steps-on-failure)<!--1358500-->

Also review the list of [Other recommendations](#other-recommendations).

## Recommended task sequence steps to prepare for upgrade

The default task sequence template for Windows 10 in-place upgrade includes other groups with recommended actions to add before the upgrade process. These actions in the **Prepare for Upgrade** group are common among many customers who are successfully upgrading devices to Windows 10. If you have an existing task sequence that doesn't already have these actions, manually add them to your task sequence in the **Prepare for Upgrade** group.

### Battery checks

Add steps in this group to check whether the computer is using battery, or wired power. This action requires a custom script or utility to run this check.

#### Battery check example

Use WbemTest and connect to the `root\cimv2` namespace. Then run the following query:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

If it returns any results, then the device is running on battery. Otherwise, the device is connected to wired power.

### Network/wired connection checks

Add steps in this group to check whether the computer is connected to a network, and isn't using a wireless connection. This action requires a custom script or utility to run this check.

#### Network check example

Use WbemTest and connect to the `root\cimv2` namespace. Then run the following query:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

If it returns any results, then the device is running on Wi-Fi. Otherwise, the device is connected to wired network connection.

### Remove incompatible applications

Add steps in this group to remove any applications that are incompatible with this version of Windows 10. The method to uninstall an application varies.

If the application uses Windows Installer, copy the **Uninstall program** command line from the **Programs** tab on the Windows Installer deployment type properties of the application. Then add a **Run Command Line** step in this group with the uninstall program command line. For example:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`

### Remove incompatible drivers

Add steps in this group to remove any drivers that are incompatible with this version of Windows 10.

### Remove/suspend third-party security

Add steps in this group to remove or suspend third-party security programs, such as antivirus.

If you're using a third-party disk encryption program, provide its encryption driver to Windows Setup with the `/ReflectDrivers` [command-line option](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Add a [Set Task Sequence Variable](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step to the task sequence in this group. Set the task sequence variable to **OSDSetupAdditionalUpgradeOptions**. Set the value to `/ReflectDrivers` with the path to the driver. This [task sequence variable](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) appends the Windows Setup command-line used by the task sequence. Contact your software vendor for any further guidance on this process.

### Download Package Content task sequence step

Use the [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) step before the **Upgrade Operating System** step in the following scenarios:

- You use a single upgrade task sequence for both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Set conditions on each step to detect the client architecture. This condition causes the step to download only the appropriate OS upgrade package. Configure each **Download Package Content** step to use the same variable, and use the variable for the media path on the **Upgrade Operating System** step.

- To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Then use that variable for the **Staged content** value in the drivers section on the **Upgrade Operating System** step.

    > [!NOTE]
    > Configuration Manager adds a numerical suffix to this variable name. For example, if you specify `%mycontent%` as a custom variable, the client stores all referenced content in this location. When you refer to the variable in a subsequent step, such as **Upgrade Operating System**, use the variable with a numerical suffix. In this example, `%mycontent01%` or `%mycontent02%`, where the number corresponds to the order in which the **Download Package Content** step lists this specific content.

## Recommended task sequence steps for post-processing

After you create the task sequence, add more steps in the **Post-Processing** group of the task sequence.  

> [!NOTE]  
> This task sequence isn't linear. There are conditions on steps that can affect the results of the task sequence. This behavior depends on whether it successfully upgrades the client computer, or if it has to roll back the client computer to the original OS.

The default task sequence template for Windows 10 in-place upgrade includes other groups with recommended actions to add after the upgrade process. These actions in the **Post-Processing** group are common among many customers who are successfully upgrading devices to Windows 10. If you have an existing task sequence that doesn't already have these actions, manually add them to your task sequence in the **Post-Processing** group.

### Apply setup-based drivers

Add steps in this group to install setup-based drivers (.exe) from packages.

### Install/enable third-party security

Add steps in this group to install or enable third-party security programs, such as antivirus.

### Set Windows default apps and associations

Add steps in this group to set Windows default apps and file associations.

1. Prepare a reference computer with app associations you want.

1. Run the following command line to export:

    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`

1. Add the XML file to a package.

1. Add a [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) step in this group. Specify the package that contains the XML file, and then specify the following command line:

    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`

For more information, see [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).

### Apply customizations and personalization

Add steps in this group to apply Start menu customizations, such as organizing program groups. For more information, see [Customize the Start layout](/windows-hardware/customize/desktop/customize-start-layout).

## Optional task sequence steps for rollback  

When something goes wrong with the upgrade process after the computer restarts, Windows Setup rolls back the system to the previous OS. The task sequence then continues with any steps in the **Rollback** group. After you create the task sequence, add optional steps in this group as necessary. For example, reverse any changes made to the system in the Prepare for Upgrade group, such as uninstalling incompatible software.

## Recommended task sequence steps on failure

<!--1358500-->
The default task sequence template for Windows 10 in-place upgrade includes a group to **Run actions on failure**. This group includes recommended actions to add in case the upgrade process fails. These actions make it easier to troubleshoot.

### Collect logs

To gather logs from the client, add steps in this group.

- A common practice is to copy the log files to a network share. To establish this connection, use the [Connect to Network Folder](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) step.

- To do the copy operation, use a custom script or utility with either the [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) or [Run PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) step.

- Files to collect might include the following logs:
     `%_SMSTSLogPath%\*.log`
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`

- For more information on setupact.log and other Windows Setup logs, see [Windows Setup Log files](/windows/deployment/upgrade/log-files).

- For more information on Configuration Manager client logs, see [Configuration Manager client logs](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).

- For more information on **_SMSTSLogPath** and other useful variables, see [Task sequence variables](../understand/task-sequence-variables.md).

### Run diagnostic tools

To run diagnostic tools, add steps in this group. Automate these tools for collecting additional information from the system right after the failure.

One such tool is Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). It's a standalone diagnostic tool to obtain details about why a Windows 10 upgrade was unsuccessful.

- In Configuration Manager, [create a package](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) for the tool.

- Add a [Run Command Line](../understand/task-sequence-steps.md#BKMK_RunCommandLine) step to this group of your task sequence. Use the **Package** option to reference the tool. The following string is an example **Command line**:
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`

> [!TIP]
> Always use the most recent version of SetupDiag for the latest functionality and fixes to known issues. For more information, see [SetupDiag](/windows/deployment/upgrade/setupdiag).

## Other recommendations

### Windows documentation

Review Windows documentation to [Resolve Windows 10 upgrade errors](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). This article also includes detailed information about the upgrade process.

### Check minimum disk space

On the default **Check Readiness** step, enable **Ensure minimum free disk space (MB)**. Set the value to at least **16384** (16 GB) for a 32-bit OS upgrade package, or **20480** (20 GB) for 64-bit.

### Retry downloading policy

Use the **SMSTSDownloadRetryCount** [task sequence variable](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) to retry downloading policy. Currently by default, the client retries twice; this variable is set to two (2). If your clients aren't on a wired intranet network connection, more retries help the client obtain policy. Using this variable causes no negative side effect, other than delayed failure if it can't download policy.<!--501016--> Also increase the **SMSTSDownloadRetryDelay** variable from the default 15 seconds.

### Do an inline compatibility assessment

1. Add a second **Upgrade Operating System** step early in the **Prepare for Upgrade** group.

    1. Name it *Upgrade assessment*.

    1. Specify the same upgrade package, and then enable the option to **Perform Windows Setup compatibility scan without starting upgrade**.

    1. Enable **Continue on error** on the Options tab.

1. Immediately following this *Upgrade assessment* step, add a **Run Command Line** step. Specify the following command line:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

    This command causes the command prompt to exit with the specified non-zero exit code, which the task sequence considers a failure.

1. On the **Options** tab, add the following condition:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

    This condition means that the task sequence only runs this **Run Command Line** step if the return code isn't a success code.

The return code `3247440400` is the decimal equivalent of MOSETUP_E_COMPAT_SCANONLY (0xC1900210), which is a successful compatibility scan with no issues. If the *Upgrade Assessment* step succeeds and returns `3247440400`, the task sequence skips this **Run Command Line** step, and continues. If the assessment step returns any other return code, this **Run Command Line** step runs. Because the command exits with a non-zero return code, the task sequence also fails. The task sequence log and status messages include the return code from the Windows Setup compatibility scan. For more information on **_SMSTSOSUpgradeActionReturnCode**, see [Task sequence variables](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

For more information, see the [Upgrade operating system](../understand/task-sequence-steps.md#BKMK_UpgradeOS) task sequence step.

### Convert from BIOS to UEFI

If you want to change the device from BIOS to UEFI during this task sequence, see [Convert from BIOS to UEFI during an in-place upgrade](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### Manage BitLocker

<!--SCCMDocs issue #494-->
If you're using BitLocker Disk Encryption, then by default Windows Setup automatically suspends it during upgrade. Starting in Windows 10 version 1803, Windows Setup includes the `/BitLocker` command-line parameter to control this behavior. If your security requirements need devices to always have active disk encryption, then use the **OSDSetupAdditionalUpgradeOptions** [task sequence variable](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) in the **Prepare for Upgrade** group to include `/BitLocker TryKeepActive`. For more information, see [Windows Setup Command-line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### Remove default apps

<!--SCCMDocs issue #526-->
Some customers remove default provisioned apps in Windows 10. For example, the Bing Weather app, or the Microsoft Solitaire Collection. In some situations, these apps return after updating Windows 10. For more information, see [How to keep apps removed from Windows 10](/windows/application-management/remove-provisioned-apps-during-update).

Add a **Run Command Line** step to the task sequence in the **Prepare for Upgrade** group. Specify a command line similar to the following example:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`

## Next steps

[Deploy the task sequence](deploy-a-task-sequence.md), [Deploy the task sequence over the internet](deploy-task-sequence-over-internet.md), or [Create a phased deployment](create-phased-deployment-for-task-sequence.md).

The pre-cache feature for available deployments of task sequences lets clients download relevant OS upgrade package content before a user installs the task sequence. For more information, see [Configure pre-cache content](configure-precache-content.md).<!--1021244-->
