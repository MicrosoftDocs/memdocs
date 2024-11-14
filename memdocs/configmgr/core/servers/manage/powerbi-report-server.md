---
title: Integrate with Power BI Report Server
titleSuffix: Configuration Manager
description: Integrate Power BI Report Server with Configuration Manager reporting for modern visualization and better performance.
ms.date: 04/08/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Integrate with Power BI Report Server

*Applies to: Configuration Manager (current branch)*

<!--3721603-->

You can integrate [Power BI Report Server](/power-bi/report-server/get-started) with Configuration Manager reporting. This integration gives you modern visualization and better performance. It adds console support for Power BI reports similar to what already exists with SQL Server Reporting Services.

Save Power BI Desktop report files (.PBIX) and deploy them to the Power BI Report Server. This process is similar as with SQL Server Reporting Services report files (.RDL). You can also launch the reports in the browser directly from the Configuration Manager console.

## Prerequisites

- Power BI Report Server license. For more information, see [Licensing Power BI Report Server](/power-bi/report-server/get-started#licensing-power-bi-report-server).

- Download [Microsoft Power BI Report Server-September 2024](https://www.microsoft.com/download/details.aspx?id=105945), or later.
   - Don't install Power BI Report Server right away. For the proper process based on your environment, see [Configure the reporting services point](#configure-the-reporting-services-point).
   - It's recommended that you use a [supported version of Power BI Report Server](/power-bi/report-server/support-timeline). For versioning information, see the [Change log for Power BI Report Server](/power-bi/report-server/changelog).

- Download Microsoft Power BI Desktop (Optimized for Power BI Report Server - September 2019), or later. It's recommended that you use a [supported version](/power-bi/report-server/support-timeline). For versioning information, see the [Change log for Power BI Report Server](/power-bi/report-server/changelog).

   Use versions of Power BI Desktop:
   - That are from the [Microsoft Download Center](https://www.microsoft.com/download/). Don't use a version from the Microsoft Store.
   - [That states they're **Optimized for Power BI Report Server**](/power-bi/report-server/install-powerbi-desktop). Don't use versions that aren't **Optimized for Power BI Report Server**.

   > [!Note]
   > When using Configuration Manager version 2111 or earlier with Power BI Desktop (Optimized for Power BI Report Server - May 2021) or later, you may notice the following behavior:<!--12428948, 2203CB-12487076 -->
   > - You might experience delays updating the data source on newly updated reports.
   > - You may receive `The remote server returned an error; (400) Bad Request.` errors in the **SRSRP.log**.
   > For more information about the relevant change to Power BI Desktop (optimized for Power BI Report Server) May 2021, see [Change data source connection strings in Power BI reports](/power-bi/report-server/connect-data-source-apis). The version before the connection change ocurred is January 2021.
 
- Power BI integration uses the same role-based administration for reporting.
   - Power BI Report Server doesn't support reports that are enabled for role-based access. All report viewers will see the same results, whatever their assigned scope.

## Configure the reporting services point

This process varies depending upon whether you already have this role in the site.

### You have a reporting services point

Only use this process if you already have a reporting services point in the site. Do all steps of this process on the same server:

1. In **Reporting Services Configuration Manager**, back up the **Encryption Keys**. For more information, see [SSRS Encryption Keys - Back Up and Restore Encryption Keys](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > If you skip this step, you'll lose access to any custom reports in SQL Server Reporting Services.

1. Remove the reporting services point role from the site.

1. Uninstall SQL Server Reporting Services, but keep the database.

1. Install Power BI Report Server.

1. Configure the Power BI Report Server

    1. Use the previous report server database.

    1. Use **Reporting Services Configuration Manager** to restore the **Encryption Keys**.

     - Before you add the reporting services point role in Configuration Manager, use SQL Server Reporting Services Configuration Manager to test and verify the configuration. For more information, see [Verify SQL Server Reporting Services installation](configuring-reporting.md#verify-sql-server-reporting-services-installation).<!-- MEMDocs #713 -->

1. Add the reporting services point role in Configuration Manager.

### You don't have a reporting services point

Only use this process if you don't already have a reporting services point in the site. Do all steps of this process on the same server:

1. Install Power BI Report Server.

2. Add the reporting services point role in Configuration Manager. For more information, see [Configure reporting](configuring-reporting.md).

## Configure the Configuration Manager console

1. On a computer that has the Configuration Manager console, update the Configuration Manager console to the latest version.

1. Install Power BI Desktop. Make sure the language is the same and verify the [versioning prerequisites](#prerequisites).

1. After it installs, launch Power BI Desktop at least once before you open the Configuration Manager console.

## Create Power BI reports

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Reporting**, and select the new **Power BI Reports** node.

1. In the ribbon, select **Create Report**. This action opens Power BI Desktop.

1. Create a report in Power BI Desktop.

    - In Power BI Desktop, when you connect to a data source, select **DirectQuery** for the Connection settings.

    - Only use supported SQL views in these reports. For more information, see [Creating custom reports by using SQL Server views in Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. When the report is ready to save, go to the **File** menu, select **Save as**, then choose **Power BI Report Server**.

1. In the **Power BI Report Server Selection** window, enter the URL for the reporting services point as the **New report server address**. For example, `https://rsp.contoso.com/Reports`. Select **OK**.

1. In the **Save report** window, double-click the `ConfigMgr_<SiteCode>` folder. For example, `ConfigMgr_PS1`, where `PS1` is the ConfigMgr site code. You can optionally choose or create (from the report server) a sub folder to store it in.
    > [!TIP]
    > Reports and report folders with Power BI reports must be located in the `ConfigMgr_<SiteCode>` folder on the report server or they won't appear in the Configuration Manager console.

1. In **File name**, enter a name for the report.

In the Configuration Manager console, you see the new report in the list of Power BI Reports. If you don't see your reports, verify that you saved the reports to the `ConfigMgr_<SiteCode>` folder.

There are sample reports available for download. For more information, see [Install Power BI sample reports](powerbi-sample-reports.md).

## <a name="bkmk_community_hub"></a> Power BI report templates in Community hub

<!--5679831-->

Using [Community hub](community-hub.md), you can share Power BI report templates you've created and download templates that others have shared.

### Contributing a Power BI report template (PBIT) files to Community hub

1. Open the Configuration Manager console and go to **Community** > **Community hub**
1. If needed, select **Sign in** to sign into GitHub. You'll see the **Your hub** link after signing in.
1. Select **Your hub** then **Add an item** to launch the **Contribute item wizard**.
1. For the **Type**, choose **Power BI Report Template** then select **Browse**.
1. Choose the `.pbit` file you want to contribute, then select **Open**.
1. Edit the **Name** and **Description** for the report template then select **Next** when done.
1. On the **Organization** page, select the **GitHub Organization** to use for [organization branding](community-hub-contribute.md#bkmk_brand) if needed. Select **Next** to upload the template.
1. Once the item is uploaded, you'll be given the pull request URL of the change for monitoring.
1. Select **Close** when you're done to exit the wizard.

### Downloading a Power BI report template (PBIT) file from Community hub

1. Open the Configuration Manager console, go to **Community** > **Community hub**.
1. From **All objects** or a search, choose a Power BI report template, then select **Download**.
1. Select a file location to save the downloaded `.pbit` file and choose **Save**.
1. If Power BI Desktop (Optimized for Power BI Report Server) is installed, you'll be prompted to open the `.pbit` file.
1. Select **Yes** and Power BI Desktop (Optimized for Power BI Report Server) will load the `.pbit` file.
1. Specify your Configuration Manager database name and database server name when prompted, then select **Load**.

    > [!NOTE]
    > When loading or applying the data model, ignore any errors if you come across one. For example, if you see the following error: "Connecting to tables from more than one database isn't supported in DirectQuery mode", select **Close**. Then refresh the data source settings:
    >
    > 1. In Power BI Desktop, in the ribbon, select **Edit Queries**, and then select **Data source settings**.
    > 1. Select **Change Source**, confirm your server and database names, and select **OK**.
    > 1. Close the data source settings window, and then select **Apply changes**.

1. When the report data is loaded, select **File** > **Save As**, then select **Power BI Report Server**.
1. Save the report to a folder on the root Configuration Manager reporting folder on the reporting point. You may want to create a `Downloaded Reports` folder for these items.
1. Repeat the steps for any other report templates that were downloaded. When you're done, close Microsoft Power BI Desktop (Optimized for Power BI Report Server).

## Known issues

There's a known issue with Power BI Report Server and email subscriptions. After you configure the email settings in the Reporting Services Configuration Manager, when you try to create a new subscription, the option to deliver a report by **Email** isn't available. To work around this issue, restart the Power BI Report Server service.<!-- 7698019 -->

## Next steps

After you create a report, use the following actions in the Configuration Manager console:

- **Run in Browser**: Opens the Power BI report in the web browser. Share this URL with others, for example: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > You can only view these reports in the web browser.

- **Edit**: Make changes to the report in Power BI Desktop. For an existing report, use the **Save** option to save changes back to the report server.

- **Add to Favorites**: Starting in version 2103, you can make a report a favorite. This action allows you to quickly access it from the **Favorites** node. For more information, see [Operations and maintenance for reporting](../../servers/manage/operations-and-maintenance-for-reporting.md#favorites).

For more information on log files to use for reporting, see [Log file reference - Reporting](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
