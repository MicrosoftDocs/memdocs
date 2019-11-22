---
title: BitLocker event logs
titleSuffix: Configuration Manager
description: Learn about how to work with BitLocker information in the Windows Event Log to troubleshoot problems
ms.date: 11/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# BitLocker event logs

*Applies to: Configuration Manager (current branch)*

The BitLocker management agent and web services use Windows event logs to record messages. In the Event Viewer, go to **Applications and Services Logs**, **Microsoft**, **Windows**. The log channel (node) varies depending upon the computer and the component:

- **MBAM**: BitLocker management agent on a client computer
- **MBAM-Server**: BitLocker administration and monitoring website
- **MBAM-Web**: BitLocker self-service portal

For more information about specific messages in these logs, see the following articles:

- [Client event logs](/configmgr/protect/tech-ref/bitlocker/client-event-logs)
- [Server event logs](/configmgr/protect/tech-ref/bitlocker/server-event-logs)

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

Especially with the analytic and debug logs, you may find it easier to review the logs entries in a single text file. Use the following PowerShell commands to export the event log entries to text files:

``` PowerShell
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Out-File -Width 300 C:\Temp\MBAM_Analytic.txt
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Out-File -Width 300 C:\Temp\MBAM_Debug.txt
```
