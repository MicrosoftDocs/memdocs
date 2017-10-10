---
title: "Configure reporting"
description: "Read about how to set up reporting in your Configuration Manager hierarchy, including information about SQL Server Reporting Services."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: 6
author: Dougebyms.author: dougebymanager: angrobe

---
# Configuring reporting in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Before you can create, modify, and run reports in the System Center Configuration Manager console, you must carry out a number of configuration tasks. Use the following sections in this topic to help you configure reporting in your Configuration Manager hierarchy:  

 Before you proceed with installing and configuring Reporting Services in your hierarchy, review the following Configuration Manager reporting topics:  

-   [Introduction to reporting in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Planning for reporting in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services is a server-based reporting platform that provides comprehensive reporting functionality for a variety of data sources. The reporting services point in Configuration Manager communicates with SQL Server Reporting Services to copy Configuration Manager reports to a specified report folder, to configure Reporting Services settings, and to configure Reporting Services security settings. Reporting Services connects to the Configuration Manager site database to retrieve data that is returned when you run reports.  

 Before you can install the reporting services point in a Configuration Manager site, you must install and configure SQL Server Reporting Services on the site system that hosts the reporting services point site system role. For information about installing Reporting Services, see the [SQL Server TechNet Library](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Use the following procedure to verify that SQL Server Reporting Services is installed and running correctly.  

#### To verify that SQL Server Reporting Services is installed and running  

1.  On the desktop, click **Start**, click **All Programs**, click **Microsoft SQL Server 2008 R2**, click **Configuration Tools**, and then click **Reporting Services Configuration Manager**.  

2.  In the **Reporting Services Configuration Connection** dialog box, specify the name of the server that is hosting SQL Server Reporting Services, on the menu, select the instance of SQL Server on which you installed SQL Reporting Services, and then click **Connect**. The Reporting Services Configuration Manager opens.  

3.  On the **Report Server Status** page, verify that **Report Service Status** is set to **Started**. If it is not, click **Start**.  

4.  On the **Web Service URL** page, click the URL in **Report Service Web Service URLs** to test the connection to the report folder. The **Windows Security** dialog box might open and prompt you for security credentials. By default, your user account is displayed. Enter your password and click **OK**. Verify that the webpage opens successfully. Close the browser window.  

5.  On the **Database** page, verify that the **Report Server Mode** setting is configured by using **Native**.  

6.  On the **Report Manager URL** page, click the URL in **Report Manager Site Identification** to test the connection to the virtual directory for Report Manager. The **Windows Security** dialog box might open and prompt you for security credentials. By default, your user account is displayed. Enter your password and click **OK**. Verify that the webpage opens successfully. Close the browser window.  

    > [!NOTE]  
    >  Reporting Services Report Manager is not required for Reporting in Configuration Manager, but it is required if you want to run reports on an Internet browser or manage reports by using Report Manager.  

7.  Click **Exit** to close Reporting Services Configuration Manager.  

##  <a name="BKMK_ReportBuilder3"></a> Configure reporting to Use Report Builder 3.0  

#### To change the Report Builder manifest name to Report Builder 3.0  

1.  On the computer running the Configuration Manager console, open the Windows Registry Editor.  

2.  Browse to **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Double-click the **ReportBuilderApplicationManifestName** key to edit the value data.  

4.  Change **ReportBuilder_2_0_0_0.application** to **ReportBuilder_3_0_0_0.application**, and then click **OK**.  

5.  Close the Windows Registry Editor.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Install a reporting services point  
 The reporting services point must be installed on a site to manage reports at the site. The reporting services point copies report folders and reports to SQL Server Reporting Services, applies the security policy for the reports and folders, and sets configuration settings in Reporting Services. You must configure a reporting services point before reports are displayed in the Configuration Manager console, and before you can manage the reports in Configuration Manager. The reporting services point is a site system role that must be configured on a server with Microsoft SQL Server Reporting Services installed and running. For more information about prerequisites, see [Prerequisites for reporting](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  When selecting a site to install the reporting services point, keep in mind that users who will access the reports must be in the same security scope as the site where the reporting services point is installed.  

> [!NOTE]  
>  After you install a reporting services point on a site system, do not change the URL for the report server. For example, if you create the reporting services point, and then in Reporting Services Configuration Manager you modify the URL for the report server, the Configuration Manager console will continue to use the old URL and you will be unable to run, edit, or create reports from the console. When you must change the URL report server, remove the reporting services point, change the URL, and then reinstall the reporting services point.  

> [!IMPORTANT]    
> When you install a reporting services point, you must specify a Reporting Services Point Account. Later, when users from a different domain try to run a report, the report will fail to run unless there is a two-way trust established between the domains.

 Use the following procedure to install the reporting services point.  

#### To install the reporting services point on a site system  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.  

    > [!TIP]  
    >  To list only site systems that host the reporting services point site role, right-click **Servers and Site System Roles** to select **Reporting services point**.  

3.  Add the reporting services point site system role to a new or existing site system server by using the associated step:  

    > [!NOTE]  
    >  For more information about configuring site systems, see [Add site system roles for System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **New site system**: On the **Home** tab, in the **Create** group, click **Create Site System Server**. The **Create Site System Server Wizard** opens.  

    -   **Existing site system**: Click the server on which you want to install the reporting services point site system role. When you click a server, a list of the site system roles that are already installed on the server are displayed in the results pane.  

         On the **Home** tab, in the **Server** group, click **Add Site System Role**. The **Add Site System Roles Wizard** opens.  

4.  On the **General** page, specify the general settings for the site system server. When you add the reporting services point to an existing site system server, verify the values that you previously configured.  

5.  On the **System Role Selection** page, select **Reporting services point** in the list of available roles, and then click **Next**.  

6.  On the **Reporting services Point** page, configure the following settings:  

    -   **Site database server name**: Specify the name of the server that hosts the Configuration Manager site database. Typically, the wizard automatically retrieves the fully qualified domain name (FQDN) for the server. To specify a database instance, use the format &lt;*Server Name*>\&lt;*Instance Name*>.  

    -   **Database name**: Specify the Configuration Manager site database name, and then click **Verify** to confirm that the wizard has access to the site database.  

        > [!IMPORTANT]  
        >  The user account that is creating the reporting services point must have **Read** access to the site database. If the connection test fails, a red warning icon appears. Move the cursor over this icon to read details of the failure. Correct the failure, and then click **Test** again.  

    -   **Folder name**: Specify the folder name that is created and used to host the Configuration Manager reports in Reporting Services.  

    -   **Reporting Services server instance**: Select in the list the instance of SQL Server for Reporting Services. When there is only one instance found, by default, it is listed and selected. When no instances are found, verify that SQL Server Reporting Services is installed and configured, and that the SQL Server Reporting Services service is started on the site system.  

        > [!IMPORTANT]  
        >  Configuration Manager makes a connection in the context of the current user to Windows Management Instrumentation (WMI) on the selected site system to retrieve the instance of SQL Server for Reporting Services. The current user must have **Read** access to WMI on the site system, or the Reporting Services instances cannot be retrieved.  

    -   **Reporting Services Point Account**: Click **Set**, and then select an account to use when SQL Server Reporting Services on the reporting services point connects to the Configuration Manager site database to retrieve the data that are displayed in a report. Select **Existing account** to specify a Windows user account that has previously been configured as a Configuration Manager account, or select **New account** to specify a Windows user account that is not currently configured as a Configuration Manager account. Configuration Manager automatically grants the specified user access to the site database. The user is displayed in the **Accounts** subfolder of the **Security** node in the **Administration** workspace with the **ConfigMgr Reporting Services Point** account name.  

         The account that runs Reporting Services must belong to the domain local security group **Windows Authorization Access Group**, and have the **Read tokenGroupsGlobalAndUniversal** permission set to **Allow**. There must be a two-way trust established for users from a different domain than that of the Reporting Servicies Point Account to successfully run reports.

         The specified Windows user account and password are encrypted and stored in the Reporting Services database. Reporting Services retrieves the data for reports from the site database by using this account and password.  

        > [!IMPORTANT]  
        >  The account that you specify must have **Log on Locally** permissions on the computer hosting the Reporting Services database.  

7.  On the **Reporting Services Point** page, click **Next**.  

8.  On the **Summary** page, verify the settings, and then click **Next** to install the reporting services point.  

     After the wizard is completed, report folders are created, and the Configuration Manager reports are copied to the specified report folders.  

    > [!NOTE]  
    >  When report folders are created and reports are copied to the report server, Configuration Manager determines the appropriate language for the objects. If the associated language pack is installed on the site, Configuration Manager creates the objects in the same language as the operating system running on the report server on the site. If the language is not available, the reports are created and displayed in English. When you install a reporting services point on a site without language packs, the reports are installed in English. If you install a language pack after you install the reporting services point, you must uninstall and reinstall the reporting services point for the reports to be available in the appropriate language pack language. For more information about language packs, see [Language Packs in System Center Configuration Manager](../deploy/install/language-packs.md).  

###  <a name="BKMK_FileInstallationAndSecurity"></a> File installation and report folder security rights  
 Configuration Manager performs the following actions to install the reporting services point and to configure Reporting Services:  

> [!IMPORTANT]  
>  The actions in the following list are performed by using the credentials of the account that is configured for the SMS_Executive service, which typically is the site server local system account.  

-   Installs the reporting services point site role.  

-   Creates the data source in Reporting Services with the stored credentials that you specified in the wizard. This is the Windows user account and password that Reporting Services uses to connect to the site database when you run reports.  

-   Creates the Configuration Manager root folder in Reporting Services.  

-   Adds the **ConfigMgr Report Users** and **ConfigMgr Report Administrators** security roles in Reporting Services.  

-   Creates subfolders and deploys Configuration Manager reports from %ProgramFiles%\SMS_SRSRP to Reporting Services.  

-   Adds the **ConfigMgr Report Users** role in Reporting Services to the root folders for all user accounts in Configuration Manager that have **Site Read** rights.  

-   Adds the **ConfigMgr Report Administrators** role in Reporting Services to the root folders for all user accounts in Configuration Manager that have **Site Modify** rights.  

-   Retrieves the mapping between report folders and Configuration Manager secured object types (maintained in the Configuration Manager site database).  

-   Configures the following rights for administrative users in Configuration Manager to specific report folders in Reporting Services:  

    -   Adds users and assigns the **ConfigMgr Report Users** role to the associated report folder for administrative users who have **Run Report** permissions for the Configuration Manager object.  

    -   Adds users and assigns the **ConfigMgr Report Administrators** role to the associated report folder for administrative users who have **Modify Report** permissions for the Configuration Manager object.  

     Configuration Manager connects to Reporting Services and sets the permissions for users on the Configuration Manager and Reporting Services root folders and specific report folders. After the initial installation of the reporting services point, Configuration Manager connects to Reporting Services in a 10-minute interval to verify that the user rights configured on the report folders are the associated rights that are set for Configuration Manager users. When users are added or user rights are modified on the report folder by using Reporting Services Report Manager, Configuration Manager overwrites those changes by using the role-based assignments stored in the site database. Configuration Manager also removes users that do not have Reporting rights in Configuration Manager.  

##  <a name="BKMK_SecurityRoles"></a> Reporting Services security roles for Configuration Manager  
 When Configuration Manager installs the reporting services point, adds the following security roles in Reporting Services:  

-   **ConfigMgr Report Users**: Users assigned with this security role can only run Configuration Manager reports.  

-   **ConfigMgr Report Administrators**: Users assigned with this security role can perform all tasks related to reporting in Configuration Manager.  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a> Verify the Reporting Services Point installation  
 After you add the reporting services point site role, you can verify the installation by looking at specific status messages and log file entries. Use the following procedure to verify that the reporting services point installation was successful.  

> [!WARNING]  
>  You can skip this procedure if reports are displayed in the **Reports** subfolder of the **Reporting** node in the **Monitoring** workspace in the Configuration Manager console.  

#### To verify the reporting services point installation  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **System Status**, and then click **Component Status**.  

3.  Click **SMS_SRS_REPORTING_POINT** in the list of components.  

4.  On the **Home** tab, in the **Component** group, click **Show Messages**, and then click **All**.  

5.  Specify a date and time for a period before you installed the reporting services point, and then click **OK**.  

6.  Verify that status message ID 1015 is listed, which indicates that the reporting services point was successfully installed. Alternatively, you can open the Srsrp.log file, located in &lt;*ConfigMgr Installation Path*>\Logs, and look for **Installation was successful**.  

     In Windows Explorer, navigate to &lt;*ConfigMgr Installation Path*>\Logs.  

7.  Open Srsrp.log and step through the log file starting from the time that the reporting services point was successfully installed. Verify that the report folders were created, the reports were deployed, and the security policy on each folder was confirmed. Look for **Successfully checked that the SRS web service is healthy on server** after the last line of security policy confirmations.  

##  <a name="BKMK_Certificate"></a> Configure a self-signed certificate for Configuration Manager console computers  
 There are many options for you to author SQL Server Reporting Services reports. When you create or edit reports in the Configuration Manager console, Configuration Manager opens Report Builder to use as the authoring environment. Regardless of how you author your Configuration Manager reports, a self-signed certificate is required for server authentication to the site database server. Configuration Manager automatically installs the certificate on the site server and the computers with the SMS Provider installed. Therefore, you can create or edit reports from the Configuration Manager console when it runs from one of these computers. However, when you create or modify reports from a Configuration Manager console that is installed on a different computer, you must export the certificate from the site server and then add it to the **Trusted People** certificate store on the computer that runs the Configuration Manager console.  

> [!NOTE]  
>  For more information about other report authoring environments for SQL Server Reporting Services, see [Comparing Report Authoring Environments](http://go.microsoft.com/fwlink/p/?LinkId=242805) in the SQL Server 2008 Books Online.  

 Use the following procedure as an example of how to transfer a copy of the self-signed certificate from the site server to another computer that runs the Configuration Manager console when both computers run Windows Server 2008 R2. If you cannot follow this procedure because you have a different operating system version, refer to your operating system documentation for the equivalent procedure.  

#### To transfer a copy of self-signed certificate from the site server to another computer  

1.  Perform the following steps on the site server to export the self-signed certificate:  

    1.  Click **Start**, click **Run**, and type **mmc.exe**. In the empty console, click **File**, and then click **Add/Remove Snap-in**.  

    2.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

    3.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

    4.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

    5.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

    6.  In the console, expand **Certificates (Local Computer)**, expand **Trusted People**, and select **Certificates**.  

    7.  Right-click the certificate with the friendly name of &lt;*FQDN of site server*>, click **All Tasks**, and then select **Export**.  

    8.  Complete the **Certificate Export Wizard** by using the default options and save the certificate with the **.cer** file name extension.  

2.  Perform the following steps on the computer that runs the Configuration Manager console to add the self-signed certificate to the Trusted People certificate store:  

    1.  Repeat the preceding steps 1.a through 1.e to configure the **Certificate** snap-in MMC on the management point computer.  

    2.  In the console, expand **Certificates (Local Computer)**, expand **Trusted People**, right-click **Certificates**, select **All Tasks**, and then select **Import** to start the **Certificate Import Wizard**.  

    3.  On the **File to Import** page, select the certificate saved in step 1.h, and then click **Next**.  

    4.  On the **Certificate Store** page, select **Place all certificates in the following store**, with the **Certificate store** set to **Trusted People**, and then click **Next**.  

    5.  Click **Finish** to close the wizard and complete the certificate configuration on the computer.  

##  <a name="BKMK_ModifyReportingServicesPoint"></a> Modify Reporting Services Point settings  
 After the reporting services point is installed, you can modify the site database connection and authentication settings in the reporting services point properties. Use the following procedure to modify the reporting services point settings.  

#### To modify reporting services point settings  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Servers and Site System Roles** to list the site systems.  

    > [!TIP]  
    >  To list only site systems that host the reporting services point site role, right-click **Servers and Site System Roles** to select **Reporting services point**.  

3.  Select the site system that hosts the reporting services point on which you want to modify settings, and then select **Reporting service point** in **Site System Roles**.  

4.  On the **Site Role** tab, in the **Properties** group, click **Properties**.  

5.  On the **Reporting Services Point Properties** dialog box, you can modify the following settings:  

    -   **Site database server name**: Specify the name of the server that hosts the Configuration Manager site database. Typically, the wizard automatically retrieves the fully qualified domain name (FQDN) for the server. To specify a database instance, use the format &lt;*Server Name*>\&lt;*Instance Name*>.  

    -   **Database name**: Specify the System Center 2012 Configuration Manager site database name, and then click **Verify** to confirm that the wizard has access to the site database.  

        > [!IMPORTANT]  
        >  The user account that is creating the reporting services point must have Read access to the site database. If the connection test fails, a red warning icon appears. Move the cursor over this icon to read details of the failure. Correct the failure, and then click **Test** again.  

    -   **User account**: Click **Set**, and then select an account that is used when SQL Server Reporting Services on the reporting services point connects to the Configuration Manager site database to retrieve the data that are displayed in a report. Select **Existing account** to specify a Windows user account that has existing Configuration Manager rights or select **New account** to specify a Windows user account that currently does not have rights in Configuration Manager. Configuration Manager automatically grants the specified user account access to the site database. The account is displayed as the **ConfigMgr SRS reporting point** account in the **Accounts** subfolder of the **Security** node in the **Administration** workspace.  

         The specified Windows user account and password are encrypted and stored in the Reporting Services database. Reporting Services retrieves the data for reports from the site database by using this account and password.  

        > [!IMPORTANT]  
        >  When the site database is on a remote site system, the account that you specify must have the **Log on Locally** permission for the computer.  

6.  Click **OK** to save the changes and exit the dialog box.  

## Upgrading SQL Server  
 After you upgrade SQL Server, and SQL Server Reporting Services that is used as the data source for a reporting services point, you might experience errors when you run or edit reports from the Configuration Manager console. For reporting to work properly from the Configuration Manager console, you must remove the reporting services point site system role for the site and reinstall it. However, after the upgrade you can continue to run and edit reports successfully from an Internet browser.  

##  <a name="BKMK_ConfigureReportOptions"></a> Configure report options  
 Use the report options for a Configuration Manager site to select the default reporting services point that is used to manage your reports. Although you can have more than one reporting services point at a site, only the default report server selected in report options is used to manage reports. Use the following procedure to configure report options for your site.  

#### To configure report options  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Reporting**, and then click **Reports**.  

3.  On the **Home** tab, in the **Settings** group, click **Report Options**.  

4.  Select the default report server in the list, and then click **OK**. If no reporting services points are listed in the list, verify that you have a reporting services point successfully installed and configured in the site.  

## Next steps
[Operations and maintenance for reporting](operations-and-maintenance-for-reporting.md)
