---
title: 'Exercise 3: Create a new report'
titleSuffix: Configuration Manager
description: Create a simple report and configure the report properties.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 16e62994-a1e2-4ee9-bf62-3985ecb1c745
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# Exercise 3: Create a new Configuration Manager report

In this exercise, you will create a simple report in Microsoft SQL Server Report Builder, and configure the report properties.

The report displays all collections that administrative users have created and excludes the built-in collections. The results will display the collection ID and name, the last collection refresh time and the date of the last collection membership change.

## To create a new report

1. In the Configuration Manager console, select **Monitoring**.
1. In the **Monitoring** workspace, expand **Reporting**, and then select **Reports**.
1. In the **Home** tab, in the **Create** group, select **Create Report**.
1. On the **Information** page of the Create Report Wizard, select **SQL-based Report**, and then configure the following properties:
   - **Name:** Enter **All collections created by administrative users**.
   - **Description:** Enter **Displays all collections that were created by an administrative user (excludes built-in collections).**
   - **Path:** Select **Browse**, and then select the **Site � General** folder to store the report.
1. Select **Next**.
1. On the **Summary** page of the Create Report Wizard, review the actions that will be taken and then select **Next**.
1. On the **Completion** page of the wizard, review any messages and then select **Close**.
1. Report Builder opens. In the **Report Data** pane, right-click **Datasets**, and then select **Add Dataset**.
1. On the **Query** page of the **Dataset Properties** dialog box, select **Use a dataset embedded in my report**.
1. In the **Data source** drop-down list, select the data source you want to use for the report. This is typically automatically generated and will begin with **AutoGen\_**.
1. Select a query type of **Text**, and then enter the following query in the **Query** field.

   ```sql    
   SELECT
   v_Collections.CollectionID,
   v_Collections.CollectionName, 
   v_Collections.LastRefreshTime, 
   v_Collections.LastMemberChangeTime
   FROM
   V_Collections
   WHERE
   IsBuiltIn=0
   ```
  
1. Select **OK** to close the **Dataset Properties** dialog box.
1. In Report Builder, on the **Insert** tab, in the **Data Regions** group, select **Table**, and then select **Table Wizard**.
1. On the **Choose a dataset** page of the **New Table or Matrix** wizard, select **Choose an existing dataset in this report or a shared dataset**, and then select the dataset you previously created, **Dataset1**.
1. Select **Next**.
1. On the **Arrange fields** page of the **New Table or Matrix** wizard, drag **CollectionID**, **CollectionName**, **LastRefreshTime** and **LastMemberChangeTime** from the **Available fields** field to the **Values** field.
1. Select **Next**.
1. On the **Choose the layout** page of the **New Table or Matrix** wizard, select **Next**.
1. On the **Choose a style** page of the wizard, choose one of the available themes for the report, and then select **Finish**.
1. Verify that the data in the report is as expected.
1. Save and close the report in Report Builder.

The new report is now available in the Configuration Manager console.
    
## Next steps

Report builder includes many options to change elements of reports, including themes, column headings and more. Consult your Report Builder help for more information.

## See also

[Exercise 1: Run an existing Configuration Manager report](exercise-1-run-existing-configuration-manager-report.md)
