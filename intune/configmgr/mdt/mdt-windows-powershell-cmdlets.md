---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Windows PowerShell Cmdlets
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Windows PowerShell Cmdlets
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

# MDT Windows PowerShell Cmdlets

In addition to the Deployment Workbench, MDT deployment shares can be managed using Windows PowerShell cmdlets. The MDT Windows PowerShell cmdlets are included in a Windows PowerShell snap-in—Microsoft.BDD.PSSnapIn—which is included with the installation of MDT.

The MDT cmdlets must be run from a Windows PowerShell console that has the MDT Windows PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT Windows PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

Table 7 lists the MDT Windows PowerShell cmdlets and provides a brief description of each cmdlet. Each cmdlet is discussed in further detail in a subsequent section.

## Table 7. MDT Windows PowerShell Cmdlets

|**Cmdlet**|**Description**|
|-|-|
|[Add-MDTPersistentDrive](#add-mdtpersistentdrive)|Adds a deployment share to the list of MDT persisted drives that can be restored using the [Restore-MDTPersistentDrive](#restore-mdtpersistentdrive) cmdlet.|
|[Disable-MDTMonitorService](#disable-mdtmonitorservice)|Disables the MDT monitoring services.|
|[Enable-MDTMonitorService](#enable-mdtmonitorservice)|Enables the MDT monitoring services.|
|[Get-MDTDeploymentShareStatistics](#get-mdtdeploymentsharestatistics)|Displays the statistics of a deployment share, including the number of entities per major folder in the deployment share.|
|[Get-MDTMonitorData](#get-mdtmonitordata)|Displays the MDT monitoring information collected for one or more monitored MTD deployments.|
|[Get-MDTOperatingSystemCatalog](#get-mdtoperatingsystemcatalog)|Returns the operating system catalog for a specific operating system. If the operating system catalog does not exist or is out of date, then the operating system catalog is regenerated.|
|[Get-MDTPersistentDrive](#get-mdtpersistentdrive)|Displays the list of deployment shares that can be restored using the [Restore-MDTPersistentDrive](#restore-mdtpersistentdrive) cmdlet.|
|[Import-MDTApplication](#import-mdtapplication)|Imports an application into a deployment share.|
|[Import-MDTDriver](#import-mdtdriver)|Imports one or more device drivers into a deployment share.|
|[Import-MDTOperatingSystem](#import-mdtoperatingsystem)|Imports one or more operating systems into a deployment share.|
|[Import-MDTPackage](#import-mdtpackage)|Imports one or more operating system packages into a deployment share.|
|[Import-MDTTaskSequence](#import-mdttasksequence)|Imports a task sequence into a deployment share.|
|[New-MDTDatabase](#new-mdtdatabase)|Creates or upgrades an MDT DB database that is associated with a deployment share.|
|[Remove-MDTMonitorData](#remove-mdtmonitordata)|Removes one or more MDT monitoring data items from the collected MDT monitoring data in a deployment share.|
|[Remove-MDTPersistentDrive](#remove-mdtpersistentdrive)|Removes a deployment share from the list of MDT persisted Windows PowerShell drives that can be restored using the [Restore-MDTPersistentDrive](#restore-mdtpersistentdrive) cmdlet.|
|[Restore-MDTPersistentDrive](#restore-mdtpersistentdrive)|Creates a Windows PowerShell drive for each deployment share in the list of MDT persisted Windows PowerShell drives.|
|[Set-MDTMonitorData](#set-mdtmonitordata)|Creates a new or updates an existing MDT monitoring data item in the collected MDT monitoring data in a deployment share.|
|[Test-MDTDeploymentShare](#test-mdtdeploymentshare)|Verifies the integrity of a deployment share.|
|[Test-MDTMonitorData](#test-mdtmonitordata)|Verifies that the MDT monitoring services is configured correctly and running.|
|[Update-MDTDatabaseSchema](#update-mdtdatabaseschema)|Updates the MDT DB database schema.|
|[Update-MDTDeploymentShare](#update-mdtdeploymentshare)|Updates a deployment share.|
|[Update-MDTLinkedDS](#update-mdtlinkedds)|Replicates content from a deployment share to a linked deployment share.|
|[Update-MDTMedia](#update-mdtmedia)|Replicates content from a deployment share to a deployment media folder.|

## Add-MDTPersistentDrive

This section describes the **Add-MDTPersistentDriveWindows PowerShell** cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Add-MDTPersistentDrive [-Name] <String> [[-InputObject] <PSObject>] [<CommonParameters>]
```

### Description

This cmdlet adds an existing Windows PowerShell drive created using the **MDTProvider** to a list of drives that are persisted in the Deployment Workbench or in a Windows PowerShell session using the [Restore-MDTPersistentDrive](#restore-mdtpersistentdrive) cmdlet. This cmdlet is called when you create or open a deployment share in the Deployment Workbench.

> [!NOTE]
>
> The list of persisted **MDTProvider** drives is maintained on a per-user based in the user profile.

 The list of persisted **MDTProvider** drives can be displayed using the **Get-MDTPersistentDrive** cmdlet.

### Parameters

This subsection provides information about the various parameters that can be used with the **Add-MDTPersistentDriveWindows** cmdlet.

#### -Name <String\>

Specifies the name of a Windows PowerShell drive created using the MDT provider and corresponds to an existing deployment share. The name was created using the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet and specifying the **MDTProvider** in the *PSProvider* parameter.

 For more information on how to create a new Windows PowerShell drive using the **MDTProvider** and how to create a deployment share using Windows PowerShell, see the section "Creating a Deployment Share Using Windows PowerShell" in the MDT document, *Microsoft Deployment Toolkit Samples Guide*.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**2** and **Named**|
|**Default value**|None|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -InputObject <PSObject\>

This parameter specifies a Windows PowerShell drive object that was created earlier in the process. Enter a PSObject object, such as one generated by the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**3** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object for the Windows PowerShell drive object was added to the list of persisted drives.

 This cmdlet also outputs a **String** type object if the *Verbose* common parameter is included.

### Example 1

```powershell
Add-MDTPersistentDrive -Name DS001
```

#### Description

This example adds the deployment share with the Windows PowerShell drive name of *DS001* to the list of persisted drives.

### Example 2

```powershell
$MDTPSDrive = New-PSDrive -Name "DS001" -PSProvider "MDTProvider" -Root "C:\DeploymentShare$" -Description "MDT Deployment Share" -NetworkPath \\WDG-MDT-01\DeploymentShare$ -Verbose
Add-MDTPersistentDrive -InputObject $MDTPSDrive
```

#### Description

This example adds the Windows PowerShell drive name *DS001,* created by the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet, to the list of persisted MDT drives using the *$MDTPSDrive* variable.

### Example 3

```powershell
New-PSDrive -Name "DS001" -PSProvider "MDTProvider" -Root "C:\DeploymentShare$" -Description "MDT Deployment Share" -NetworkPath \\WDG-MDT-01\DeploymentShare$ -Verbose | Add-MDTPersistentDrive -Verbose
```

#### Description

This example adds the Windows PowerShell drive name *DS001,* created by the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet, to the list of persisted MDT drives by piping the newly created Windows PowerShell drive object to the **Add-MDTPersistentDrive** cmdlet.

## Disable-MDTMonitorService

This section describes the **Disable-MDTMonitorService** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Disable-MDTMonitorService [<CommonParameters>]
```

### Description

This cmdlet disables the MDT monitoring service, which runs on the computer where MDT is installed. The MDT monitoring service collects monitoring information that can be displayed:

- In the Monitoring node in a deployment share in the Deployment Workbench

- Using the [Get-MDTMonitorData](#get-mdtmonitordata) cmdlet

  The MDT monitoring service can subsequently be enabled using the [Enable-MDTMonitorService](#enable-mdtmonitorservice).

  For more information on the MDT monitoring service, see the section "Monitoring MDT Deployments" in the MDT document, *Using the Microsoft Deployment Toolkit*.

### Parameters

This subsection provides information about the various parameters that can be used with the **Disable-MDTMonitorService** cmdlet.

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can accessed by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **String** type object if the *Verbose* common parameter is included; otherwise, no output is generated.

### Example 1

```powershell
Disable-MDTMonitorService
```

#### Description

This example disables the MDT monitoring service.

## Enable-MDTMonitorService

This section describes the **Enable-MDTMonitorService** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Enable-MDTMonitorService [-EventPort] <Int32> [-DataPort] <Int32> [<CommonParameters>]
```

### Description

This cmdlet enables the MDT monitoring service, which runs on the computer where MDT is installed. The MDT monitoring service collects monitoring information that can be displayed:

- In the Monitoring node in a deployment share in the Deployment Workbench.

- Using the [Get-MDTMonitorData](#get-mdtmonitordata) cmdlet

  The MDT monitoring service can be disabled using the [Disable-MDTMonitorService](#disable-mdtmonitorservice).

  For more information on the MDT monitoring service, see the section "Monitoring MDT Deployments" in the MDT document, *Using the Microsoft Deployment Toolkit*.

### Parameters

This subsection provides information about the various parameters that can be used with the **Enable-MDTMonitorService** cmdlet.

#### -EventPort <Int32\>

This parameter specifies the TCP port used as the event port for the MDT monitoring service.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**2** and **Named**|
|**Default value**|**9800**|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -DataPort <Int32\>

This parameter specifies the TCP port used as the data port for the MDT monitoring service.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**3** and **Named**|
|**Default value**|**9801**|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **String** type object if the *Verbose* common parameter is included; otherwise, no output is generated.

### Example 1

```powershell
Enable-MDTMonitorService
```

#### Description

This example enables the MDT monitoring service on the local computer using the default value of **9800** for the event port and the value of **9801** for the data port on the MDT monitoring service.

### Example 2

```powershell
Enable-MDTMonitorService -EventPort 7000 -DataPort 7001
```

#### Description

This example enables the MDT monitoring service on the local computer using the value of **7000** for the event port and the value of **7001** for the data port on the MDT monitoring service.

## Get-MDTDeploymentShareStatistics

This section describes the **Get-MDTDeploymentShareStatistics** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Get-MDTDeploymentShareStatistics [-Path <String>] [<CommonParameters>]
```

### Description

This cmdlet displays the statistics of a deployment share based on the MDTProvder drive that is specified in the *Path* parameter. The statistics include the number of items in the specified deployment share:

- Applications

- Drivers

- Operating Systems

- Packages

- Task Sequences

- Selection Profiles

- Linked Deployment Shares

- MDT Media

- Computers in the MDT DB

- Make and Models in the MDT DB

- Locations in the MDT DB

- Roles in the MDT DB

> [!NOTE]
>
> The values for the statistics that relate to the MDT DB are not populated and always return a value of zero.

### Parameters

This subsection provides information about the various parameters that can be used with the **Get-MDTDeploymentShareStatistics** cmdlet.

#### -Path <String\>

This parameter specifies the MDTProvider Windows PowerShell drive for the desired deployment share.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to a location within the desired MDTProvider Windows PowerShell drive.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**2** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object that contains the statistics for the deployment share.

### Example 1

```powershell
Get-MDTDeploymentShareStatistics -Path DS001:
```

#### Description

This example returns the deployment share statistics for the deployment share that is specified in the DS001: MDTProvider Windows PowerShell drive.

### Example 2

```powershell
cd DS001:
Get-MDTDeploymentShareStatistics
```

#### Description

This example returns the deployment share statistics for the deployment share that is specified in the DS001: MDTProvider Windows PowerShell drive. Use the **cd** command to set the working directory for Windows PowerShell to the DS001: MDTProvider Windows PowerShell drive.

## Get-MDTMonitorData

This section describes the **Get-MDTMonitorData** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Get-MDTMonitorData [-Path <String>] [-ID <Nullable>] [<CommonParameters>]
```

### Description

This cmdlet displays the MDT monitoring data that is being reported to the deployment share that is specified in the *Path* parameter. The following is example output from this cmdlet:

```powershell
Name               : WDG-REF-01
PercentComplete    : 100
Settings           :
Warnings           : 0
Errors             : 0
DeploymentStatus   : 3
StartTime          : 5/23/2012 6:45:39 PM
EndTime            : 5/23/2012 8:46:32 PM
ID                 : 1
UniqueID           : 94a0830e-f2bb-421c-b1e0-6f86f9eb9fa1
CurrentStep        : 88
TotalSteps         : 88
StepName           :
LastTime           : 5/23/2012 8:46:32 PM
DartIP             :
DartPort           :
DartTicket         :
VMHost             : WDG-HOST-01
VMName             : WDG-REF-01
ComputerIdentities : {}

```

> [!NOTE]
>
> The MDTProvider Windows PowerShell drive that this cmdlet references must exist prior to running this cmdlet.

### Parameters

This subsection provides information about the various parameters that you can use with the **Get- MDTMonitorData** cmdlet.

#### -Path <String\>

This parameter specifies the MDTProvider Windows PowerShell drive for the desired deployment share.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to a location within the desired MDTProvider Windows PowerShell drive.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**2** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ID <Nullable\>

This parameter specifies the specific identifier for the deployment of a specific computer. If this parameter is not specified, then all monitoring data for deployments in the deployment share are displayed.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**3** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object for each monitored computer, which contains the monitoring data for the computer.

### Example 1

```powershell
Get-MDTMonitorData -Path DS001:
```

#### Description

This example returns the monitoring data for all deployments in the deployment share that is specified in the DS001: MDTProvider Windows PowerShell drive.

### Example 2

```powershell
cd DS001:
Get-MDTMonitorData
```

#### Description

This example returns the monitoring data for all deployments in the deployment share that is specified in the DS001: MDTProvider Windows PowerShell drive. Use the **cd** command to set the working directory for Windows PowerShell to the DS001: MDTProvider Windows PowerShell drive.

### Example 3

```powershell
Get-MDTMonitorData -Path DS001: -ID 22
```

#### Description

This example returns the monitoring data for the deployment with an ID of 22 in the deployment share that is specified in the DS001: MDTProvider Windows PowerShell drive.

## Get-MDTOperatingSystemCatalog

This section describes the **Get-MDTOperatingSystemCatalog** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Get-MDTOperatingSystemCatalog [-ImageFile] <String> [-Index] <Int32> [<CommonParameters>]
```

### Description

This cmdlet retrieves or creates an operating system catalog for a custom operating system image so that you can modify the corresponding unattend.xml file using Windows System Image Manager (WSIM). If no operating system catalog is available or if the existing operating system catalog is invalid or out of date, this cmdlet will generate a new operating system catalog.

> [!NOTE]
>
> The process of generating a new operating system catalog may take a long time as the custom operating system image must be mounted, inspected, and unmounted before the operating system catalog creation completes.

### Parameters

This subsection provides information about the various parameters that can be used with the **Get-MDTOperatingSystemCatalog** cmdlet.

#### -ImageFile <String\>

This parameter specifies the fully qualified path to the custom operating system image file (.wim file), including the name of the custom operating system image file.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**2** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Index <Int32\>

This parameter specifies the index of the desired operating system image within the operating system image file (.wim file).

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**3** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object that contains the path to the operating system catalog.

### Example 1

```powershell
Get-MDTOperatingSystemCatalog -ImageFile "DS001:\Operating Systems\Windows 8\sources\install.wim" -Index 2
```

#### Description

This example returns the operating system catalog for the operating system image at the index of 2 in the operating system image file DS001:\Operating Systems\Windows 8\sources\install.wim.

## Get-MDTPersistentDrive

This section describes the **Get-MDTPersistentDrive** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Get-MDTPersistentDrive [<CommonParameters>]
```

### Description

This cmdlet displays the list of persisted MDT Windows PowerShell drives. The list of persisted MDT Windows PowerShell drives is managed using the [Add-MDTPersistentDrive](#add-mdtpersistentdrive) and [Remove-MDTPersistentDrive](#remove-mdtpersistentdrive) cmdlets or the Deployment Workbench.

 The output from this cmdlet contains the following information:

- Windows PowerShell drive name, such as DS001

- Directory path, such as \\\WDG-MDT-01\DeploymentShare$

  Persisted MDT Windows PowerShell drives are similar to persisted network drive mappings.

> [!NOTE]
>
> This list of persisted MDT Windows PowerShell drives is maintained on a per user basis and are stored in the user profile.

### Parameters

This subsection provides information about the various parameters that can be used with the **Get- MDTPersistentDrive** cmdlet.

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object for each MDT persisted drive that is identical to the **PSObject** type object that the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet returns.

### Example 1

```powershell
Get-MDTPersistentDrive
```

#### Description

This example displays a list of the MDT persisted drives.

## Import-MDTApplication

This section describes the **Import-MDTApplication** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Import-MDTApplication [-Path <String>] -Name <String> ApplicationSourcePath <String> -DestinationFolder <String> [-Move] [<CommonParameters>]
```

 -or-

```powershell
Import-MDTApplication [-Path <String>] -Name <String> NoSource [<CommonParameters>]
```

 -or-

```powershell
Import-MDTApplication [-Path <String>] -Name <String> Bundle [<CommonParameters>]
```

### Description

This cmdlet imports an application into a deployment share. The following application types can be imported using this cmdlet:

- Applications that have source files, using the *ApplicationSourcePath*, *DestinationFolder*, and *Move* parameters. The first syntax example illustrates the use of this cmdlet for this type of application.

- Applications without source files or with source files located on other network shared folders using the *NoSource* parameter. The second syntax example illustrates the use of this cmdlet for this type of application.

- Application bundles, which are used to group a set of related applications, using the *Bundle* parameter. The last syntax example illustrates the use of this cmdlet for this type of application.

### Parameters

This subsection provides information about the various parameters that can be used with the **Import-MDTApplication** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to an existing folder where the application being imported will be placed within the deployment share. If the *DestinationFolder* parameter is used, then the folder specified in the *DestinationFolder* parameter is created beneath the folder specified in this parameter. This parameter is used in all syntax usages for this cmdlet.

> [!NOTE]
>
> If this parameter is not provided, the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Name <String\>

This parameter specifies the name of the application to be added to the deployments share and must be unique within the deployment share. This parameter is used in all syntax usages for this cmdlet.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ApplicationSourcePath <String\>

This parameter specifies the fully qualified path to the application source files for the application that will be imported into the deployment share. This parameter is only valid for use in the first syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -DestinationFolder <String\>

This parameter specifies the folder in the deployment share where the application source files are to be imported. This folder is created beneath the folder specified in the *Path* parameter. This parameter is only valid for use in the first syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Move [<SwitchParameter\>]

This parameter specifies whether the application's source files should be moved (instead of copied) from the folder where the application's source files are located, which is specified in the *ApplicationSourcePath* parameter.

 If this parameter is:

- Specified, then the files are moved and the files in the folder specified in the *ApplicationSourcePath* parameter are deleted

- Not specified, then the files are copied and the files in the folder specified in the *ApplicationSourcePath* parameter are retained

  This parameter is only valid for use in the first syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -NoSource [<SwitchParameter\>]

This parameter specifies that the application being imported is an application that has no source files to be copied. When using this parameter, the application source files are:

- On a network shared folder, which is specified in the application installation command line or working directory configuration settings

- Already present in the operating system image

  This parameter is only valid for use in the second syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -Bundle [<SwitchParameter\>]

This parameter specifies that the application being imported is an application that is a bundle of two or more applications. This parameter is only valid for use in the last syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object that references the application just imported.

### Example 1

```powershell
Import-MDTApplication -Path "DS001:\Applications" -Name "Office 2010 Professional Plus 32-bit" ApplicationSourcePath "\\WDG-MDT-01\Source$\Office2010ProPlus\x86" DestinationFolder "Office2010ProPlusx86"
```

#### Description

This example imports an application with source files from the network shared folder at \\\WDG-MDT-01\Source$\Office2010ProPlus\x86 and copies the source files to DS001:\Applications\Office2010ProPlusx86 within the deployment share. The source files are retained.

### Example 2

```powershell
Import-MDTApplication -Path "DS001:\Applications" -Name "Office 2010 Professional Plus 32-bit" ApplicationSourcePath "\\WDG-MDT-01\Source$\Office2010ProPlus\x86" DestinationFolder "Office2010ProPlusx86" -Move
```

#### Description

This example imports an application with source files from the network shared folder at \\\WDG-MDT-01\Source$\Office2010ProPlus\x86 and moves the source files to DS001:\Applications\Office2010ProPlusx86 within the deployment share. The source files are removed from the network shared folder at \\\WDG-MDT-01\Source$\Office2010ProPlus\x86. The application is named *Office 2012 Professional Plus 32-bit.*

### Example 3

```powershell
Import-MDTApplication -Path "DS001:\Applications" -Name "Office 2010 Professional Plus 32-bit" NoSource
```

#### Description

This example imports an application named *Office 2012 Professional Plus 32-bit* with no source files.

### Example 4

```powershell
Import-MDTApplication -Path "DS001:\Applications" -Name "Woodgrove Bank Core Applications" Bundle
```

#### Description

This example imports an application bundle named *Woodgrove Bank Core Applications.*

## Import-MDTDriver

This section describes the **Import-MDTDriver** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Import-MDTDriver [-Path <String>] -SourcePath <String[]> [ImportDuplicates] [<CommonParameters>]
```

### Description

This cmdlet imports one or more device drivers into a deployment share. This cmdlet searches for device drivers starting at the folder specified in the *SourcePath* parameter. This cmdlet will locate multiple device drivers found in that folder structure.

### Parameters

This subsection provides information about the various parameters that can be used with the **Import-MDTDriver** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to an existing folder where the device driver being imported will be placed within the deployment share.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share. This parameter must be provided if the *SourcePath* parameter is not provided.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -SourcePath <String[ ]>

This parameter specifies one or more fully qualified paths in a string array for the source folders where the device driver files are located. Each folder structure, starting with the folder specified in this parameter, is searched for device drivers, including all subfolders and the contents of .cab files in the folder structure.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the folder where the device driver files are located. This parameter must be provided if the *Path* parameter is not provided.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**1** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ImportDuplicates [<SwitchParameter\>]

This parameter specifies whether this cmdlet should import duplicate device drivers. By default, duplicate device drivers are not imported. Duplicate device drivers are detected by calculating a hash values for all the files in a device driver folder. If the calculated hash value matches another device driver, the device driver to be imported is considered a duplicate.

 If a duplicate driver is detected and this parameter is not provided, the device driver will be added and linked to the original, existing device driver.

 If this parameter is:

- Specified, then the duplicate device drivers are imported

- Not specified, then the device drivers will be added and linked to the original, existing device drivers

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs one or more **PSObject** type objects (one for each device driver imported).

### Example 1

```powershell
Import-MDTDriver -Path "DS001:\Out-of-Box Drivers" SourcePath "\\WDG-MDT-01\Source$\Drivers"
```

#### Description

This example imports all device drivers in the folders structure with the root of the folder structure at \\\WDG-MDT-01\Source$\Drivers. The device drivers are stored in the Out-of-Box Drivers folder in the deployment share that is mapped to the DS001: MDTProvder Windows PowerShell drive. If any duplicate device drivers are detected, the device drivers will be added and linked to the original, existing device drivers in the deployment share.

### Example 2

```powershell
$DriverSourcePath="\\WDG-MDT-01\Source$\VendorADrivers", "\\WDG-MDT-01\Source$\VendorBDrivers"
Import-MDTDriver -Path "DS001:\Out-of-Box Drivers" SourcePath $DriverSourcePath ImportDuplicates
```

#### Description

This example imports all device drivers in the folders structure specified in the string array $DriverSourcePath. The device drivers are stored in the Out-of-Box Drivers folder in the deployment share that is mapped to the DS001: MDTProvder Windows PowerShell drive. If any duplicate device drivers are detected, the duplicate device drivers are imported.

## Import-MDTOperatingSystem

This section describes the **Import-MDTOperatingSystem** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Import-MDTOperatingSystem [-Path <String>] -SourcePath <String> [-DestinationFolder <String>] [-Move] [<CommonParameters>]
```

 -or-

```powershell
Import-MDTOperatingSystem [-Path <String>] [DestinationFolder <String>] -SourceFile <String> [SetupPath <String>] [-Move] [<CommonParameters>]
```

 -or-

```powershell
Import-MDTOperatingSystem [-Path <String>] -WDSServer <String> [<CommonParameters>]
```

### Description

This cmdlet imports an operating system into a deployment share. The following operating system types can be imported using this cmdlet:

- Operating systems from the original source files, using the *SourcePath* parameters. The first syntax example illustrates the use of this cmdlet for this type of operating system import.

- Custom operating systems image files, such as capture images from reference computers, using the *SourceFile* parameter. The second syntax example illustrates the use of this cmdlet for this type of operating system import.

- Operating system images that are present in Windows Deployment Services using the *WDSServer* parameter. The last syntax example illustrates the use of this cmdlet for this type of operating system import.

### Parameters

This subsection provides information about the various parameters that can be used with the **Import-MDTOperatingSystem** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to an existing folder within the deployment share where the operating system being imported will be placed. If the *DestinationFolder* parameter is used, then the folder specified in the *DestinationFolder* parameter is created beneath the folder specified in this parameter. This parameter is used in all syntax usages for this cmdlet.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -SourcePath <String\>

This parameter specifies the fully qualified path to the operating system source files for the operating system that will be imported into the deployment share. This parameter is only valid for use in the first syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -DestinationFolder <String\>

This parameter specifies the folder in the deployment share where the operating system source files are to be imported. This folder is created beneath the folder specified in the *Path* parameter. This parameter is only valid for use in the first and second syntax examples.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Move [<SwitchParameter\>]

This parameter specifies if the operating system source files should be moved (instead of copied) from the folder where the operating system source files are located, which is specified in the *DestinationFolder* parameter.

 If this parameter is:

- Specified, then the files are moved and the files in the folder specified in the *DestinationFolder* parameter are deleted

- Not specified, then the files are copied and the files in the folder specified in the *DestinationFolder* parameter are retained

  This parameter is only valid for use in the first and second syntax examples.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -SourceFile <String\>

This parameter specifies the fully qualified path to the operating system source .wim file for the operating system that will be imported into the deployment share. This parameter is only valid for use in the second syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -SetupPath <String\>

This parameter specifies the fully qualified path to the operating system setup files that need to be imported along with the .wim file specified in the *SourceFile* parameter. This parameter is only valid for use in the second syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -WDSServer <String\>

This parameter specifies the name of the Windows Deployment Services server on which the operating system image files to be imported are located. All operating image files on the Windows Deployment Services server will be imported into the deployment share. The actual operating system image files are not copied to the deployment share. Instead, the deployment share contains a link to each operating system file on the Windows Deployment Services server.

 This parameter is only valid for use in the last syntax example.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs one or more **PSObject** type objects (one for each operating system that was imported).

### Example 1

```powershell
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" SourcePath "\\WDGMDT01\Source$\Windows8" DestinationFolder "Windows8x64"
```

#### Description

This example imports an operating system from the network shared folder at \\\WDG-MDT-01\Source$\Windows8 and copies the source files to DS001:\Operating Systems\Windows8x64 within the deployment share. The source files are retained.

### Example 2

```powershell
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" SourcePath "\\WDGMDT01\Source$\Windows8" DestinationFolder "Windows8x64" -Move
```

#### Description

This example imports an operating system from the network shared folder at \\\WDG-MDT-01\Source$\Windows8 and copies the source files to DS001:\Operating Systems\Windows8x64 within the deployment share. The source files are removed from the network shared folder at \\\WDG-MDT-01\Source$\Windows8.

### Example 3

```powershell
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" DestinationFolder "Windows8x64-Reference" -SourceFile "\\WDGMDT01\Capture$\WDG-REF-01_Capture.wim"
```

#### Description

This example imports an operating system captured, custom image file (.wim file) from \\\WDG-MDT-01\ Capture$\WDG-REF-01_Capture.wim and copies the image file to DS001:\Operating Systems\Windows8x64-Reference within the deployment share. The source .wim file is retained on the network shared folder.

### Example 4

```powershell
Import-MDTOperatingSystem -Path "DS001:\Operating Systems" WDSServer "WDG-WDS-01"
```

#### Description

This example imports all the operating system images from the Windows Deployment Services server named WDG-WDS-01 and creates a link to each operating system image in DS001:\Operating Systems within the deployment share. The source operating system image files on the Windows Deployment Services server are retained on the Windows Deployment Services server.

## Import-MDTPackage

This section describes the **Import-MDTPackage** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Import-MDTPackage [-Path <String>] [[-SourcePath] <String[]>] [<CommonParameters>]
```

### Description

This cmdlet imports one or more operating system packages into a deployment share. The types of operating system packages that can be imported include security updates, language packs, or new components. Service packs should not be imported as operating system packages as they cannot be installed offline.

### Parameters

This subsection provides information about the various parameters that can be used with the **Import-MDTPackage** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to an existing folder within the deployment share where the operating system packages being imported will be placed.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -SourcePath <String\>

This parameter specifies the fully qualified path to a folder structure to be scanned for operating system packages to import. The specified folder structure will be scanned for .cab and .msu files. For .msu files, the .cab files inside the .msu files are automatically extracted.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**1** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object that references the package just imported.

### Example 1

```powershell
Import-MDTOperatingSystem -Path "DS001:\Packages" SourcePath "\\WDGMDT01\Source$\OSPackages"
```

#### Description

This example scans network shared folder at \\\WDG-MDT-01\Source$\OSPackages for operating system packages and copies the source files to DS001:\Packages folder within the deployment share. The source files are removed from the network shared folder at \\\WDG-MDT-01\Source$\OSPackages.

## Import-MDTTaskSequence

This section describes the **Import-MDTTaskSequence** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Import-MDTTaskSequence [-Path <String>] -Template <String> -Name <String> -ID <String> [[-Comments] <String>] [[-Version] <String>] [-OperatingSystemPath <String>] [-OperatingSystem <PSObject>] [-FullName <String>] [-OrgName <String>] [-HomePage <String>] [-ProductKey <String>] [-OverrideProductKey <String>] [-AdminPassword <String>] [<CommonParameters>]
```

### Description

This cmdlet imports a task sequence into a deployment share. The newly imported task sequence will be based on an existing task sequence template specified in the *Template* property.

### Parameters

This subsection provides information about the various parameters that can be used with the **Import-MDTPackage** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to an existing folder within the deployment share where the task sequence being imported will be placed. By default, the path should point to the Control folder and or a subfolder of the Control folder in the deployment share. The value of the *ID* parameter will be used to create a subfolder within the path specified in this parameter.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Template <String\>

This parameter specifies the task sequence template to be used for importing the new task sequence. Task sequence templates are .xml files that contain the task sequence steps for a particular type of task sequence. If the task sequence template is located in:

- The *installation_folder*\Templates folder (where *installation_folder* is the folder in which MDT is installed), then only the .xml file name is required.

- Another folder, then the fully qualified path, including the name of the task sequence template .xml, is required.

  For more information on the task sequence templates that are included with MDT for LTI deployments, see the section "Create a New Task Sequence in the Deployment Workbench" in the MDT document, *Using the Microsoft Deployment Toolkit*.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**1** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Name <String\>

This parameter specifies the name of the task sequence to be imported. The value of this parameter must be unique within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**2** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ID <String\>

This parameter specifies the identifier of the task sequence to be imported. The value of this parameter must be unique within the deployment share. The value assigned to this parameter should be in uppercase and not have any spaces or special characters. This value is used to create a subfolder in the folder specified in the *Path* parameter, which should be under the Control folder in the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**3** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Comments <String\>

This parameter specifies the text that provides additional, descriptive information about the task sequence to be imported. This descriptive information is visible in the Deployment Workbench.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**4** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Version <String\>

This parameter specifies the version number of the task sequence to be imported. The value of this parameter is informational only and is not used by MDT for version-related processing.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**4** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -OperatingSystemPath <String\>

This parameter specifies the fully qualified Windows PowerShell path to the folder in the deployment share that contains the operating system to be used with this task sequence, such as DS001:\Operating Systems\Windows 8. The operating system must already exist in the deployment share where the task sequence is being imported.

> [!NOTE]
>
> If you do not provide this parameter and the task sequence needs to reference an operating system, then you must provide the *OperatingSystem* parameter.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -OperatingSystem <PSObject\>

This parameter specifies the operating system object to be used with this task sequence. The operating system must already exist in the deployment share where the task sequence is being imported.

 You can retrieve the Windows PowerShell object for an operating system using the **Get-Item** cmdlet, such as the following example:

```powershell
$OS=Get-Item "DS001:\Operating Systems\Windows 8"
```

 For more information on the **Get-Item** cmdlet, see [Using the Get-Item Cmdlet](/previous-versions/windows/it-pro/windows-powershell-1.0/ee176851(v=technet.10)).

> [!NOTE]
>
> If you do not provide this parameter and the task sequence needs to reference an operating system, then you must provide the *OperatingSystemPath* parameter.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -FullName <String\>

This parameter specifies the name of the registered owner of the operating system to be used with this task sequence. This name is saved in the **RegisteredOwner** registry key at **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion**. The value of this parameter is injected into the Unattend.xml file to be associated with this task sequences.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -OrgName <String\>

This parameter specifies the name of the organization for the registered owner of the operating system to be used with this task sequence. This name is saved in the **RegisteredOrganization** registry key at **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion**. The value of this parameter is injected into the Unattend.xml file to be associated with this task sequences.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -HomePage <String\>

This parameter specifies the URL to be used as the home page in Internet Explorer. The value of this parameter is injected into the Unattend.xml file to be associated with this task sequences.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ProductKey <String\>

This parameter specifies the product key to be used for the operating system to be used with this task sequence. This product key is valid only for retail versions of Windows operating systems. The value of this parameter is injected into the Unattend.xml file to be associated with this task sequences.

> [!NOTE]
>
> If this parameter is not provided, then the product key must be provided when deploying this task sequence in the Deployment Wizard, in the CustomSettings.ini file, or in the MDT DB.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -OverrideProductKey <String\>

This parameter specifies the MAK key to be used for the operating system to be used with this task sequence. This product key is valid only for volume license versions of Windows. The value of this parameter is injected into the Unattend.xml file to be associated with this task sequences.

> [!NOTE]
>
> If this parameter is not provided, then the MAK key must be provided when deploying this task sequence in the Deployment Wizard, in the CustomSettings.ini file, or in the MDT DB.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -AdminPassword <String\>

This parameter specifies the password to be assigned to the built-in, local Administrator account on the target computer. The value of this parameter is injected into the Unattend.xml file to be associated with this task sequences.

> [!NOTE]
>
> If this parameter is not provided, then the password to be assigned to the built-in, local Administrator account on the target computer must be provided when deploying this task sequence in the Deployment Wizard, in the CustomSettings.ini file, or in the MDT DB.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object that references the task sequence just imported.

### Example 1

```powershell
Import-MDTTaskSequence -Path "DS001:\Control" -Template "Client.xml" -Name "Deploy Windows 8 to Reference Computer" -ID "WIN8REFERENCE" -Comments "Task sequence for deploying Windows 8 to the reference computer (WDG-REF-01)" -Version "1.00" -OperatingSystemPath "DS001:\Operating Systems\Windows 8_x64" -FullName "Woodgrove Bank Employee" -OrgName "Woodgrove Bank" HomePage "https://www.woodgrovebank.com"  OverrideProductKey "1234512345123451234512345" AdministratorPassword "P@ssw0rd"
```

#### Description

This example imports a task sequence named *Deploy Windows 8 to Reference Computer* and creates the task sequence in the DS001:\Control\WIN8REFERENCE folder in the deployment share. The comment, "Task sequence for deploying Windows 8 to the reference computer (WDG-REF-01)," is assigned to the task sequence. The version number of the task sequence is set to **1.00**.

 The operating system associated with the task sequence is located at DS001:\Operating Systems\Windows 8_x64 in the deployment share. The registered owner of the operating system will be set to **Woodgrove Bank Employee**. The registered organization of the operating system will be set to **Woodgrove Bank**. The Internet Explorer home page will default to `https://www.woodgrovebank.com`. The password for the local, built-in Administrator account will be set to a value of `P@ssw0rd`. The product key for the operating system will be set to **1234512345123451234512345**.

### Example 2

```powershell
$OSObject=Get-Item "DS001:\Operating Systems\Windows 8_x64"
Import-MDTTaskSequence -Path "DS001:\Control" -Template "Client.xml" -Name "Deploy Windows 8 to Reference Computer" -ID "WIN8REFERENCE" -Comments "Task sequence for deploying Windows 8 to the reference computer (WDG-REF-01)" -Version "1.00"-OperatingSystem $OSObject -FullName "Woodgrove Bank Employee" -OrgName "Woodgrove Bank" HomePage "https://www.woodgrovebank.com"  AdministratorPassword "P@ssw0rd"
```

#### Description

This example imports a task sequence named *Deploy Windows 8 to Reference Computer* and creates the task sequence in the DS001:\Control\WIN8REFERENCE folder in the deployment share. The comment, "Task sequence for deploying Windows 8 to the reference computer (WDG-REF-01)," is assigned to the task sequence. The version number of the task sequence is set to **1.00**.

 The operating system associated with the task sequence is located at DS001:\Operating Systems\Windows 8_x64 in the deployment share, which is passed to the cmdlet using the *$OSObject* variable. The *$OSObject* variable is set to an existing operating system object using the **Get-Item** cmdlet.

 The registered owner of the operating system will be set to **Woodgrove Bank Employee**. The registered organization of the operating system will be set to **Woodgrove Bank**. The Internet Explorer home page will default to `https://www.woodgrovebank.com`. The password for the local, built-in Administrator account will be set to a value of `P@ssw0rd`. The product key for the operating system will need to be provided when deploying this task sequence in the Deployment Wizard, in the CustomSettings.ini file, or in the MDT DB.

## New-MDTDatabase

This section describes the **New-MDTDatabase** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
New-MDTDatabase [-Path <String>] [-Force] -SQLServer <String> [-Instance <String>] [-Port <String>] [-Netlib <String>] -Database <String> [-SQLShare <String>] [<CommonParameters>]
```

### Description

This cmdlet creates a new MDT DB database that is associated with a deployment share. Each deployment share can be associated with only one MDT DB database.

### Parameters

This subsection provides information about the various parameters that can be used with the **New-MDTDatabase** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified Windows PowerShell path to the deployment share to which the new MDT DB database will be associated placed.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Force [<SwitchParameter\>]

This parameter specifies that tables within the MDT DB should be recreated if the database specified in the *Database* parameter already exist. If this parameter is:

- Provided, then the tables within an existing MDT DB will be re-created

- Omitted, then the tables within an existing MDT DB will not be re-created

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -SQLServer <String\>

This parameter specifies the name of the computer running SQL Server where the new MDT DB database will be created.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Instance <String\>

This parameter specifies the SQL Server instance in which the new MDT DB database will be created. If this parameter is omitted, the MDT DB database is created in the default SQL Server instance.

> [!NOTE]
>
> The SQL Server Browser service must be running on the computer running SQL Server for the cmdlet to locate the instance specified in this parameter.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Port <String\>

This parameter specifies the TCP port to be used in communication with the SQL Server instance specified in the *SQLServer* parameter. The default port that SQL Server uses is 1433. Specify this parameter when SQL Server is configured to use a port other than the default value. The value of this parameter must match the port configured for SQL Server.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Netlib <String\>

This parameter specifies the SQL Server network library used in communication with the SQL Server instance specified in the *SQLServer* parameter. The parameter can be set to one of the following values:

- **DBNMPNTW**, which is used to specify named pipes communication

- **DBSMSOCN**, which is used to specify TCP/IP sockets communication

  If this parameter is not provided, the named pipes SQL Server network library (DBNMPNTW) is used.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Database <String\>

This parameter specifies the name of the database to be created in the SQL Server instance specified in the *Instance* parameter on the SQL Server specified in the *SQLServer* parameter. The default location and naming convention will be used for the database and log files when creating the database.

 If the database specified in this parameter already exists, the database will not be recreated. The tables within the database can be recreated based on the *Force* parameter.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -SQLShare <String\>

This parameter specifies the name of a network shared folder on the computer where SQL Server is running. This connection is used to establish Windows Integrated Security connections using the Named Pipes protocol.

> [!NOTE]
>
> If this parameter is not included, then a secured IPC$ connection is not established. As a result, named pipes communication with SQL Server may fail.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object for the new MDT DB that was created.

### Example 1

```powershell
New-MDTDatabase -Path "DS001:" -SQLServer "WDGSQL01" Database "MDTDB" -SQLShare "\\WDGSQL01\MDTShare$"
```

#### Description

This example creates an MDT DB named *MDTDB* in the default SQL Server instance on a computer named *WDG-SQL-01.* If the database already exists, the tables in the existing database will not be recreated. The connection will be made using the default SQL Server TCP port and the Named Pipes protocol.

### Example 2

```powershell
New-MDTDatabase -Path "DS001:" -Force -SQLServer "WDGSQL01" -Instance "MDTInstance" Database "MDTDB" -SQLShare "\\WDGSQL01\MDTShare$"
```

#### Description

This example creates an MDT DB named *MDTDB* in the SQL Server instance named *MDTInstance* on a computer named *WDG-SQL-01.* If the database already exists, the tables in the existing database will be recreated. The connection will be made using the default SQL Server TCP port and the Named Pipes protocol.

## Remove-MDTMonitorData

This section describes the **Get-MDTPersistentDrive** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Remove-MDTMonitorData [-Path <String>] [-ID <Int32>] [<CommonParameters>]
```

 -or-

```powershell
Remove-MDTMonitorData [-Path <String>] [-ComputerObject <PSObject>] [<CommonParameters>]
```

### Description

This cmdlet removes collected monitoring data from the existing collected monitoring data in a deployment share. You can identify the monitoring data to remove by specifying the:

- Identifier (ID) of the monitoring item for a specific deployment share. The monitoring item IDs are automatically generated and assigned to the item when the item is created for the deployment share. The first syntax example illustrates this usage.

- Computer object for the monitoring item in the deployment share. The computer object can be obtained using the **Get-MDTMonitorData** cmdlet. The last syntax example illustrates this usage.

> [!NOTE]
>
> Once the monitoring data has been removed, there is no method for recovering the information.

### Parameters

This subsection provides information about the various parameters that can be used with the **Get- MDTMonitorData** cmdlet.

#### -Path <String\>

This parameter specifies the **MDTProvider** Windows PowerShell drive for the desired deployment share.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to a location within the desired MDTProvider Windows PowerShell drive.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ID <Nullable\>

This parameter specifies the monitoring data item to be removed using the identifier of the monitoring data item. If this parameter is not specified, then the *ComputerObject* parameter must be specified to identify a particular monitoring data item.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -ComputerObject <PSObject\>

This parameter specifies the monitoring data item to be removed using a computer object. If this parameter is not specified, then the *ID* parameter must be specified to identify a particular monitoring data item.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet may output a **String** type object if the *Verbose* common parameter is included; otherwise, no output is generated.

### Example 1

```powershell
Remove-MDTMonitorData -Path "DS001:" -ID 3
```

#### Description

This example removes the monitoring data item with an ID that has a value of **3** from the deployment share at the Windows PowerShell path DS001:.

### Example 2

```powershell
Remove-MDTMonitorData -ID 3
```

#### Description

This example removes the monitoring data item with an ID that has a value of **3** from the deployment share at the default Windows PowerShell path.

### Example 3

```powershell
$MonitorObject=Get-MDTMonitorData | Where-Object {$_.Name eq 'WDG-REF-01'}
Remove-MDTMonitorData -ComputerObject $MonitorObject
```

#### Description

This example removes any monitoring data item where the name of the computer is WDG-REF-01. The object is found using the **Get-MDTMonitorData** cmdlet and the **Where-Object** cmdlet. For more information on the **Where-Object** cmdlet, see [Using the Where-Object Cmdlet](/previous-versions/windows/it-pro/windows-powershell-1.0/ee177028(v=technet.10)).

## Remove-MDTPersistentDrive

This section describes the **Remove-MDTPersistentDriveWindows** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Remove-MDTPersistentDrive [-Name] <String> [[-InputObject] <PSObject>] [<CommonParameters>]
```

### Description

This cmdlet removes an existing Windows PowerShell drive created using the **MDTProvider** from the list of drives that are persisted in the Deployment Workbench or in a Windows PowerShell session using the [Restore-MDTPersistentDrive](#restore-mdtpersistentdrive) cmdlet. This cmdlet is called when a deployment share is closed in (removed from) the Deployment Workbench.

> [!NOTE]
>
> The list of persisted **MDTProvider** drives is maintained on a per-user based in the user profile.

 The list of persisted **MDTProvider** drives can be displayed using the **Get-MDTPersistentDrive** cmdlet. An MDTProvider drive can be added to the list of persisted drives using the **Add-MDTPersistentDrive** cmdlet.

### Parameters

This subsection provides information about the various parameters that can be used with the **Add-MDTPersistentDriveWindows** cmdlet.

#### -Name <String\>

Specifies the name of a Windows PowerShell drive created using the MDT provider and corresponds to an existing deployment share. The name was created using the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet and specifying the **MDTProvider** in the *PSProvider* parameter.

 For more information on how to create a new Windows PowerShell drive using the **MDTProvider** and how to create a deployment share using Windows PowerShell, see the section "Creating a Deployment Share Using Windows PowerShell" in the MDT document, *Microsoft Deployment Toolkit Samples Guide*.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**1** and **Named**|
|**Default value**|**None**|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -InputObject <PSObject\>

This parameter specifies a Windows PowerShell drive object that was created earlier in the process. Enter a **PSObject** object, such as one generated by the [New-PSDrive](/previous-versions//dd315340(v=technet.10)) cmdlet.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**2** and **Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet provides no outputs.

### Example 1

```powershell
Remove-MDTPersistentDrive -Name "DS001:"
```

#### Description

This example removes the deployment share with the Windows PowerShell drive name of *DS001* from the list of persisted drives.

### Example 2

```powershell
$MDTPSDrive = Get-PSDrive | Where-Object {$_.Root -eq "C:\DeploymentShare" -and $_.Provider -like "*MDTProvider"}
Remove-MDTPersistentDrive -InputObject $MDTPSDrive
```

#### Description

This example removes the deployment share at C:\DeploymentShare$ from the list of persisted drives. The **GetPSDrive** and **Where-Object** cmdlets are used to return the MDT persisted Windows PowerShell drive to the **Remove-MDTPersistentDrive** cmdlet using the *$MDTPSDrive* variable. For more information on the **Where-Object** cmdlet, see [Using the Where-Object Cmdlet](/previous-versions/windows/it-pro/windows-powershell-1.0/ee177028(v=technet.10)). For more information on the **Get-PSDrive** cmdlet, see [Using the Get-PSDrive Cmdlet](/previous-versions/windows/it-pro/windows-powershell-1.0/ee176856(v=technet.10)).

## Restore-MDTPersistentDrive

This section describes the **Restore-MDTPersistentDrive** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Restore-MDTPersistentDrive [-Force] [<CommonParameters>]
```

### Description

This cmdlet restores a persisted MDT Windows PowerShell drive to the list of active Windows PowerShell drive for each deployment share that was added to the list of persisted MDT Windows PowerShell drives. The list of persisted MDT Windows PowerShell drives is managed using the [Add-MDTPersistentDrive](#add-mdtpersistentdrive) and [Remove-MDTPersistentDrive](#remove-mdtpersistentdrive) cmdlets or the Deployment Workbench.

 This cmdlet calls the **New-PSDrive** cmdlet to create a Windows PowerShell drive for each drive in the MDT persisted list. Persisted MDT Windows PowerShell drives are similar to persisted network drive mappings.

> [!NOTE]
>
> This list of persisted MDT Windows PowerShell drives is maintained on a per-user basis and are stored in the user profile.

### Parameters

This subsection provides information about the various parameters that can be used with the **Restore-MDTPersistentDrive** cmdlet.

#### -Force [<SwitchParameter\>]

This parameter specifies that the deployment share should be upgraded when restored (if required). If this parameter is:

- Provided, then the deployment share will be upgraded when restored (if required)

- Omitted, then deployment share will not be upgraded when restored

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object for each MDT Provider Windows PowerShell drive that is restored.

### Example 1

```powershell
Get-MDTPersistentDrive
```

#### Description

This example restores the list of MDT persisted drives, by creating a Windows PowerShell drive using the **MDTProvider** type. The deployment share will not be upgraded when restored.

### Example 2

```powershell
Get-MDTPersistentDrive -Force
```

#### Description

This example restores the list of MDT persisted drives, by creating a Windows PowerShell drive using the **MDTProvider** type. The deployment share will be upgraded when restored (if required).

## Set-MDTMonitorData

This section describes the **Get-MDTPersistentDrive** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Set-MDTMonitorData [-Path <String>] [-ComputerObject <PSObject>] [-Settings <Hashtable>] [<CommonParameters>]
```

 -or-

```powershell
Set-MDTMonitorData [-Path <String>] [-MacAddress <String>] [Settings <Hashtable>] [<CommonParameters>]
```

### Description

This cmdlet creates a new monitoring data item, or updates an existing monitoring data item, in a deployment share. You can identify the monitoring data to remove by specifying the:

- Computer object for the monitoring item in the deployment share. The computer object can be obtained using the **Get-MDTMonitorData** cmdlet. The first syntax example illustrates this usage.

- MAC address of the primary network adapter of the monitoring item for a specific deployment share. The MAC address is automatically assigned to the monitoring data item when the item is created for the deployment share. The last syntax example illustrates this usage.

> [!NOTE]
>
> Once the monitoring data has been removed, there is no method for recovering the information.

### Parameters

This subsection provides information about the various parameters that can be used with the **Get- MDTMonitorData** cmdlet.

#### -Path <String\>

This parameter specifies the MDTProvider Windows PowerShell drive for the desired deployment share.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to a location within the desired MDTProvider Windows PowerShell drive.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -ComputerObject <PSObject\>

This parameter specifies the monitoring data item to be created or updated using a computer object. If this parameter is not specified, then the *MACAddress* parameter must be specified to identify a particular monitoring data item.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -MACAddress <String\>

This parameter specifies the monitoring data item to be created or updated using the MAC address of the primary network adapter of the computer being monitored. The format of the MACAddress is *xx:xx:xx:xx:xx:xx,* where *x* is a hexadecimal character specified in uppercase (as required). If this parameter is not specified, then the *ComputerObject* parameter must be specified to identify a particular monitoring data item.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -Settings <Hashtable\>

This parameter specifies the monitoring data settings for the monitoring data item to be created or updated. The format of the hashtable provided with this parameter is `@{"Setting"="Value"; "Setting1"="Value1"; "Setting2"="Value2}`. If this parameter is not specified, then the monitoring data item is created, but no monitoring information is stored.

 `"Setting"` can be any property listed in the ZTIGather.xml file. `Value` can be any valid value for the property specified in `"Setting"`.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet does not generate any output.

### Example 1

```powershell
$MonitorObject=Get-MDTMonitorData | Where-Object {$_.Name eq 'WDG-REF-01'}
Set-MDTMonitorData -ComputerObject $MonitorObject Setting @{"OSDComputerName"="WDG-MDT-01";"SkipWizard"="YES"}
```

#### Description

This example removes any monitoring data item where the name of the computer is *WDG-REF-01.* The object is found using the **Get-MDTMonitorData** cmdlet and the **Where-Object** cmdlet. For more information on the **Where-Object** cmdlet, see [Using the Where-Object Cmdlet](/previous-versions/windows/it-pro/windows-powershell-1.0/ee177028(v=technet.10)). The [OSDComputerName](properties.md#osdcomputername) property is recorded as having a value of **WDG-MDT-01**, and the [SkipWizard](properties.md#skipwizard) property is recorded as having a value of **YES**.

### Example 2

```powershell
Set-MDTMonitorData -MACAddress "00:11:22:33:44:55" MonitorObject Setting @{"OSDComputerName"="WDG-MDT-01";"SkipWizard"="YES"}
```

#### Description

This example creates or updates a monitoring data item with a **MACAddress** that has a value of **00:11:22:33:44:55**. The [OSDComputerName](properties.md#osdcomputername) property is recorded as having a value of **WDG-MDT-01**, and the [SkipWizard](properties.md#skipwizard) property is recorded as having a value of **YES**.

## Test-MDTDeploymentShare

Although this cmdlet is returned using the **Get-Command** cmdlet as being in the Microsoft.BDD.PSSnapIn snap-in, it is not implemented.

## Test-MDTMonitorData

This section describes the **Test-MDTMonitorData** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Test-MDTMonitorData -ServerName <String> -EventPort <Int32> -DataPort <Int32> [<CommonParameters>]
```

### Description

This cmdlet validates if the MDT monitoring service, which runs on the computer on which MDT is installed, is enabled and running properly. The MDT monitoring service collects monitoring information that can be displayed:

- In the Monitoring node in a deployment share in the Deployment Workbench

- Using the [Get-MDTMonitorData](#get-mdtmonitordata) cmdlet

  The MDT monitoring service can be disabled using the [Disable-MDTMonitorService](#disable-mdtmonitorservice). Monitoring information can be written to the MDT monitoring service using the [Set-MDTMonitorData](#set-mdtmonitordata) cmdlet.

> [!NOTE]
>
> For this cmdlet to function properly there must be at least one MDT monitoring data item in the deployment share. If no MDT monitoring information has been recorded, the deployment share will fail the test.

 For more information on the MDT monitoring service, see the section "Monitoring MDT Deployments" in the MDT document, *Using the Microsoft Deployment Toolkit*.

### Parameters

This subsection provides information about the various parameters that can be used with the **Test-MDTMonitorData** cmdlet.

#### -Server <String\>

Specifies the name of the computer on which MDT is installed and the MDT monitoring service is running.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|None|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -DataPort <Int32\>

This parameter specifies the TCP port used as the data port for the MDT monitoring service.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -EventPort <Int32\>

This parameter specifies the TCP port used as the event port for the MDT monitoring service.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a Boolean value that represents the success (true) or failure (false) of the text.

### Example 1

```powershell
Test-MDTMonitorData -Server "WDG-MDT-01" -DataPort "9801" EventPort "9800"
```

#### Description

This example verifies if the MDT monitoring service on WDG-MDT-01 is installed and running. The cmdlet will verify using a data port of 9801 and an event port of 9800.

## Update-MDTDatabaseSchema

This section describes the **Update-MDTDatabaseSchema** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Update-MDTDatabaseSchema -SQLServer <String> [-Instance <String>] [-Port <String>] [-Netlib <String>] -Database <String> [-SQLShare <String>] [<CommonParameters>]
```

### Description

This cmdlet updates an existing MDT DB database to the latest version of the MDT DB database schema. Each deployment share can be associated with only one MDT DB database.

 This cmdlet is automatically called when a deployment share is being upgraded, such as when running the [Restore-MDTPersistentDrive](#restore-mdtpersistentdrive) cmdlet with the *Force* parameter and the [Update-MDTDeploymentShare](#update-mdtdeploymentshare) cmdlet.

### Parameters

This subsection provides information about the various parameters that can be used with the **Upgrade-MDTDatabaseSchema** cmdlet.

#### -SQLServer <String\>

This parameter specifies the name of the computer running SQL Server where the MDT DB database will be upgraded.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Instance <String\>

This parameter specifies the SQL Server instance on which the MDT DB database to be upgraded exists. If this parameter is omitted, then the MDT DB database is assumed to be in the default SQL Server instance.

> [!NOTE]
>
> The SQL Server Browser service must be running on the computer running SQL Server for the cmdlet to locate the instance specified in this parameter.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Port <String\>

This parameter specifies the TCP port to be used in communication with the SQL Server instance specified in the *SQLServer* parameter. The default port that SQL Server uses is 1433. Specify this parameter when SQL Server is configured to use a port other than the default value. The value of this parameter must match the port configured for SQL Server.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Netlib <String\>

This parameter specifies the SQL Server network library that is used in communication with the SQL Server instance specified in the *SQLServer* parameter. The parameter can be set to one of the following values:

- **DBNMPNTW**, which is used to specify named pipes communication

- **DBSMSOCN**, which is used to specify TCP/IP sockets communication

  If this parameter is not provided, the named pipes SQL Server network library (**DBNMPNTW**) is used.

> [!NOTE]
>
> The Deployment Workbench does not provide the option for configuring the SQL Server network library. The Deployment Workbench always uses named pipes communication. However, the SQL Server network library can be configured in the CustomSettings.ini file.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Database <String\>

This parameter specifies the name of the database to be upgraded in the SQL Server instance specified in the *Instance* parameter on the SQL Server instance specified in the *SQLServer* parameter.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **PSObject** type object for the MDT database that was upgraded. This cmdlet also outputs a **String** type data if the *Verbose* common parameter is included.

### Example 1

```powershell
Update-MDTDatabaseSchema -SQLServer "WDGSQL01" Database "MDTDB"
```

#### Description

This example updates the schema for an MDT database named *MDTDB* in the default SQL Server instance on a computer named *WDG-SQL-01.* The connection will be made to the SQL Server instance using the default TCP port and the Named Pipes protocol.

### Example 2

```powershell
Update-MDTDatabaseSchema -SQLServer "WDGSQL01" -Instance "MDTInstance" -Port "6333" Database "MDTDB"
```

#### Description

This example updates the schema for an MDT database named *MDTDB* in the SQL Server instance named *MDTInstance* on a computer named *WDG-SQL-01.* The connection will be made to the SQL Server using TCP port 6333 and the Named Pipes protocol.

## Update-MDTDeploymentShare

This section describes the **Update-MDTDeploymentShare** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Update-MDTDeploymentShare [-Path <String>] [-Force] [Compress] [<CommonParameters>]
```

### Description

This cmdlet updates an existing deployment share with the latest files from the Windows ADK. This cmdlet also updates or regenerates the required Windows PE boot images in both WIM and ISO file formats.

### Parameters

This subsection provides information about the various parameters that can be used with the **Update-MDTDeploymentShare** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to an existing folder in the deployment share that is being updated.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### -Force [<SwitchParameter\>]

This parameter specifies whether Windows PE boot images (.iso and .wim files) for the deployment share should be completely regenerated. If this parameter is:

- Provided, then the cmdlet creates new versions of the Windows PE boot images. This process takes more time than optimizing the existing Windows PE boot images.

- Omitted, then the cmdlet optimizes the existing Windows PE boot images. This process takes less time than generating new versions of the Windows PE boot images. If this parameter is omitted, the *Compress* parameter can be used to reduce the size of the boot images as a part of the Windows PE boot image optimization process.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### -Compress [<SwitchParameter\>]

This parameter specifies whether Windows PE boot images (.iso and .wim files) for the deployment share should be compressed when they are optimized (without the *Force* parameter). If this parameter is:

- Provided, then the cmdlet compresses the Windows PE boot images as they are being optimized

- Omitted, then the cmdlet does not compress the Windows PE boot images as they are being optimized

> [!NOTE]
>
> This parameter should only be provided if the *Force* parameter is not provided. If the *Force* parameter is included, new Windows PE boot images are generated and are compressed to the minimal size.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**False**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**True** (**ByValue**)|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **String** type data and produces additional **String** type data if the *Verbose* common parameter is included.

### Example 1

```powershell
Update-MDTDepoymentShare
```

#### Description

This example updates the deployment share at the Windows PowerShell working directory. The Windows PE boot images will be optimized. The Windows PE boot images will not be compressed.

### Example 2

```powershell
Update-MDTDepoymentShare -Path "DS001:"
```

#### Description

This example updates the deployment share at the MDT Windows PowerShell drive named *DS001:.* The Windows PE boot images will be optimized. The Windows PE boot images will not be compressed.

### Example 3

```powershell
Update-MDTDepoymentShare -Path "DS001:" -Compress
```

#### Description

This example updates the deployment share at the MDT Windows PowerShell drive named *DS001:.* The Windows PE boot images will be optimized. The Windows PE boot images will be compressed.

### Example 4

```powershell
Update-MDTDepoymentShare -Path "DS001:" -Force
```

#### Description

This example updates the deployment share at the MDT Windows PowerShell drive named *DS001:.* New versions of the Windows PE boot images will be generated.

## Update-MDTLinkedDS

This section describes the **Update-MDTLinkedDS** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Update-MDTLinkedDS -Path <String> [<CommonParameters>]
```

### Description

This cmdlet replicates content from a deployment share to a linked deployment share using the selection profile used to define the linked deployment share. The replication behavior is determined based on the configuration settings for the linked deployment share.

### Parameters

This subsection provides information about the various parameters that can be used with the **Update-MDTLinkedDS** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to the linked deployment share that is being updated.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **String** type data and produces additional **String** type data if the *Verbose* common parameter is included.

### Example 1

```powershell
Update-MDTLinkedDS -Path "DS001:\Linked Deployment Shares\LINKED001"
```

#### Description

This example replicates content from the deployment share to the linked deployment share at the Windows PowerShell path DS001:\Linked Deployment Shares\LINKED001 folder.

## Update-MDTMedia

This section describes the **Update-MDTMedia** Windows PowerShell cmdlet. Run this cmdlet from a Windows PowerShell console that has the MDT PowerShell snap-in loaded. For more information on how to start a Windows PowerShell console that has the MDT PowerShell snap-in loaded, see "Loading the MDT Windows PowerShell Snap-In".

### Syntax

```powershell
Update-MDTMedia -Path <String> [<CommonParameters>]
```

### Description

This cmdlet replicates content from a deployment share to a folder that contains deployment media using the selection profile used to define the deployment media. The replication behavior is determined based on the configuration settings for the deployment media.

 Media in LTI allows you to perform LTI deployments solely from local media without connecting to a deployment share. You can store the media on a DVD, USB hard disk, or other portable device. After you create the media, generate bootable WIM images that allow the deployment to be performed from portable media devices locally available on the target computer.

### Parameters

This subsection provides information about the various parameters that can be used with the **Update-MDTMedia** cmdlet.

#### -Path <String\>

This parameter specifies the fully qualified path to the folder that contains the deployment media that is being updated.

> [!NOTE]
>
> If this parameter is not provided, then the Windows PowerShell working directory must default to the desired location within the deployment share.

|**Parameter**|**Value**|
|-|-|
|**Required?**|**True**|
|**Position?**|**Named**|
|**Default value**|-|
|**Accept pipeline input?**|**False**|
|**Accept wildcard characters?**|**False**|

#### <CommonParameters\>

This cmdlet supports the following common parameters: *Verbose, Debug, ErrorAction, ErrorVariable, OutBuffer, OutVariable, WarningAction,* and *WarningVariable.* For more information, see the topic, "about_CommonParameters," which you can access by typing the following command, and then pressing ENTER:

```powershell
Get-Help about_CommonParameters
```

### Outputs

This cmdlet outputs a **String** type data and produces additional **String** type data if the *Verbose* common parameter is included.

### Example 1

```powershell
Update-MDTMedia -Path "DS001:\Media\MEDIA001"
```

#### Description

This example replicates content from the deployment share to the folder containing the deployment media at the Windows PowerShell path DS001:\Media \MEDIA001 folder.

## Related articles

- [Task Sequence Steps](task-sequence-steps.md).
- [Properties](properties.md).
- [Scripts](scripts.md).
- [Support Files](support-files.md).
- [Utilities](utilities.md).
- [Tables and Views in the MDT DB](tables-views-mdt-db.md).
- [Windows 7 Feature Dependency Reference](windows-7-feature-dependency.md).
- [UDI Reference](udi-reference.md).