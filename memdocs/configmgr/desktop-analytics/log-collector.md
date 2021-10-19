---
title: Log collector
titleSuffix: Configuration Manager
description: Use the logs collector tool to help troubleshoot Desktop Analytics
ms.date: 07/21/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# Desktop Analytics log collector

Use the **DesktopAnalyticsLogsCollector.ps1** tool from the Configuration Manager install directory to help troubleshoot Desktop Analytics device enrollment issues. It runs some basic troubleshooting steps and collects the relevant logs into a single working directory. You can share this content with Microsoft support.

## Prerequisites

- A Desktop Analytics client running Windows 10, Windows 8.1, or Windows 7 with Service Pack 1.

- Run the script on the device as an administrative user, and **Run as Administrator**.

    > [!TIP]
    > You can use the Configuration Manager **Scripts** feature with this tool. For more information, see [Example 5: Deploy script via Configuration Manager **Scripts**](#bkmk_ex5).

- For Windows 7 with Service Pack 1: PowerShell version 4.0 or later

  - [.NET framework version 4.6 or later](https://dotnet.microsoft.com/download/dotnet-framework)

  - Windows Management Framework [version 4.0](https://support.microsoft.com/topic/description-of-wmf-4-0-for-windows-7-sp1-windows-embedded-standard-7-sp1-and-windows-server-2008-r2-sp1-e3c830c7-269a-8ae0-d7e9-5ab4a0c37484) (`aka.ms/wmf4download`) or [version 5.1](https://www.microsoft.com/download/details.aspx?id=54616) (`aka.ms/wmf5download`)

## Usage

Get the script from the Configuration Manager installation content: `SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## Parameters

### `-LogPath`

Specifies a local or UNC path to put the log and other output files.

**Values**:

- Local path (maximum length = 130), for example: `c:\myfolder`

- UNC path (maximum length = 130), for example: `\\myserver\myfolder`

**Type**: String

**Position**: 1

**Default value**: `$Env:SystemDrive\M365AnalyticsLogs` (When this parameter is null, empty, or white space, the script creates the M365AnalyticsLogs folder under the system drive.)

### `-LogMode`

Specifies the verbose level of the logs.

**Values**:

- `0`: Log script messages to PowerShell command window only.

- `1`: Log script messages to both log file under the output folder and PowerShell command window.

- `2`: Log script messages to log file under the output folder only.

**Type**: Int16

**Position**: 2

**Default value**: `1` (Log script messages to both log file and PowerShell command window.)

### `-CollectNetTrace`

Specifies whether the script collects the network trace.

**Values**:

- `0`: Don't enable the network trace.

- `1` (any non-zero integer value): Enable network trace and collect results.

**Type**: Int16

**Position**: 3

**Default value**: `0` (Don't enable the network trace)

### `-CollectUTCTrace`

Specifies whether the script collects the Windows UTC trace and run connectivity diagnosis.

**Values**:

- `0`: Don't enable the UTC trace or run connectivity diagnosis.

- `1` (any non-zero integer value): Enable the UTC trace, run connectivity diagnosis, and collect results.

**Type**: Int16

**Position**: 4

**Default value**: `0` (Don't enable the UTC trace or run connectivity diagnosis)

## Output

The script creates a *working folder* under the specified path. For example, `M365AnalyticsLogs_yy_MM_dd_HH_mm_ss`. It puts all its output files into this working folder.

If you enable the script to write to a *log file*, it generates one in the working folder. For example, `M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt`.

The script also generates other *diagnostic files* in the working folder. For example:

- `installedKBs.txt`: a list of Windows updates installed on the device
- `appcompat`: application compatibility data
- `Reg*.txt`: a series of files with exported data from the Windows Registry

## Examples

### <a name="bkmk_ex1"></a> Example 1: Run script via PowerShell command window with default values

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="bkmk_ex2"></a> Example 2: Run script via PowerShell command window with specified parameters

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="bkmk_ex3"></a> Example 3: Run script via PowerShell command window with specified parameters in position

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="bkmk_ex4"></a> Example 4: Run script via PowerShell command window with specified parameter and verbose messages

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="bkmk_ex5"></a> Example 5: Deploy script via Configuration Manager **Scripts**

For more information, see [Create and run PowerShell scripts from the Configuration Manager console](../apps/deploy-use/create-deploy-scripts.md).

**DesktopAnalyticsLogsCollector.ps1** is digitally signed by Microsoft. You may need to add its Microsoft code signing certificate as a Trusted Publisher on the target device.

1. Open the properties of the script in Windows Explorer. Switch to the **Digital Signatures** tab and select **Details**.

2. On the **General** tab, select **View Certificate**.

    > [!NOTE]
    > To distribute the certificate via other mechanisms, first export the certificate to a file. Go to the **Details** tab, and select **Copy to File**.

3. Select **Install Certificate**. Import the certificate, placing it in the **Trusted Publishers** store.

## Next steps

- [Troubleshoot Desktop Analytics](troubleshooting.md)

- [Create and run PowerShell scripts from the Configuration Manager console](../apps/deploy-use/create-deploy-scripts.md)
