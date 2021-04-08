---
title: Support Center
titleSuffix: Configuration Manager
description: Troubleshoot Configuration Manager clients with the Support Center.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
---

# Support Center for Configuration Manager

*Applies to: Configuration Manager (current branch)*

<!--1357489-->
Use Support Center for client troubleshooting, real-time log viewing, or capturing the state of a Configuration Manager client computer for later analysis. Support Center is a single tool to combine many administrator troubleshooting tools.

## About

Support Center aims to reduce the challenges and frustration when troubleshooting Configuration Manager client computers. Previously, when working with support to address an issue with Configuration Manager clients, you would need to manually collect log files and other information to help troubleshoot the issue. It was easy to accidentally forget a crucial log file, causing headaches for you and the support personnel who you're working with.

Use Support Center to streamline the support experience. It lets you:

- Create a troubleshooting bundle (.zip file) that contains the Configuration Manager client log files. You then have a single file to send to support personnel.  

- View Configuration Manager client log files, certificates, registry settings, debug dumps, client policies.  

- Real-time diagnostic of inventory (replaces ContentSpy), policy (replaces PolicySpy), and client cache.  

Starting in version 2103, Support Center is split into the following tools:<!--8693068-->

- **Support Center Client Data Collector**: Collects data from a device to view in the Support Center Viewer. This separate tool encompasses the existing Support Center action to [Collect selected data](support-center-ui-reference.md#collect-selected-data).

- **Support Center Client Tools**: The other Support Center troubleshooting functionality, except for **Collect selected data**.

The following tools are still a part of Support Center:

- **Support Center Viewer**
- **Support Center OneTrace**
- **Support Center Log File Viewer**

### Support Center viewer

Support Center includes Support Center Viewer, a tool that support personnel use to open the bundle of files that you create using Support Center. Support Center's data collector collects and packages diagnostic logs from a local or remote Configuration Manager client. To view data collector bundles, use the viewer application.

### Support Center log file viewer

Support Center includes a modern log viewer. This tool replaces CMTrace and provides a customizable interface with support for tabs and dockable windows. It has a fast presentation layer, and can load large log files in seconds.

### Support Center OneTrace (Preview)

<!--3555962-->
**OneTrace** is a new log viewer with Support Center. It works similarly to CMTrace, with improvements. For more information, see [Support Center OneTrace](support-center-onetrace.md).

### PowerShell cmdlets

Support Center also includes PowerShell cmdlets. Use these cmdlets to create a remote connection to another Configuration Manager client, to configure the data collection options, and to start data collection. These cmdlets are in separate PowerShell module named **ConfigMgrSupportCenter.PS**. After you install Support Center, use the following command to import this module:

```powershell
Import-Module "C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.PS.psd1"
```

## Prerequisites

Install the following components on the server or client computer on which you install Support Center:

- Any Windows OS version supported by Configuration Manager. For more information, see [Supported OS versions for clients](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). Support Center doesn't support mobile devices or macOS.

- .NET Framework 4.5.2 is required on the computer where you run Support Center and its components.  

## Install

Find the Support Center installer on the site server at the following path: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

After you install it, find the following items on the Start menu in the **Microsoft Endpoint Manager** group:  

- Support Center Client Data Collector (starting in version 2103)
- Support Center Client Tools (starting in version 2103)
- Support Center (version 2010 and earlier)
- Support Center Log File Viewer
- Support Center OneTrace
- Support Center Viewer

Starting in version 2103, the Start menu group for Support Center includes these five tools:

:::image type="content" source="media/8693068-support-center-start-menu.png" alt-text="Start menu showing five Support Center tools in version 2103 and later":::

## Known issues

### Remote connections must include computer name or domain as part of the user name

If you connect to a remote client from Support Center, you must provide the machine name or domain name for the user account when establishing the connection. If you use a shorthand computer name or domain name (such as `.\administrator`), the connection succeeds, but Support Center doesn't collect data from the client.

To avoid this issue, use the following user name formats to connect to a remote client:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### Scripted server message block connections to remote clients might require removal

When connecting to remote clients using the [New-CMMachineConnection](/previous-versions/system-center/powershell/system-center-2012-r2/dn688183(v=sc.20)) PowerShell cmdlet, Support Center creates a server message block (SMB) connection to each remote client. It keeps those connections after you complete data collection. To avoid exceeding the maximum number of remote connections for Windows, use the `net use` command to see the currently active set of remote connections. Then disable any unneeded connections by using the following command:
`net use <connection_name> /d`
where `<connection_name>` is the name of the remote connection.

## Next steps

[Support Center quickstart](support-center-quickstart.md)
