---
title: In-place upgrade recommendations
titleSuffix: Configuration Manager
description: Recommended steps for using the task sequence to upgrade Windows.
ms.date: 10/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# In-place upgrade recommendations

*Applies to: Configuration Manager (current branch)*

The default task sequence template for Windows in-place upgrade includes groups with recommended actions to add before and after the upgrade process. These actions are common among many customers who are successfully upgrading Windows on devices. This article provides information about these recommended steps during different phases of the upgrade process.

## Prepare for upgrade

If you have an existing task sequence that doesn't already have these actions, manually add them to your task sequence in the **Prepare for Upgrade** group.

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

Add steps in this group to remove any applications that are incompatible with the target version of Windows. The method to uninstall an application varies.

If the application uses Windows Installer, copy the **Uninstall program** command line from the **Programs** tab on the Windows Installer deployment type properties of the application. Then add a **Run Command Line** step in this group with the uninstall program command line. For example:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`

### Remove incompatible drivers

Add steps in this group to remove any drivers that are incompatible with the target version of Windows.

### Remove/suspend third-party security

Add steps in this group to remove or suspend third-party security programs, such as antivirus.

If you're using a third-party disk encryption program, provide its encryption driver to Windows Setup with the `/ReflectDrivers` [command-line option](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Add a [Set Task Sequence Variable](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step to the task sequence in this group. Set the task sequence variable to **OSDSetupAdditionalUpgradeOptions**. Set the value to `/ReflectDrivers` with the path to the driver. This [task sequence variable](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) appends the Windows Setup command-line used by the task sequence. Contact your software vendor for any further guidance on this process.

### Download Package Content task sequence step

Use the [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) step before the **Upgrade Operating System** step in the following scenarios:

- You use a single upgrade task sequence for both x86 and x64 platforms. Include two **Download Package Content** steps in the **Prepare for Upgrade** group. Set conditions on each step to detect the client architecture. This condition causes the step to download only the appropriate OS upgrade package. Configure each **Download Package Content** step to use the same variable, and use the variable for the media path on the **Upgrade Operating System** step.

- To dynamically download an applicable driver package, use two **Download Package Content** steps with conditions to detect the appropriate hardware type for each driver package. Configure each **Download Package Content** step to use the same variable. Then use that variable for the **Staged content** value in the drivers section on the **Upgrade Operating System** step.

    > [!NOTE]
    > Configuration Manager adds a numerical suffix to this variable name. For example, if you specify `%mycontent%` as a custom variable, the client stores all referenced content in this location. When you refer to the variable in a subsequent step, such as **Upgrade Operating System**, use the variable with a numerical suffix. In this example, `%mycontent01%` or `%mycontent02%`, where the number corresponds to the order in which the **Download Package Content** step lists this specific content.

## Post-processing

After you create the task sequence, add more steps in the **Post-Processing** group of the task sequence.  

> [!NOTE]  
> This task sequence isn't linear. There are conditions on steps that can affect the results of the task sequence. This behavior depends on whether it successfully upgrades the client computer, or if it has to roll back the client computer to the original OS.

The default task sequence template for Windows in-place upgrade includes other groups with recommended actions to add after the upgrade process. These actions in the **Post-Processing** group are common among many customers who are successfully upgrading Windows on devices. If you have an existing task sequence that doesn't already have these actions, manually add them to your task sequence in the **Post-Processing** group.

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

1. Add a [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step in this group. Specify the package that contains the XML file, and then specify the following command line:

    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`

For more information, see [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).

### Apply customizations and personalization

Add steps in this group to apply Start menu customizations, such as organizing program groups. For more information, see [Customize the Start layout](/windows-hardware/customize/desktop/customize-start-layout).

## Rollback  

When something goes wrong with the upgrade process after the computer restarts, Windows Setup rolls back the system to the previous OS. The task sequence then continues with any steps in the **Rollback** group. After you create the task sequence, add optional steps in this group as necessary. For example, reverse any changes made to the system in the Prepare for Upgrade group, such as uninstalling incompatible software.

## Run actions on failure

<!--1358500-->
The default task sequence template for Windows in-place upgrade includes a group to **Run actions on failure**. This group includes recommended actions to add in case the upgrade process fails. These actions make it easier to troubleshoot.

### Collect logs

To gather logs from the client, add steps in this group.

- A common practice is to copy the log files to a network share. To establish this connection, use the [Connect to Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) step.

- To do the copy operation, use a custom script or utility with either the [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) or [Run PowerShell Script](task-sequence-steps.md#BKMK_RunPowerShellScript) step.

- Files to collect might include the following logs:
     `%_SMSTSLogPath%\*.log`
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`

- For more information on setupact.log and other Windows Setup logs, see [Windows Setup Log files](/windows/deployment/upgrade/log-files).

- For more information on Configuration Manager client logs, see [Configuration Manager client logs](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs).

- For more information on **_SMSTSLogPath** and other useful variables, see [Task sequence variables](task-sequence-variables.md).

### Run diagnostic tools

To run diagnostic tools, add steps in this group. Automate these tools for collecting additional information from the system right after the failure.

One such tool is Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). It's a standalone diagnostic tool to get details about why a Windows upgrade was unsuccessful.

- In Configuration Manager, [create a package](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) for the tool.

- Add a [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step to this group of your task sequence. Use the **Package** option to reference the tool. The following string is an example **Command line**:
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log"`

> [!TIP]
> Always use the most recent version of SetupDiag for the latest functionality and fixes to known issues. For more information, see [SetupDiag](/windows/deployment/upgrade/setupdiag).

## Other recommendations

### Windows documentation

Review Windows documentation to [Resolve Windows client upgrade errors](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). This article also includes detailed information about the upgrade process.

### Check minimum disk space

On the default **Check Readiness** step, enable **Ensure minimum free disk space (MB)**. Set the value to at least **16384** (16 GB) for a 32-bit OS upgrade package, or **20480** (20 GB) for 64-bit.

### Retry downloading policy

Use the **SMSTSDownloadRetryCount** [task sequence variable](task-sequence-variables.md#SMSTSDownloadRetryCount) to retry downloading policy. Currently by default, the client retries twice; this variable is set to two (2). If your clients aren't on a wired intranet network connection, more retries help the client obtain policy. Using this variable causes no negative side effect, other than delayed failure if it can't download policy.<!--501016--> Also increase the **SMSTSDownloadRetryDelay** variable from the default 15 seconds.

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

The return code `3247440400` is the decimal equivalent of MOSETUP_E_COMPAT_SCANONLY (0xC1900210), which is a successful compatibility scan with no issues. If the *Upgrade Assessment* step succeeds and returns `3247440400`, the task sequence skips this **Run Command Line** step, and continues. If the assessment step returns any other return code, this **Run Command Line** step runs. Because the command exits with a non-zero return code, the task sequence also fails. The task sequence log and status messages include the return code from the Windows Setup compatibility scan. For more information on **_SMSTSOSUpgradeActionReturnCode**, see [Task sequence variables](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode).

For more information, see the [Upgrade operating system](task-sequence-steps.md#BKMK_UpgradeOS) task sequence step.

### Convert from BIOS to UEFI

If you want to change the device from BIOS to UEFI during this task sequence, see [Convert from BIOS to UEFI during an in-place upgrade](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### Manage BitLocker

<!--SCCMDocs issue #494-->
If you're using BitLocker Disk Encryption, then by default Windows Setup automatically suspends it during upgrade. Windows Setup includes the `/BitLocker` command-line parameter to control this behavior. If your security requirements need devices to always have active disk encryption, then use the **OSDSetupAdditionalUpgradeOptions** [task sequence variable](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) in the **Prepare for Upgrade** group to include `/BitLocker TryKeepActive`. For more information, see [Windows Setup Command-line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker).

### Remove default apps

<!--SCCMDocs issue #526-->
Some customers remove default provisioned apps in Windows. For example, the Bing Weather app, or the Microsoft Solitaire Collection. In some situations, these apps return after upgrading Windows. For more information, see [How to keep apps removed from Windows client from returning during an update](/windows/application-management/remove-provisioned-apps-during-update).

Add a **Run Command Line** step to the task sequence in the **Prepare for Upgrade** group. Specify a command line similar to the following example:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`

## Next steps

For more information, see the following articles:

- [Upgrade Windows to the latest version](../deploy-use/upgrade-windows-to-the-latest-version.md)
- [Create a task sequence to upgrade an OS](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
- [About task sequence steps: Upgrade OS](task-sequence-steps.md#BKMK_UpgradeOS)
