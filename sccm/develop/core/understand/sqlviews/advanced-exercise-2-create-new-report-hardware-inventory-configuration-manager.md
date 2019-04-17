---
title: 'Advanced Exercise 2: Create a New Report for Hardware Inventory'
titleSuffix: Configuration Manager
description: Create a Configuration Manager report that displays hardware inventory information.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: d7e964d3-5c1a-42c5-81fd-57fc833cb55a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Advanced Exercise 2: Create a New Report for Hardware Inventory in Configuration Manager

In this exercise, you will create a Configuration Manager report that displays the computer name, site code, the date of the last scan for hardware inventory, and the number of days since the last scan for a specified computer.

> [!IMPORTANT]
> Before you begin this exercise, you should review the basic exercises to learn about the report elements, the properties for a report, and the different ways to create the report SQL statement.

## Report Requirements

Use the following report requirements to create the new report.

## SQL Server Views in the SQL Statement

Use the following Configuration Manager SQL views when creating the report SQL statement:

- **v_GS_WORKSTATION_STATUS**: This SQL view contains the date and time of the last scan for hardware inventory reported by client computers. For more information about this SQL view, see [Hardware Inventory Views in Configuration Manager](hardware-inventory-views-configuration-manager.md).
- **v_R_System**: This SQL view contains all of the discovered system resources. For more information about this SQL view, see [Discovery Views in Configuration Manager](discovery-views-configuration-manager.md).
- **v_RA_System_SMSInstalledSites**: This SQL view contains the installed site for all client computers. For more information about this SQL view, see [Discovery Views in Configuration Manager](discovery-views-configuration-manager.md).

## JOINS in the SQL Statement

Create the following JOINS in the SQL statement:

- **v_GS_WORKSTATION_STATUS** is joined to **v_R_System** by using the **ResourceID** columns.
- **v_RA_System_SMSInstalledSites** is joined to **v_R_System** by using the **ResourceID** columns.

## Columns in the SQL Statement

Use the following report columns, in the order listed:

1.  **Netbios_Name0** AS **[Computer Name]** from **v_R_System**
1.  **SMS_Installed_Sites0** AS **[Site Code]** from **v_RA_System_SMSInstalledSites**
1.  **LastHWScan** AS **[Last HWScan]** from **v_GS_WORKSTATION_STATUS**
1.  **DATEDIFF(day, v_GS_WORKSTATION_STATUS.LastHWScan, GETDATE())** AS **[Days Since Last HWScan]**

> [!NOTE]
> This report integrates two SQL functions to determine the difference between the last hardware scan date and the current date. To display this column, you can copy the whole line into the SQL statement, or you can copy **DATEDIFF(day, v_GS_WORKSTATION_STATUS.LastHWScan, GETDATE())** into the **Column** column and **Days Since Last HWScan** into the **Alias** column in Query Designer.

Sort the data in descending order, using the **LastHWScan** column.

## Filters in the SQL Statement

The report SQL statement does not contain any filters.

## Report Prompts

The Configuration Manager report should contain a report prompt for the computer name that will be reported on.

## Solution

See [Advanced Exercise 2 Solution: Create a New Report for Hardware Inventory in Configuration Manager](advanced-exercise-2-solution-create-new-report-hardware-inventory-configuration-manager.md) for detailed information about how to create this report.

## See Also

[Exercises for Creating Custom Reports in Configuration Manager](exercises-creating-custom-reports-configuration-manager.md)  
[Advanced Exercise 2 Solution: Create a New Report for Hardware Inventory in Configuration Manager](advanced-exercise-2-solution-create-new-report-hardware-inventory-configuration-manager.md)