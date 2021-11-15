---
title: Install Power BI sample reports
titleSuffix: Configuration Manager
description: Learn how to install the Power BI sample reports in Configuration Manager
ms.date: 11/03/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Install Power BI sample reports
<!--5679791, 10123832, 10131458, 10488910-->
*Applies to: Configuration Manager (current branch)*

You can integrate [Power BI Report Server](/power-bi/report-server/get-started) with Configuration Manager reporting. There are sample reports available for download that you can install in Configuration Manager. This article explains how to install the Power BI sample reports in Configuration Manager.

## Prerequisites

- Configuration Manager reporting services point with [Power BI Report Server integrated](powerbi-report-server.md)

- Microsoft Power BI Desktop (Optimized for Power BI Report Server). Use a version released between September 2019 and [January 2021](https://www.microsoft.com/download/details.aspx?id=55330). For versioning information, see the [Change log for Power BI Report Server](/power-bi/report-server/changelog). <!--12428948, Power BI Desktop versioning information, latest version link, (currently unsupported with CM) is https://www.microsoft.com/download/details.aspx?id=57271 -->

    > [!IMPORTANT]
    > Use versions of Power BI Desktop:
    > - That are from the [Microsoft Download Center](https://www.microsoft.com/download/). Don't use a version from the Microsoft Store
    > - [That states they're **Optimized for Power BI Report Server**](/power-bi/report-server/install-powerbi-desktop). Don't use versions that aren't **Optimized for Power BI Report Server**.
    > - That were released no earlier than September 2019 and no later than January 2021. [Microsoft Power BI Desktop (Optimized for Power BI Report Server - January 2021)](https://www.microsoft.com/download/details.aspx?id=55330) is recommended. <!--12428948, Power BI Desktop versioning information, latest version link, (currently unsupported with CM) is https://www.microsoft.com/download/details.aspx?id=57271 -->

## Download the sample reports

To download the sample reports:

1. Download the Power BI sample reports from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452).

1. Save the `ConfigMgrSamplePowerBIReports.exe` file.

1. Move the file to a computer with Microsoft Power BI Desktop (Optimized for Power BI Report Server) installed if you downloaded it from a different device.

1. Run the `ConfigMgrSamplePowerBIReports.exe` file to extract the .pbit files.

> [!NOTE]
> Some of the sample reports are also available for download in [Community hub](community-hub.md).
> - Community hub direct link to the [Software Update Compliance Status sample report](https://communityhub.microsoft.com/item/10428)
> - Community hub direct link to the [Software Update Deployment Status sample report](https://communityhub.microsoft.com/item/10429)

## Install the sample reports

To install the sample reports:

1. On the Power BI Report server, create a new folder called `Sample Reports` in the root Configuration Manager reporting folder.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Creating the Sample Report folder in the root Configuration Manager reporting folder from " lightbox="media/create-sample-reports-folder.png":::

1. Launch Microsoft Power BI Desktop (Optimized for Power BI Report Server).

1. Select **File** then **Open** and navigate to where you saved the extracted .pbit files.

1. Select one of the .pbit files you extracted from the `ConfigMgrSamplePowerBIReports.exe` file.

1. Specify your Configuration Manager database name and database server name when prompted, then select **Load**.

    :::image type="content" source="media/sample-report-database.png" alt-text="Specify the database and database server name" lightbox="media/sample-report-database.png":::

    > [!NOTE]
    > When loading or applying the data model, ignore any errors if you come across one. For example, if you see the following error: "Connecting to tables from more than one database isn't supported in DirectQuery mode", select **Close**. Then refresh the data source settings:
    >
    > 1. In Power BI Desktop, in the ribbon, select **Edit Queries**, and then select **Data source settings**.
    > 1. Select **Change Source**, confirm your server and database names, and select **OK**.
    > 1. Close the data source settings window, and then select **Apply changes**.

1. When the report data is loaded, select **File** > **Save As**, then select **Power BI Report Server**.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Save as Power BI Report Server" lightbox="media/save-powerbi-report-server.png":::

1. Save the report to the `Sample Reports` folder you created on the reporting point.

    :::image type="content" source="media/save-sample-report.png" alt-text="Save to the Sample Reports folder" lightbox="media/save-sample-report.png":::

1. Repeat the steps for any other sample reports. When you're done, close Microsoft Power BI Desktop (Optimized for Power BI Report Server).

1. In the Configuration Manager console, go to **Monitoring** > **Power BI Reports** > **Sample Reports**.

1. Right-click on one of the reports and select **Run in Browser** to launch the report.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Run the sample report from the Configuration Manager console" lightbox="media/view-powerbi-report.png":::

## Sample reports

The following sample Power BI reports are included in the download:

- Software Update Compliance Status
- Software Update Deployment Status
- Client Status
- Content Status
- Microsoft Edge Management
