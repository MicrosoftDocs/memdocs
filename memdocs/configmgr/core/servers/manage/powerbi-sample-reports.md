---
title: Install Power BI sample reports
titleSuffix: Configuration Manager
description: Learn how to install the Power BI sample reports in Configuration Manager
ms.date: 06/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
---

# Install Power BI sample reports
<!--5679791-->
*Applies to: Configuration Manager (current branch)*

Starting in version 2002, you can integrate [Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) with Configuration Manager reporting. There are sample reports available for download that you can install in Configuration Manager. This article explains how to install the Power BI sample reports in Configuration Manager.

## Prerequisites

- Configuration Manager reporting services point with [Power BI Report Server integrated](powerbi-report-server)
- [Microsoft Power BI Desktop (Optimized for Power BI Report Server - September 2019)](https://www.microsoft.com/download/details.aspx?id=57271), or later

    > [!IMPORTANT]
    > - Only use versions of Power BI Desktop from the [Microsoft Download Center](https://www.microsoft.com/download/), don't use a version from the Microsoft Store.
    > - Only use a version of [Power BI Desktop that states it's **Optimized for Power BI Report Server**](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## Download the sample reports

To download the sample reports:

1. Download the Power BI sample reports from the [Microsoft Download Center](https://www.microsoft.com/download).
1. Save the `ConfigMgrSamplePowerBIReports.exe` file. 
1. Move the file to a computer with Microsoft Power BI Desktop (Optimized for Power BI Report Server) installed if you downloaded it from a different device.
1. Run the `ConfigMgrSamplePowerBIReports.exe` file to extract the .pbit files.

## Install the sample reports

To install the sample reports:

1. On the Power BI Report server, create a new folder called `Sample Reports` in the root Configuration Manager reporting folder.
   
   :::image type="complex" source="media/create-sample-reports-folder.png" alt-text="Create Sample Report folder in the root Configuration Manager reporting folder" lightbox="media/create-sample-reports-folder.png":::
:::image-end:::

1. Launch Microsoft Power BI Desktop (Optimized for Power BI Report Server).
1. Select **File** then **Open** and navigate to where you saved the extracted .pbit files.
1. Select one of the .pbit files you extracted from the `ConfigMgrSamplePowerBIReports.exe` file.
1. Specify your Configuration Manager database name and database server name when prompted, then select **Load**.
   - When loading or applying the data model, ignore any errors if you come across one.
   
    :::image type="complex" source="media/sample-report-database.png" alt-text="Specify the database and database server name" lightbox="media/sample-report-database.png":::
:::image-end:::
1. When the report data is loaded, select **File** > **Save As**, then select **Power BI Report Server**.
   
   :::image type="complex" source="media/save-powerbi-report-server.png" alt-text="Save as Power BI Report Server" lightbox="media/save-powerbi-report-server.png":::

1. Save the report to the `Sample Reports` folder you created on the reporting point.
     
   :::image type="complex" source="media/save-sample-report.png" alt-text="Save to the Sample Reports folder" lightbox="media/save-sample-report.png":::

1. Repeat the steps for any other sample reports. When you're done, close Microsoft Power BI Desktop (Optimized for Power BI Report Server).
1. In the Configuration Manager console, go to **Monitoring** > **Power BI Reports** > **Sample Reports**.
1. Right-click on one of the reports and select **Run in Browser** to launch the report.

   :::image type="complex" source="media/view-powerbi-report.png" alt-text="Run the sample report from the Configuration Manager console" lightbox="media/view-powerbi-report.png":::

## Next steps

[Integrate with Power BI Report Server](powerbi-report-server.md)