---
title: Run Meter Summarization Tool
titleSuffix: Configuration Manager
description: Use the Run Meter Summarization Tool to trigger the software metering summarization tasks in Configuration Manager.
ms.date: 07/30/2018
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Run Meter Summarization Tool

*Applies to: Configuration Manager (current branch)*

The Run Meter Summarization Tool is one of the [Configuration Manager tools](tools.md). Use it to immediately trigger the maintenance tasks for software metering summarization on primary sites. By default, these tasks run as scheduled in **Site Maintenance** tasks, which start after 12:00 AM every day. 

These tasks summarize the data in the **MeterData** SQL Server table, and write the summary results into the **FileUsageSummary** and **MonthlyUsageSummary** tables. Then you see the summarized result in software metering reports. Any Configuration Manager administrative user who can connect to the primary site database can use this tool to run summarization. 

This tool runs the **File Usage Summary** and **Monthly Usage Summary** software metering data summarization tasks. It summarizes all existing meter data without the usual 12-hour waiting period. Run it on the SQL Server that hosts the site database. If summarization is successful, the exit code is set to `0`. If there was an error, the exit code is `1`.



## Usage

### Command Line

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### Options

#### Database name
The name of the site database on the SQL Server.

#### Delay in hours for summarization
The tool summarizes the software metering usage generated before the delay. By default, this delay is zero.


### Example

#### Summarize the software metering usage generated 12 hours ago

`runmetersumm CCM_ABC <12>`



## See also

- [Maintenance tasks](../servers/manage/maintenance-tasks.md)
- [Monitor app usage with software metering](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
