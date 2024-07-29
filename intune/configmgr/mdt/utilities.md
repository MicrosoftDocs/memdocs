---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Utilities
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Utilities
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: frankroj,mstewart,aaroncz
---

# Utilities

The scripts used in LTI and ZTI reference utilities that perform specialized tasks supporting the steps used during the deployment process. Use the following information to help determine the correct utilities to include in actions and the valid arguments to provide when running each utility.

The following information is provided for each utility:

- **Name**. Specifies the name of the utility

- **Description**. Provides a description of the purpose of the utility

- **Location**. Indicates the folder where the utility can be found; in the information for the location, the following variables are used:

  - **program_files**. This variable points to the location of the Program Files folder on the computer where MDT is installed.

  - **distribution**. This variable points to the location of the Distribution folder for the deployment share.

  - **platform**. This variable is a placeholder for the operating system platform (x86 or x64).

- **Use**.Provides the commands and options that can be specified

- **Arguments and description**.Indicates the valid arguments to be specified for the utility and a brief description of what each argument means

## BCDBoot.exe

BCDBoot is a tool used to quickly set up a system partition or repair the boot environment located on the system partition. The system partition is set up by copying a small set of boot environment files from an installed Windows image. BCDBoot also creates a Boot Configuration Data (BCD) store on the system partition, with a new boot entry that enables Windows to boot to the installed Windows image.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|

### Arguments

|**Value**|**Description**|
|-|-|
||See the command-line help provided by this utility.|

## BDDRun.exe

This utility is run as an action by the Task Sequencer for executables (such as a script or other code) that require user interaction. By default, the task sequence cannot run an executable that requires user interaction. However, this utility allows the Task Sequencer to run an executable that requires user interaction.

 The executable that requires user interaction is provided as an argument to this utility. This utility runs the executable in a separate command environment.

> [!NOTE]
>
> This utility can only be used in LTI deployments. ZTI deployments prohibit any user interaction.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Tools\\*platform*|
|**Use**|`BDDRun.exe commandline`|

### Arguments

|**Value**|**Description**|
|-|-|
|*commandline*|The command to be run that requires user interaction|

> [!NOTE]
>
> Put double quotation marks around any part of the *command-line* portion of the argument that contains blanks. For example: `BDDRun.exe MyAppInstall.exe /destinationdir: "%ProgramFiles%\AppName"`.

## Bootsect.exe

Bootsect.exe updates the master boot code for hard disk partitions to switch between BOOTMGR and NTLDR. Use this utility to restore the boot sector on the computer.

 For more information on Bootsect.exe, see the section, "Bootsect Command-Line Options," in the *Windows Preinstallation Environment (Windows PE) User's Guide*.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Tools\\*platform*|
|**Use**|`bootsect.exe /nt52 C:`|

### Arguments

|**Value**|**Description**|
|-|-|
|**/Help**|Displays the use instructions listed here.|
|**/nt52**|Applies the master boot code compatible with NTLDR to **SYS**, **ALL**, or *DriveLetter*. The operating system installed on **SYS**, **ALL**, or *DriveLetter* must be an earlier version of Windows Vista.|
|**/nt60**|Applies the master boot code compatible with BOOTMGR to **SYS**, **ALL**, or *DriveLetter*. The operating system installed on **SYS**, **ALL**, or *DriveLetter* must be Windows Vista.|
|**SYS**|Updates the master boot code on the system partition used to boot Windows.|
|**All**|Updates the master boot code on all partitions. **ALL** does not necessarily update the boot code for each volume. Instead, this option updates the boot code on volumes that can be used as Windows boot volumes, which excludes any dynamic volumes not connected with an underlying disk partition. This restriction is present, because the boot code must be located at the beginning of a disk partition.|
|***DriveLetter***|Updates the master boot code on the volume associated with this drive letter. The boot code will not be updated if either (1) **DriveLetter** is not associated with a volume or (2) **DriveLetter** is associated with a volume not connected to an underlying disk partition.|
|**/Force**|Forcibly dismounts the volumes during the boot code update. Use this option with caution.|

## Compact.exe

Displays or alters the compression of files on NTFS file system partitions.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|

### Arguments

|**Value**|**Description**|
|-|-|
|**/C**|Compresses the specified files. Directories will be marked so that files added afterward will be compressed.|
|**/V**|Decompresses the specified files. Directories will be marked so that files added afterward will not be compressed.|
|**/S**|Performs the specified operation on files in the given directory and in all subdirectories. Default dir is the current directory.|
|**/A**|Displays files with the hidden or system attributes. These files are omitted by default.|
|**/I**|Continues performing the specified operation even after errors have occurred. By default, Compact.exe stops when an error is encountered.|
|**/F**|Forces the compress operation on all specified files, even those which are already compressed. Already-compressed files are skipped by default.|
|**/Q**|Reports only the most essential information.|
|***filename***|Specifies a pattern, file, or directory.|

## Diskpart.exe

Diskpart is a text-mode command interpreter that allows management of objects (disks, partitions, or volumes) using scripts or direct input in a Command Prompt window.

 For more information on Diskpart.exe, see the section, "Diskpart Command-Line Options," in the *Windows Preinstallation Environment (Windows PE) User's Guide*.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows PE source files|

### Arguments

|**Value**|**Description**|
|-|-|
||See the guide referenced in the utility description.|

## Expand.exe

This utility is run to expand (extract) files from compressed files.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|
|**Use**|`Expand.exe -r wuredist.cab -F:wuRedist.xml %temp%`|

### Arguments

|     **Value**     |                                                                                  **Description**                                                                                   |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      **-r**       |                                                                               Renames expanded files                                                                               |
|      **-D**       |                                                                 Displays the list of files in the source directory                                                                 |
|   ***Source***    |                                                                 Source file specification (Wildcards can be used.)                                                                 |
|  **-F:*Files***   |                                                                      Name of files to expand from a .cab file                                                                      |
| ***Destination*** | Destination file &#124; path specification (**Destination** can be a directory. If **Source** is multiple files and **-r** is not specified, **Destination** must be a directory.) |

## ImageX.exe

ImageX is a command-line utility that enables OEMs and corporations to capture, modify, and apply file-based disk images for rapid deployment. ImageX works with WIM files for copying to a network, or it can work with other technologies that use WIM images, such as Windows Setup and Windows Deployment Services.

 For more information about ImageX, see the section, "What is ImageX," in the *Windows Preinstallation Environment (Windows PE) User's Guide*.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Tools\\*platform*|

### Arguments

|**Value**|**Description**|
|-|-|
||See the guide referenced in the utility description.|

## Microsoft.BDD.PnpEnum.exe

This utility is run to enumerate Plug and Play devices installed on the target computer.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Tools\\*platform*|

### Arguments

|**Value**|**Description**|
|-|-|
|None|-|

## Mofcomp.exe

Mofcomp.exe is the Managed Object Format compiler that parses a file that contains Managed Object Format statements and adds the classes and class instances defined in the file to the WMI repository. Mofcomp.exe provides command-line help on the switch use options.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|

### Arguments

|**Value**|**Description**|
|-|-|
||See the command-line help that this utility provides.|

## Netsh.exe

Netsh.exe is a command-line and scripting utility used to automate the configuration of networking components. For more information about Netsh.exe, see [The Netsh Command-Line Utility](/previous-versions/windows/it-pro/windows-server-2003/cc785383(v=ws.10)).

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|

### Arguments

|**Value**|**Description**|
|-|-|
||See the command-line help that this utility provides or the information found at the URL listed in the utility description.|

## Reg.exe

The Console Registry Tool is used to read and modify registry data.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|

### Arguments

|**Value**|**Description**|
|-|-|
||See the command-line help that this utility provides.|

## Regsvr32.exe

This utility is used to register files (.dll, .exe, .ocx, and so on) with the operating system.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows source files|

### Arguments

|**Value**|**Description**|
|-|-|
|***file***|The name of the file to register or unregister|
|**/s**|Runs the utility in silent mode|
|**/u**|Unregisters the file|

## Wpeutil.exe

The Windows PE utility (Wpeutil) is a command-line utility with which various commands can be run in a Windows PE session. For example, an administrator can shut down or reboot Windows PE, activate or deactivate a firewall, configure language settings, and initialize a network. MDT uses the utility to initialize Windows PE and network connections, and start LTI deployments.

 For more information on Wpeutil.exe, see the section, "Wpeutil Command-Line Options," in the *Windows Preinstallation Environment (Windows PE) User's Guide*.

|**Value**|**Description**|
|-|-|
|**Location**|Included in the Windows PE source files|

### Arguments

|**Value**|**Description**|
|-|-|
||See the guide referenced in the utility description.|

## Related articles

- [Task Sequence Steps](task-sequence-steps.md).
- [Properties](properties.md).
- [Scripts](scripts.md).
- [Support Files](support-files.md).
- [MDT Windows PowerShell Cmdlets](mdt-windows-powershell-cmdlets.md).
- [Tables and Views in the MDT DB](tables-views-mdt-db.md).
- [Windows 7 Feature Dependency Reference](windows-7-feature-dependency.md).
- [UDI Reference](udi-reference.md).