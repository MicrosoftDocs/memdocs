---
title: Integrate with Power BI Report Server
titleSuffix: Configuration Manager
description: Integrate Power BI Report Server with Configuration Manager reporting for modern visualization and better performance.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Integrate with Power BI Report Server

*Applies to: Configuration Manager (current branch)*

<!--3721603-->

Starting in version 2002, you can integrate [Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) with Configuration Manager reporting. This integration gives you modern visualization and better performance. It adds console support for Power BI reports similar to what already exists with SQL Server Reporting Services.

Save Power BI Desktop report files (.PBIX) and deploy them to the Power BI Report Server. This process is similar as with SQL Server Reporting Services report files (.RDL). You can also launch the reports in the browser directly from the Configuration Manager console.

## Prerequisites

- Power BI Report Server license. For more information, see [Licensing Power BI Report Server](https://docs.microsoft.com/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Download [Microsoft Power BI Report Server-September 2019](https://www.microsoft.com/download/details.aspx?id=57270), or later.

    > [!NOTE]
    > Don't install Power BI Report Server right away. For the proper process based on your environment, see [Configure the reporting services point](#configure-the-reporting-services-point).

- Download [Microsoft Power BI Desktop (Optimized for Power BI Report Server - September 2019)](https://www.microsoft.com/download/details.aspx?id=57271), or later.

    > [!IMPORTANT]
    > Only use this version of Power BI Desktop, don't use the version from the Microsoft Store.

- Power BI integration uses the same role-based administration for reporting.

## Configure the reporting services point

This process varies depending upon whether you already have this role in the site.

### You have a reporting services point

Only use this process if you already have a reporting services point in the site. Do all steps of this process on the same server:

1. In **Reporting Server Configuration Manager**, back up the **Encryption Keys**. For more information, see [SSRS Encryption Keys - Back Up and Restore Encryption Keys](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > If you skip this step, you'll lose access to any custom reports in SQL Server Reporting Services.

1. Remove the reporting services point role from the site.

1. Uninstall SQL Server Reporting Services, but keep the database.

1. Install Power BI Report Server.

1. Configure the Power BI Report Server

    1. Use the previous report server database.

    1. Use **Reporting Server Configuration Manager** to restore the **Encryption Keys**.

1. Add the reporting services point role in Configuration Manager.

### You don't have a reporting services point

Only use this process if you don't already have a reporting services point in the site. Do all steps of this process on the same server:

1. Install Power BI Report Server.

2. Add the reporting services point role in Configuration Manager. For more information, see [Configure reporting](/configmgr/core/servers/manage/configuring-reporting).

## Configure the Configuration Manager console

1. On a computer that has the Configuration Manager console, update the Configuration Manager console to the latest version.

1. Install Power BI Desktop. Make sure the language is the same.

1. After it installs, launch Power BI Desktop at least once before you open the Configuration Manager console.

## Create Power BI reports

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Reporting**, and select the new **Power BI Reports** node.

1. In the ribbon, select **Create Report**. This action opens Power BI Desktop.

1. Create a report in Power BI Desktop.

    - In Power BI Desktop, when you connect to a data source, select **DirectQuery** for the Connection settings.

    - Only use supported SQL views in these reports. For more information, see [Creating custom reports by using SQL Server views in Configuration Manager](/configmgr/develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views).

1. When the report is ready to save, go to the **File** menu, select **Save as**, then choose **Power BI Report Server**.

1. In the **Power BI Report Server Selection** window, enter the URL for the reporting services point as the **New report server address**. For example, `https://rsp.contoso.com/Reports`.

In the Configuration Manager console, you see the new report in the list of Power BI Reports.

## Next steps

After you create a report, use the following actions in the Configuration Manager console:

- **Run in Browser**: Opens the Power BI report in the web browser. Share this URL with others, for example: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > You can only view these reports in the web browser.

- **Edit**: Make changes to the report in Power BI Desktop. For an existing report, use the **Save** option to save changes back to the report server.

For more information on log files to use for reporting, see [Log file reference - Reporting](/configmgr/core/plan-design/hierarchy/log-files#BKMK_ReportLog).
