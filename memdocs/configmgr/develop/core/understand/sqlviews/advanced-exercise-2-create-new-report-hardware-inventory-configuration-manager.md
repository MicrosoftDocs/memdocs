---
title: "'Advanced exercise 2: Create a new report for hardware inventory'"
titleSuffix: Configuration Manager
description: Create a Configuration Manager report that displays hardware inventory information.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: d7e964d3-5c1a-42c5-81fd-57fc833cb55a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Advanced exercise 2: Create a new report for hardware inventory in Configuration Manager

In this exercise, you will create a Configuration Manager report that displays the computer name, site code, the date of the last scan for hardware inventory, and the number of days since the last scan for a specified computer.

> [!IMPORTANT]
> Before you begin this exercise, you should review the basic exercises to learn about the report elements, the properties for a report, and the different ways to create the report SQL statement.

## Report requirements

Use the following report requirements to create the new report.

## SQL Server views in the SQL statement

Use the following Configuration Manager SQL Server views when creating the report SQL statement:

- **v_GS_WORKSTATION_STATUS**: This SQL Server view contains the date and time of the last scan for hardware inventory reported by client computers. For more information about this SQL Server view, see [Hardware Inventory Views in Configuration Manager](hardware-inventory-views-configuration-manager.md).
- **v_R_System**: This SQL Server view contains all of the discovered system resources. For more information about this SQL Server view, see [Discovery Views in Configuration Manager](discovery-views-configuration-manager.md).
- **v_RA_System_SMSInstalledSites**: This SQL Server view contains the installed site for all client computers. For more information about this SQL Server view, see [Discovery Views in Configuration Manager](discovery-views-configuration-manager.md).

## JOINS in the SQL statement

Create the following JOINS in the SQL statement:

- **v_GS_WORKSTATION_STATUS** is joined to **v_R_System** by using the **ResourceID** columns.
- **v_RA_System_SMSInstalledSites** is joined to **v_R_System** by using the **ResourceID** columns.

## Columns in the SQL statement

Use the following report columns, in the order listed:

1.  **Netbios_Name0** AS **[Computer Name]** from **v_R_System**
1.  **SMS_Installed_Sites0** AS **[Site Code]** from **v_RA_System_SMSInstalledSites**
1.  **LastHWScan** AS **[Last HWScan]** from **v_GS_WORKSTATION_STATUS**
1.  **DATEDIFF(day, v_GS_WORKSTATION_STATUS.LastHWScan, GETDATE())** AS **[Days Since Last HWScan]**

> [!NOTE]
> This report integrates two SQL Server functions to determine the difference between the last hardware scan date and the current date. To display this column, you can copy the whole line into the SQL statement, or you can copy **DATEDIFF(day, v_GS_WORKSTATION_STATUS.LastHWScan, GETDATE())** into the **Column** column and **Days Since Last HWScan** into the **Alias** column in Query Designer.

Sort the data in descending order, using the **LastHWScan** column.

## Filters in the SQL statement

The report SQL statement does not contain any filters.

## Report prompts

The Configuration Manager report should contain a report prompt for the computer name that will be reported on.

## Solution

See [Advanced exercise 2 solution: Create a new report for hardware inventory in Configuration Manager](advanced-exercise-2-solution-create-new-report-hardware-inventory-configuration-manager.md) for detailed information about how to create this report.

## See also

[Exercise 1: run an existing Configuration Manager report](exercise-1-run-existing-configuration-manager-report.md)  
[Advanced exercise 2 solution: Create a new report for hardware inventory in Configuration Manager](advanced-exercise-2-solution-create-new-report-hardware-inventory-configuration-manager.md)
