---
title: BitLocker event logs
titleSuffix: Configuration Manager
description: Learn about how to work with BitLocker information in the Windows Event Log to troubleshoot problems
ms.date: 11/29/2019
ms.service: configuration-manager
ms.subservice: protect
ms.topic: troubleshooting
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# BitLocker event logs

*Applies to: Configuration Manager (current branch)*

The BitLocker management agent and web services use Windows event logs to record messages. In the Event Viewer, go to **Applications and Services Logs**, **Microsoft**, **Windows**. The log channel (node) varies depending upon the computer and the component:

- **MBAM**: BitLocker management agent on a client computer
- **MBAM-Web**:
  - Recovery service on the management point
  - Self-service portal
  - Administration and monitoring website

For more information about specific messages in these logs, see the following articles:

- [Client event logs](client-event-logs.md)
- [Server event logs](server-event-logs.md)

In each node, by default you'll see two log channels: **Admin** and **Operational**. For more detailed troubleshooting information, you can also show [analytics and debug logs](#bkmk_debug).

## Log properties

In Windows Event Viewer, select a specific log. For example, **Admin**. Go to the **Action** menu, and select **Properties**. Configure the following settings:

- **Maximum log size (KB)**: by default, this setting is `1028` (1 MB) for all logs.
- **When maximum event log size is reached**: by default, the **Admin** and **Operational** logs are set to **Overwrite events as needed (oldest events first)**.

## <a name="bkmk_debug"></a> Analytic and debug logs

You can enable more detailed logs for troubleshooting purposes. In Event Viewer, go to the **View** menu, and select **Show Analytic and Debug Logs**. Now when you browse to the log channel, you'll see two additional logs: **Analytic** and **Debug**.

> [!TIP]
> By default, these logs have the following properties:
>
> - **Maximum log size (KB)**: `1028` (1 MB)
> - **Do not overwrite events (Clear logs manually)**

## Export logs to text

Especially with the [analytic and debug logs](#bkmk_debug), you may find it easier to review the logs entries in a single text file. Use the following PowerShell commands to export the event log entries to text files:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
