---
title: Support Center
titleSuffix: Configuration Manager
description: Troubleshoot Configuration Manager clients with the Support Center.
ms.date: 11/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Support Center for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1357489-->
Starting in version 1810, use Support Center for client troubleshooting, real-time log viewing, or capturing the state of a Configuration Manager client computer for later analysis. Support Center is a single tool to consolidate many administrator troubleshooting tools. 



## About 

Support Center aims to reduce the challenges and frustration when troubleshooting Configuration Manager client computers. Previously, when working with support to address an issue with Configuration Manager clients, you would need to manually collect log files and other information to help troubleshoot the issue. It was easy to accidentally forget a crucial log file, causing additional headaches for you and the support personnel who you're working with.

Use Support Center to streamline the support experience. It lets you:

 - Create a troubleshooting bundle (.zip file) that contains the Configuration Manager client log files. You then have a single file to send to support personnel.  

 - View Configuration Manager client log files, certificates, registry settings, debug dumps, client policies.  

 - Real-time diagnostic of inventory (replaces ContentSpy), policy (replaces PolicySpy), and client cache.  


### Support Center viewer

Support Center includes Support Center Viewer, a tool that support personnel use to open the bundle of files that you create using Support Center. Support Center's data collector collects and packages diagnostic logs from a local or remote Configuration Manager client. To view data collector bundles, use the viewer application.


### Support Center log file viewer

Support Center includes a modern log viewer. This tool replaces CMTrace. OneTrace provides a customizable interface with support for tabs and dockable windows. It has a fast presentation layer, and can load large log files in seconds.


### PowerShell cmdlets

Support Center also includes [Windows PowerShell cmdlets](https://go.microsoft.com/fwlink/?linkid=397830). Use these cmdlets to create a remote connection to another Configuration Manager client, to configure the data collection options, and to start data collection.



## Prerequisites

Install the following components on the server or client computer on which you install Support Center:

- An OS version supported by Configuration Manager. For more information, see [Supported OS versions for clients](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Support Center doesn't support mobile devices.  

- .NET Framework 4.5.2 is required on the computer where you run Support Center and its components.  



## Install

Find the Support Center installer on the site server at the following path: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

After you install it, find the following items on the Start menu in the **Microsoft System Center** group:  
- Support Center (ConfigMgrSupportCenter.exe)  
- Support Center Log File Viewer (CMLogViewer.exe)  
- Support Center Viewer (ConfigMgrSupportCenterViewer.exe)  



## Known issues 

#### Remote connections must include computer name or domain as part of the user name
If you connect to a remote client from Support Center, you must provide the machine name or domain name for the user account when establishing the connection. If you use a shorthand computer name or domain name (such as `.\administrator`), the connection succeeds, but Support Center doesn't collect data from the client. 

To avoid this issue, use the following user name formats to connect to a remote client: 
- `ComputerName\UserName`  
- `DomainName\UserName`  

#### Scripted server message block connections to remote clients might require removal
When connecting to remote clients using the [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) PowerShell cmdlet, Support Center creates a server message block (SMB) connection to each remote client. It retains those connections after you complete data collection. To avoid exceeding the maximum number of remote connections for Windows, use the `net use` command to see the currently active set of remote connections. Then disable any unneeded connections by using the following command: 
`net use <connection_name> /d` 
where `<connection_name>` is the name of the remote connection.



## Next steps

[Support Center quickstart](/sccm/core/support/support-center-quickstart)
