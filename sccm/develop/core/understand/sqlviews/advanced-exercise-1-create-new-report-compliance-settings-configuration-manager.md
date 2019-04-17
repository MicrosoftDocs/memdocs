---
title: 'Advanced Exercise 1: Create a New Report for Compliance Settings'
titleSuffix: Configuration Manager
description: Create a Configuration Manager report that displays the name and description of the configuration baselines.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 9b87348f-21d1-40ba-9d3d-c56dd7bae60d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Advanced Exercise 1: Create a New Report for Compliance Settings in Configuration Manager

In this exercise, you will create a Configuration Manager report that displays the name and description of the configuration baselines that are deployed to a specified computer and whether the computer returns compliant or noncompliant for the configuration baseline.

> [!IMPORTANT]
> Before you begin this exercise, you should review the basic exercises to learn about the report elements, the properties for a report, and the different ways to create the report SQL statement.

## Report Requirements

Use the following report requirements to create the new report.

## SQL Server Views in the SQL Statement

Use the following Configuration Manager SQL views when creating the report SQL statement:

- **v_CICurrentComplianceStatus:** This SQL view contains compliance information for all configuration items. For more information about this SQL view, see [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md).

- **v_ConfigurationItems:** This SQL view contains all of the configuration items. For more information about this SQL view, see [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md).

- **v_LocalizedCIProperties:** This SQL view contains the localized titles and descriptions for the configuration items. For more information about this SQL view, see [Compliance Settings Views in Configuration Manager](compliance-settings-views-configuration-manager.md).

- **v_R_System:** This SQL view contains all of the discovered system resources. For more information about this SQL view, see [Discovery Views in Configuration Manager](discovery-views-configuration-manager.md).

## JOINS in the SQL Statement

Create the following JOINS in the SQL statement:

- **v_CICurrentComplianceStatus** is joined to **v_ConfigurationItems** by using the **CI_ID** column.

- **v_CICurrentComplianceStatus** is joined to **v_LocalizedCIProperties** by using the **CI_ID** column.

- **v_CICurrentComplianceStatus** is joined to **v_R_System** by using the **ResourceID** column.

## Columns in the SQL Statement

Use the following report columns, in the order listed:

1. **ComplianceStateName** from **v_CICurrentComplianceStatus**

1. **DisplayName** from **v_LocalizedCIProperties**

1. **Description** from **v_LocalizedCIProperties**

1. **Netbios_Name0** from **v_R_System**

1. **CIType_ID** from **v_ConfigurationItems** (Not displayed)

Sort the returned data in ascending order, using the **Netbios_Name0** column.

## Filters in the SQL Statement

The report SQL statement should meet the following filtering criteria:

- Select only configuration baselines. You can filter specifically on configuration baselines by selecting the **CIType_ID**. Configuration baselines are CI type 2.

## Report Prompts

The Configuration Manager report should contain a report prompt for the computer name that will be reported on.

## Solution

See [Advanced Exercise 1 Solution: Create a New Report for Compliance Settings in Configuration Manager](advanced-exercise-1-solution-create-new-report-compliance-settings-configuration-manager.md) for detailed information about how to create this report.

## See Also

[Exercises for Creating Custom Reports in Configuration Manager](exercises-creating-custom-reports-configuration-manager.md)  
[Advanced Exercise 1 Solution: Create a New Report for Compliance Settings in Configuration Manager](advanced-exercise-1-solution-create-new-report-compliance-settings-configuration-manager.md)