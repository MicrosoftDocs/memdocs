---
title: How to run reports
titleSuffix: Configuration Manager
description: Information about how to access reports in the Configuration Manager console or by using Report Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to


ms.assetid: 2020b94b-fc6f-4a70-91fb-51df948b9cb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# How to run Configuration Manager reports

Reports in Configuration Manager are stored in SQL Server Reporting Services, and the data rendered in the report is retrieved from the Configuration Manager site database. You can access reports in the Configuration Manager console or by using Report Manager, which you access in a web browser. You can open reports on any computer that has access to the computer that is running SQL Server Reporting Services, and you must have sufficient rights to view the reports. When you run a report, the report title, description, and category are displayed in the language of the local operating system.

## How to run a Configuration Manager report

Use the following procedures to run a Configuration Manager report.

> [!WARNING]
> To run reports, you must have **Read** rights for the **Site** permission and the **Run Report** permission that is configured for specific objects.

Report Manager is a web-based report access and management tool that you use to administer a single report server instance on a remote location over an HTTP connection. You can use Report Manager for operational tasks, for example, to view reports, modify report properties, and manage associated report subscriptions. This topic provides the steps to view a report and modify report properties in Report Manager, but for more information about the other options that Report Manager provides, see Report Manager in SQL Server&nbsp;2008 Books Online.

### To run a report in the Configuration Manager console

1. In the Configuration Manager console, select **Monitoring**.
1. In the **Monitoring** workspace, expand **Reporting**, and then select **Reports** to list the available reports.
    > [!TIP]
    > If no reports are listed, verify that the reporting services point is installed and configured. For more information, see the topic [Configuring Reporting in Configuration Manager](../../../../core/servers/manage/configuring-reporting.md).

1. Select the report that you want to run, and then on the **Home** tab, in the **Report Group** section, select **Run** to open the report.
1. When there are required parameters, specify the parameters, and then select **View Report**.

### To run a report in a web browser

1. In your web browser, enter the Report Manager URL, for example, `http://Server1/Reports`. You can determine the Report Manager URL on the **Report Manager URL** page in Reporting Services Configuration Manager.
1. In Report Manager, select the report folder for Configuration Manager, for example, ConfigMgr\_CAS.

    > [!TIP]
    > If no reports are listed, verify that the reporting services point is installed and configured. For more information, see the topic [Configuring Reporting in Configuration Manager](../../../../core/servers/manage/configuring-reporting.md).

1. Select the report category for the report that you want to run, and then select the link for the report. The report opens in Report Manager.
1. When there are required parameters, specify the parameters, and then select **View Report**.

## See also

[How to view the SQL Statement for Configuration Manager reports](how-to-view-sql-statement-configuration-manager-reports.md)
