---
title: How to view the SQL Statement for reports
titleSuffix: Configuration Manager
description: Information to find out what SQL statement is used in a Configuration Manager report.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to


ms.assetid: e596b1be-c09e-4e44-a400-43345ab0f71b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# How to view the SQL statement for Configuration Manager reports

Reports in Configuration Manager can be based on simple SQL statements or very complex ones that prompt the user for information, join several Microsoft SQL Server views, and use filters to limit the results. Use the following procedure to find out what SQL statement is used in a Configuration Manager report.

## To view the SQL statement for a report

1. In the Configuration Manager console, select **Monitoring**.
1. In the **Monitoring** workspace, expand **Reporting**, and then select **Reports**.
1. Select the report for which you want to view the SQL statement and then, in the **Home** tab, in the **Report Group** group, select **Edit**.
1. The Report Builder window opens. In the **Report Data** pane, expand **Datasets** to view the data sets for the report.
1. Double-click a dataset to open the **Dataset Properties** dialog box.

   The first dataset is typically (but not always), the main SQL statement for the report. Other datasets might contain the SQL statements that can be used to present a list of items for a user to choose from, such as a list of computers.
1. You can view and modify the SQL statement for the dataset in the **Query** field.
1. Close the **Dataset Properties** dialog box.
1. Close Report Builder.

## See also

[How to modify Configuration Manager reports](how-to-modify-configuration-manager-reports.md)
