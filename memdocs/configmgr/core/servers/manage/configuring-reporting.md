---
title: Configure reporting
titleSuffix: Configuration Manager
description: How to set up reporting in your Configuration Manager hierarchy, including information about SQL Server Reporting Services.
ms.date: 04/01/2020
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

# Configure reporting in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before you can create, modify, and run reports in the Configuration Manager console, there are several configuration tasks to complete. Use this article to help you configure reporting in your Configuration Manager hierarchy.  

Before you install and configure SQL Server Reporting Services in your hierarchy, review the following Configuration Manager reporting articles:  

- [Introduction to reporting](introduction-to-reporting.md)  

- [Plan for reporting](planning-for-reporting.md)  

## SQL Server Reporting Services

SQL Server Reporting Services is a server-based reporting platform that provides comprehensive reporting functionality for different kinds of data sources. The reporting services point in Configuration Manager communicates with SQL Server Reporting Services to:

- Copy Configuration Manager reports to a specified report folder
- Configure Reporting Services settings
- Configure Reporting Services security settings

When you run a report, the Reporting Services component connects to the Configuration Manager site database to retrieve data.  

Before you can install the reporting services point in a Configuration Manager site, install and configure SQL Server Reporting Services on the target site system. For more information, see [Install SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services).  

### Verify SQL Server Reporting Services installation

Use the following procedure to verify that SQL Server Reporting Services is installed and running correctly.

1. Go to the **Start** menu on the site system, and open **Report Server Configuration Manager**. You may find it in the **Configuration Tools** section of the **Microsoft SQL Server** group.

2. In the **Reporting Services Configuration Connection** window, enter the name of the server that hosts SQL Server Reporting Services. Select the instance of SQL Server on which you installed SQL Server Reporting Services. Then select **Connect** to open Reporting Services Configuration Manager.  

3. On the **Report Server Status** page, verify that **Report Service Status** is **Started**. If it's not in this state, select **Start**.  

4. On the **Web Service URL** page, select the URL in **Report Service Web Service URLs**. This action tests the connection to the report folder. The browser might prompt you for credentials. Verify that the webpage opens successfully.

5. On the **Database** page, verify that the **Report Server Mode** is set to **Native**.  

6. On the **Report Manager URL** page, select the URL in **Report Manager Site Identification**. This action tests the connection to the virtual directory for Report Manager. The browser might prompt you for credentials. Verify that the webpage opens successfully.

    > [!NOTE]  
    > Reporting in Configuration Manager doesn't require Reporting Services Report Manager. You only need it if you want to run reports in the browser or manage reports by using Report Manager.  

7. Select **Exit** to close Reporting Services Configuration Manager.  

## Configure reporting to use Report Builder 3.0

1. On the computer running the Configuration Manager console, open the Windows Registry Editor.  

2. Browse to `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting`.

3. Open the **ReportBuilderApplicationManifestName** key to edit the value data.  

4. Change the value to `ReportBuilder_3_0_0_0.application`, and then select **OK** to save.

5. Close the Windows Registry Editor.  

## Install a reporting services point

To manage reports at the site, install the reporting services point. The reporting services point:

- Copies report folders and reports to SQL Server Reporting Services
- Applies the security policy for the reports and folders
- Sets configuration settings in Reporting Services

### Requirements and limitations

Before you can view or manage reports in the Configuration Manager console, you need a reporting services point. Configure this site system role on a server with Microsoft SQL Server Reporting Services. For more information, see [Prerequisites for reporting](prerequisites-for-reporting.md).  

- When you select a site to install the reporting services point, users who will access the reports must be in the same security scope as the site where you install the role.  

- After you install a reporting services point on a site system, don't change the URL for the report server.

    For example, you create the reporting services point. You then modify the URL for the report server in Reporting Services Configuration Manager. The Configuration Manager console continues to use the old URL. You can't run, edit, or create reports from the console.

    If you need to change the report server URL, first remove the existing reporting services point. Change the URL, and then reinstall the reporting services point.  

- When you install a reporting services point, specify a [Reporting services point account](../../plan-design/hierarchy/accounts.md#reporting-services-point-account). For users from a different domain to run a report, create a two-way trust between domains. Otherwise the report fails to run.
  
- The account that runs Reporting Services service must belong to the domain local security group **Windows Authorization Access Group**. This grants the account **Allow Read** permissions on the **tokenGroupsGlobalAndUniversal** attribute for all user objects within the domain. Users in a different domain than the reporting services point account need a two-way trust between the domains to successfully run reports.

### <a name="bkmk_install"></a> Install the reporting services point on a site system  

For more information about configuring site systems, see [Install site system roles](../deploy/configure/install-site-system-roles.md).  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the  **Servers and Site System Roles** node.  

1. Add the reporting services point to a new or existing site system server:  

    - *New site system*: On the **Home** tab of the ribbon, in the **Create** group, select **Create Site System Server**. The **Create Site System Server Wizard** opens.  

    - *Existing site system*: Select the target server. On the **Home** tab of the ribbon, in the **Server** group, select **Add Site System Role**. The **Add Site System Roles Wizard** opens.  

1. On the **General** page, specify the general settings for the site system server. When you add the reporting services point to an existing server, verify the values that you previously configured.  

1. On the **System Role Selection** page, select **Reporting services point** in the list of available roles, and then select **Next**.  

1. On the **Reporting services point** page, configure the following settings:  

    - **Site database server name**: Specify the name of the server that hosts the Configuration Manager site database. The wizard typically retrieves the fully qualified domain name (FQDN) for the server. To specify a database instance, use the format &lt;*server name*>\&lt;*instance name*>. For example, `sqlserver\named1`.

    - **Database name**: Specify the Configuration Manager site database name. Select **Verify** to confirm that the wizard has access to the site database.  

        > [!IMPORTANT]  
        > The user account you use to create the reporting services point must have **Read** access to the site database. If the connection test fails, a red warning icon appears. Contextual hover text on the icon has the details of the failure. Correct the failure, and then select **Test** again.  

    - **Folder name**: Specify the folder name to create and use for Configuration Manager reports in Reporting Services.  

    - **Reporting Services server instance**: Select the instance of SQL Server for Reporting Services. If this page doesn't list any instances, verify that SQL Server Reporting Services is installed, configured, and started.  

        > [!IMPORTANT]  
        > Configuration Manager makes a connection in the context of the current user to WMI on the selected site system. It uses this connection to retrieve the instance of SQL Server for Reporting Services. The current user must have **Read** access to WMI on the site system, or the wizard can't get the Reporting Services instances.  

    - **Reporting services point account**: Select **Set**, and then select an account to use. SQL Server Reporting Services on the reporting services point uses this account to connect to the Configuration Manager site database. This connection is to retrieve the data for a report. Select **Existing account** to specify a Windows user account that you previously configured as a Configuration Manager account. Select **New account** to specify a Windows user account that's not currently configured for use. Configuration Manager automatically grants the specified user access to the site database. The specified Windows user account and password are encrypted and stored in the Reporting Services database. Reporting Services retrieves the data for reports from the site database by using this account and password.  

        > [!IMPORTANT]  
        > The account that you specify must have the **Log on locally** permission on the server that hosts the Reporting Services database.  

1. Complete the wizard.

After the wizard completes, Configuration Manager creates the report folders in Reporting Services. It then copies its reports to the specified report folders.  

> [!TIP]  
> To list only site systems that host the reporting services point site role, right-click **Servers and Site System Roles**, and select **Reporting services point**.  

### <a name="bkmk_languages"></a> Languages for reports

<!-- SCCMDocs#1067 -->

When Configuration Manager creates report folders and copies reports to the report server, it determines the appropriate language for the objects.

- Create report folders, copy reports

  - Create objects using locale of the site server OS

  - If the specific language pack isn't available, default to English (ENU)

- View reports in a web browser

  - Folder and report names: the same locale as the site server
  
  - Report contents: dynamic based on the browser locale

- View reports in the Configuration Manager console

  - Folder and report names: dynamic based on the locale of the console
  
  - Report contents: dynamic based on the locale of the console

When you install a reporting services point on a site without language packs, the reports are installed in English. If you install a language pack after you install the reporting services point, you must uninstall and reinstall the reporting services point for the reports to be available in the appropriate language pack language.  

For more information, see [Language packs](../deploy/install/language-packs.md).

### File installation and report folder security rights

Configuration Manager does the following actions to install the reporting services point and to configure Reporting Services:  

> [!IMPORTANT]  
> The site does these actions in the context of the account that's configured for the SMS_Executive service. Typically, this account is the site server local System account.  

- Install the reporting services point site role.  

- Create the data source in Reporting Services with the stored credentials that you specified in the wizard. This account is the Windows user account and password that Reporting Services uses to connect to the site database when you run reports.  

- Create the Configuration Manager root folder in Reporting Services.  

- Add the **ConfigMgr Report Users** and **ConfigMgr Report Administrators** security roles in Reporting Services.  

- Create subfolders, and then deploy Configuration Manager reports from `%ProgramFiles%\SMS_SRSRP` on the site server to Reporting Services.  

- Add the **ConfigMgr Report Users** role in Reporting Services to the root folders for all user accounts in Configuration Manager that have **Site Read** rights.  

- Add the **ConfigMgr Report Administrators** role in Reporting Services to the root folders for all user accounts in Configuration Manager that have **Site Modify** rights.  

- Retrieve the mapping between report folders and Configuration Manager secured object types. Configuration Manager maintains this map in the site database.  

- Configure the following rights for administrative users in Configuration Manager to specific report folders in Reporting Services:  

  - Add users and assign the **ConfigMgr Report Users** role to the associated report folder for administrative users who have **Run Report** permissions for the Configuration Manager object.  

  - Add users and assign the **ConfigMgr Report Administrators** role to the associated report folder for administrative users who have **Modify Report** permissions for the Configuration Manager object.  

Configuration Manager connects to Reporting Services and sets the permissions for users on the Configuration Manager and Reporting Services root folders and specific report folders. After the initial installation of the reporting services point, Configuration Manager connects to Reporting Services every 10 minutes to verify that the user rights configured on the report folders are the associated rights that are set for Configuration Manager users. When users are added or user rights are modified on the report folder by using Reporting Services Report Manager, Configuration Manager overwrites those changes by using the role-based assignments stored in the site database. Configuration Manager also removes users that don't have Reporting rights in Configuration Manager.  

### Reporting Services security roles

When Configuration Manager installs the reporting services point, it adds the following security roles in Reporting Services:  

- **ConfigMgr Report Users**: Users assigned with this security role can only run Configuration Manager reports.  

- **ConfigMgr Report Administrators**: Users assigned with this security role can do all tasks related to reporting in Configuration Manager.  

## <a name="bkmk_verify"></a> Verify installation

Verify the installation of the reporting services point by looking at specific status messages and log file entries. Use the following procedure to verify that the reporting services point installation was successful.  

> [!Note]  
> If you see reports in the **Reports** subfolder of the **Reporting** node in the **Monitoring** workspace in the Configuration Manager console, you can skip this procedure.

### Verify installation by status message

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **System Status**, and select the **Component Status** node.  

1. Select the **SMS_SRS_REPORTING_POINT** component.  

1. On the **Home** tab of the ribbon, in the **Component** group, select **Show Messages**, and then choose **All**.  

1. Specify a date and time for a period before you installed the reporting services point, and then select **OK**.  

1. Verify status message ID **1015**. This status message indicates that the reporting services point was successfully installed.

### Verify installation by log file

Open the **Srsrp.log** file, located in the **Logs** directory of the Configuration Manager installation path. Look for the string `Installation was successful`.

Step through this log file starting from the time that the reporting services point was successfully installed. Verify that the report folders were created, the reports were deployed, and the security policy on each folder was confirmed. After the last line of security policy confirmations, look for the string `Successfully checked that the SRS web service is healthy on server`.  

## Configure a certificate to author reports

There are many options for you to author reports in SQL Server Reporting Services. When you create or edit reports in the Configuration Manager console, Configuration Manager opens Report Builder to use as the authoring environment. Regardless of how you author your Configuration Manager reports, you need a self-signed certificate for server authentication to the site database server.

> [!NOTE]  
> For more information about authoring reports with SQL Server Reporting Services, see [Report Builder authoring environment](/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Configuration Manager automatically installs the certificate on the site server and any SMS Provider roles. You can create or edit reports from the Configuration Manager console when you run it from one of these servers.

When you create or modify reports from a Configuration Manager console on a different computer, export the certificate from the site server. The specific certificate's friendly name is the FQDN of the site server in the **Trusted People** certificate store for the local computer. Add this certificate to the **Trusted People** certificate store on the computer that runs the Configuration Manager console.  

## Modify reporting services point settings

After you install this role, you can modify the site database connection and authentication settings in the reporting services point properties.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the **Servers and Site System Roles** node.  

    > [!TIP]  
    > To list only site systems that host the reporting services point, right-click the **Servers and Site System Roles** node, and select **Reporting services point**.  

1. Select the site system that hosts the reporting services point. Then select the **Reporting service point** site system roles in the details pane.

1. On the **Site Role** tab of the ribbon, in the **Properties** group, select **Properties**.  

1. You can modify the following settings in the **Reporting Services Point Properties**:  

    - **Site database server name**

    - **Database name**

    - **User account**

1. Select **OK** to save the changes and close the properties.  

For more information about these settings, see the descriptions in the section to [Install the reporting services point on a site system](#bkmk_install).

## Power BI Report Server

Starting in version 2002, you can integrate reporting with Power BI Report Server. For more information on configuring it, see [Integrate with Power BI Report Server](powerbi-report-server.md).

## Upgrade SQL Server

To upgrade SQL Server and SQL Server Reporting Services, first remove the reporting services point from the site. After you upgrade SQL Server, then reinstall the reporting services point in Configuration Manager.

If you don't follow this process, you'll see errors when you run or edit reports from the Configuration Manager console. You can continue to run and edit reports successfully from a web browser.  

## Configure report options

You can select the default reporting services point that you use to manage reports. The site can have more than one reporting services point, but it only uses the default server to manage reports. Use the following procedure to configure report options for your site.  

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Reporting**, and then select the **Reports** node.  

1. On the **Home** tab of the ribbon, in the **Settings** group, select **Report Options**.  

1. Select the default report server in the list, and then select **OK**.

If it doesn't show any servers, verify that you installed and configured a reporting services point in the site. For more information, see [Verify installation](#bkmk_verify).

Make sure your computer runs a version of SQL Server Report Builder that matches the version of SQL Server that you use for your report server. Otherwise you'll see an error, the default report server won't save, and you can't create or edit reports.<!-- SCCMDocs#791 -->

## Next steps

[Operations and maintenance for reporting](operations-and-maintenance-for-reporting.md)
