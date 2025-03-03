---
title: "'Advanced exercise 2 solution: Create a new report for hardware inventory'"
titleSuffix: Configuration Manager
description: Create the report for Advanced Exercise 2
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: d1b574f9-d765-4f37-a552-bd018ce86224
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Advanced exercise 2 solution: Create a new report for hardware inventory in Configuration Manager

The following procedure can be used to create the report for [Advanced exercise 2: Create a new report for hardware inventory in Configuration Manager](advanced-exercise-2-create-new-report-hardware-inventory-configuration-manager.md).

> [!NOTE]
> Depending on your experience at creating SQL Server reports, there are numerous paths you can use to create a report. You can use your preferred method of creating reports if you prefer.

## To create the hardware inventory information report

1. In the Configuration Manager console, select **Monitoring**.
1. In the **Monitoring** workspace, expand **Reporting**, and then select **Reports**.
1. In the **Home** tab, in the **Create** group, select **Create Report**.
1. On the **Information** page of the Create Report Wizard, select **SQL-based Report**, and then supply the following information:
    
   - **Name:** Enter **Hardware Inventory Information**.
   - **Description:** Enter **Displays the computer name, site code, the date of the last scan for hardware inventory, and the number of days since the last scan.**
   - **Server:** This field is automatically entered. Ensure that it matches the name of your Reporting Server.
   - **Path:** Select **Browse** to select the folder in which the new report will be stored. For this exercise, select **Hardware - General**.
    
1. To continue, select **Next**.
1. On the **Summary** page of the Create Report Wizard, review the information and then select **Next**.
1. On the **Completion** page of the Create Report Wizard, review the actions that were taken, and then select **Close**. Report Builder now opens to allow you to construct the report.
1. Next, you must create the datasets that this report will use to return results for the report. This report uses two datasets. The first of these is used to list computer names that can be selected to use as a basis for the report. The second contains the SQL statements for the report itself.
1. In the **Report Data** pane, right-click **Datasets** and then select **Add Dataset**.
1. On the **Query** page of the **Dataset Properties** dialog box, supply a name for the dataset, or use the default name, and then select **Use a dataset embedded in my report**.
1. In the **Data source** drop-down list, select the data source you want to use for the report. This is typically automatically generated and will begin with **AutoGen\_**.
1. Select a query type of **Text**, and then enter the following query in the **Query** field.

   ```sql 
   SELECT DISTINCT SYS.Netbios_Name0 
   ��from v_R_System SYS WHERE SYS.Client0=1 
   ��ORDER By SYS.Netbios_Name0
   ```    
1. Select **OK** to close the **Dataset Properties** dialog box. The new dataset, named by default **DataSet1** is now displayed in the **Datasets** node of the **Report Data** pane.
 
   You have now created the query that the report parameter will use to return the available client names from which you can choose to run the report.
    
1. Next create the parameter that the report will use to let you select the computer that will be reported on.

   In the **Report Data** pane, right-click **Parameters**, and then select **Add Parameter**.
    
1. On the **General** page of the **Report Parameter Properties** dialog box, change the value in the **Prompt** field to read **Computer name**.
1. On the **Available Values** page of the **Report Parameter Properties** dialog box, select **Get values from a query**.
1. Select the following values:
    
   - **Dataset:** Choose **DataSet1**
   - **Value field:** Choose **Netbios\_Name0**
   - **Label field:** Choose **Netbios\_Name0**
    
1. Select **OK** to close the **Report Parameter Properties** dialog box. The new parameter **ReportParameter1** is displayed in the **Parameters** node of the **Report Data** pane.
1. At this point, run the report to check the parameter is working correctly. On the **Home** tab, in the **Views** group, select **Run**.
1. Verify that the **Computer name** field is shown. When you select this field, you should see all Windows client computers in the drop-down list.
1. On the **Home** tab, in the **Views** group, select **Design** to return to the design view.
1. Now, you must create the main dataset for the report.
    
   In the **Report Data** pane, right-click **Datasets** and then select **Add Dataset**.
1. On the **Query** page of the **Dataset Properties** dialog box, supply a name for the dataset, or use the default name, and then select **Use a dataset embedded in my report**.
1. In the **Data source** drop-down list, select the data source you want to use for the report. This is typically automatically generated and will begin with **AutoGen\_**.
1. Select a query type of **Text**, and then enter the following query in the **Query** field.

   ```sql 
   SELECT v_R_System.Netbios_Name0 AS [Computer Name], 
   ��v_RA_System_SMSInstalledSites.SMS_Installed_Sites0 AS [Site Code], 
   ��v_GS_WORKSTATION_STATUS.LastHWScan AS [Last HWScan], 
   ��DATEDIFF(day, v_GS_WORKSTATION_STATUS.LastHWScan, GETDATE()) AS [Days Since Last HWScan] 
   FROM v_GS_WORKSTATION_STATUS INNER JOIN v_R_System ON 
   ��v_GS_WORKSTATION_STATUS.ResourceID = v_R_System.ResourceID 
   ��INNER JOIN v_RA_System_SMSInstalledSites ON 
   ��v_R_System.ResourceID = v_RA_System_SMSInstalledSites.ResourceID 
   ORDER BY [Last HWScan] DESC 
   ```

1. Select **OK** to close the **Dataset Properties** dialog box.
1. On the **Insert** tab, in the **Data Regions** group, select **Table**, and then select **Table Wizard**.
1. On the **New Table or Matrix** page of the wizard, select **Choose an existing dataset in this report or a shared dataset**, select **DataSet2** and then select **Next**.
1. On the **Arrange fields** page of the wizard, drag **Computer\_Name**, **Site\_Code**, **Last\_HWScan** and **Days\_Since\_Last\_HWScan** from the **Available fields** pane, to the **Values** pane.
1. Select **Next** to see a preview of your report, and then select **Next** again.
1. On the **Choose a style** page of the wizard, choose one of the available themes for the report, and then select **Finish**.
1. On the **Home** tab, in the **Views** group, select **Run**.
1. In the **Computer name** field, select a computer from the drop-down list, and then select **View Report**.
1. Verify that the data in the report is as expected.
1. Save and close the report in Report Builder.

The new report is now available in the Configuration Manager console.

## Next steps

Report builder includes many options to change elements of reports, including themes, column headings and more. Consult your Report Builder help for more information.

## See also

[Advanced exercise 2: Create a new report for hardware inventory in Configuration Manager](advanced-exercise-2-create-new-report-hardware-inventory-configuration-manager.md)
