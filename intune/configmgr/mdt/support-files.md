---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Support Files
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Support Files
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: frankroj,mstewart,aaroncz
---

# Support Files

The utilities and scripts used in LTI and ZTI deployments reference external configuration files to determine the process steps and configuration settings used during the deployment process.

 The following information is provided for each utility:

- **Name**. Specifies the name of the file

- **Description**. Provides a description of the purpose of the file

- **Location**. Indicates the folder where the file can be found; in the information for the location, the following variables are used:

  - **program_files**. This variable points to the location of the Program Files folder on the computer where MDT is installed.

  - **distribution**. This variable points to the location of the Distribution folder for the deployment share.

  - **platform**. This variable is a placeholder for the operating system platform (x86 or x64).

## ApplicationGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## Applications.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## BootStrap.ini

The configuration file used when the target computer is not able to connect to the appropriate deployment share. This situation occurs in the New Computer and the Replace Computer scenarios.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## CustomSettings.ini

The primary configuration file for the MDT processing rules used in all scenarios.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## Deploy.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*program_files*\Microsoft Deployment Toolkit\Control|

## DriverGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## Drivers.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|Description|
|-|-|
|**Location**|*distribution*\Control|

## LinkedDeploymentShares.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## ListOfLanguages.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## MediaGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## Medias.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## OperatingSystemGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## OperatingSystems.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## PackageGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## Packages.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## SelectionProfileGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## SelectionProfiles.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## ServerManager.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*program_files*\Microsoft Deployment Toolkit\Bin|

## Settings.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## TaskSequenceGroups.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## TaskSequences.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control|

## TS.xml

> [!NOTE]
>
> This XML file is managed by MDT and should not require modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Control\\*task_sequence_id*|

> [!NOTE]
>
> *Task_sequence_id* is a placeholder for the task sequence ID that was assigned to each task sequence when it was created in the Task Sequences node in the Deployment Workbench.

## Wimscript.ini

This .ini file is an ImageX configuration file that contains the list of folders and files that will be excluded from an image. It is referenced by ImageX during the LTI Capture Phase.

 For assistance with customizing this file, see the section, "Create an ImageX Configuration File," in the *Windows Preinstallation Environment (Windows PE) User's Guide*.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Tools\\*platform*|

## ZTIBIOSCheck.xml

This XML file contains metadata about BIOSes for target computers. This file is edited manually and is read by [ZTIBIOSCheck.wsf](scripts.md#ztibioscheckwsf). Extract the necessary information from a target computer to create an entry in this XML file using the Microsoft Visual Basic&reg; Scripting Edition (VBScript) program (ZTIBIOS_Extract_Utility.vbs) that is embedded in this XML file.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## ZTIConfigure.xml

This XML file is used by the [ZTIConfigure.wsf](scripts.md#zticonfigurewsf) script to translate property values (specified earlier in the deployment process) to configure settings in the Unattend.xml file. This file is already customized to make the appropriate translations and should not require further modification.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## ZTIGather.xml

> [!NOTE]
>
> This XML file is preconfigured and should not require modification. Define custom properties in the CustomSettings.ini file or the MDT DB.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## ZTIUserState_config.xml

This XML file is used by the [ZTIUserState.wsf](scripts.md#ztiuserstatewsf) script as a default USMT configuration file. This file is used by default if no custom configuration file is specified by the [USMTConfigFile](properties.md#usmtconfigfile) property. See the [Config.xml File](/windows/deployment/usmt/usmt-configxml-file) topic in the USMT documentation for more information on syntax and use.

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## ZTITatoo.mof

This .mof file, when imported into the WMI repository of the target computer using Mofcomp.exe, creates the **Microsoft_BDD_Info** WMI class. This class contains deployment-related information, such as:

- DeploymentMethod

- DeploymentType

- DeploymentTimestamp

- BuildID

- BuildName

- BuildVersion

- OSDPackageID

- OSDProgramName

- OSDAdvertisementID

- TaskSequenceID

- TaskSequenceName

- TaskSequenceVersion

|**Value**|**Description**|
|-|-|
|**Location**|*distribution*\Scripts|

## Related articles

- [Task Sequence Steps](task-sequence-steps.md).
- [Properties](properties.md).
- [Scripts](scripts.md).
- [Utilities](utilities.md).
- [MDT Windows PowerShell Cmdlets](mdt-windows-powershell-cmdlets.md).
- [Tables and Views in the MDT DB](tables-views-mdt-db.md).
- [Windows 7 Feature Dependency Reference](windows-7-feature-dependency.md).
- [UDI Reference](udi-reference.md).