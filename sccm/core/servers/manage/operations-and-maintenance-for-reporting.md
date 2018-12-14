---
title: "Operations and maintenance for reporting "
titleSuffix: "Configuration Manager"
description: "Learn the details of managing reports and report subscriptions in System Center Configuration Manager."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Operations and maintenance for reporting in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
After the infrastructure is in place for reporting in System Center Configuration Manager, there are a number of operations that you typically perform to manage reports and report subscriptions.  

##  <a name="BKMK_ManageReports"></a> Manage Configuration Manager reports  
 Configuration Manager provides over 400 predefined reports that help you gather, organize, and present information about users, hardware and software inventory, software updates, applications, site status, and other Configuration Manager operations in your organization. You can use the predefined reports as they are, or you can modify a report to meet your requirements. You can also create custom model\-based and SQL\-based reports to meet your requirements. Use the following sections to help you manage Configuration Manager reports.  

###  <a name="BKMK_RunReport"></a> Run a Configuration Manager report  
 Reports in Configuration Manager are stored in SQL Server Reporting Services, and the data rendered in the report is retrieved from the Configuration Manager site database. You can access reports in the Configuration Manager console or by using Report Manager, which you access in a web browser. You can open reports on any computer that has access to the computer that is running SQL Server Reporting Services, and you must have sufficient rights to view the reports. When you run a report, the report title, description, and category are displayed in the language of the local operating system.  

> [!NOTE]  
>  In some non\-English languages, characters may not appear correctly in reports.  In this case, reports can be viewed using the web\-based Report Manager or through the Remote Administrator Console.  

> [!WARNING]  
>  To run reports, you must have **Read** rights for the **Site** permission and the **Run Report** permission that is configured for specific objects.  

> [!IMPORTANT]    
> There must be a two-way trust established for users from a different domain than that of the Reporting Servicies Point Account to successfully run reports.

> [!NOTE]  
>  Report Manager is a web\-based report access and management tool that you use to administer a single report server instance on a remote location over an HTTP connection. You can use Report Manager for operational tasks, for example, to view reports, modify report properties, and manage associated report subscriptions. This topic provides the steps to view a report and modify report properties in Report Manager, but for more information about the other options that Report Manager provides, see [Report Manager](http://go.microsoft.com/fwlink/p/?LinkId=224916) in SQL Server 2008 Books Online.  

 Use the following procedures to run a Configuration Manager report.  

##### To run a report in the Configuration Manager console  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Reporting**, and then click **Reports** to list the available reports.  

    > [!IMPORTANT]  
    >  In this version of Configuration Manager, the **All content** reports only display packages, not applications.  

    > [!TIP]  
    >  If no reports are listed, verify that the reporting services point is installed and configured. For more information, see [Configuring reporting](configuring-reporting.md).  

3.  Select the report that you want to run, and then on the **Home** tab, in the **Report Group** section, click **Run** to open the report.  

4.  When there are required parameters, specify the parameters, and then click **View Report**.  

#### To run a report in a web browser  

1.  In your web browser, enter the Report Manager URL, for example, **http:\/\/Server1\/Reports**. You can determine the Report Manager URL on the **Report Manager URL** page in Reporting Services Configuration Manager.  

2.  In Report Manager, click the report folder for Configuration Manager, for example, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  If no reports are listed, verify that the reporting services point is installed and configured. For more information, see [Configuring reporting](configuring-reporting.md).  

3.  Click the report category for the report that you want to run, and then click the link for the report. The report opens in Report Manager.  

4.  When there are required parameters, specify the parameters, and then click **View Report**.  

###  <a name="BKMK_ModifyReportProperties"></a> Modify the properties for a Configuration Manager report  
 In the Configuration Manager console, you can view the properties for a report, such as the report name and description, but to change the properties, use Report Manager. Use the following procedure to modify the properties for a Configuration Manager report.  

#### To modify report properties in Report Manager  

1.  In your web browser, enter the Report Manager URL, for example, **http:\/\/Server1\/Reports**. You can determine the Report Manager URL on the **Report Manager URL** page in Reporting Services Configuration Manager.  

2.  In Report Manager, click the report folder for Configuration Manager, for example, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  If no reports are listed, verify that the Reporting Services point is installed and configured. For more information, see [Configuring reporting](configuring-reporting.md)  

3.  Click the report category for the report for which you want to modify properties, and then click the link for the report. The report opens in Report Manager.  

4.  Click the **Properties** tab. You can modify the report name and description.  

5.  When you are finished, click **Apply**. The report properties are saved on the report server, and the Configuration Manager console retrieves the updated report properties for the report.  

###  <a name="BKMK_EditReport"></a> Edit a Configuration Manager report  
 When an existing Configuration Manager report does not retrieve the information that you have to have or does not provide the layout or design that you want, you can edit the report in Report Builder.  

> [!NOTE]  
>  You can also choose to clone an existing report by opening it for editing, and clicking **Save As** to save it as a new report.  

> [!IMPORTANT]  
>  The user account must have **Site Modify** permission and **Modify Report** permissions on the specific objects associated with the report that you want to modify.  

> [!IMPORTANT]  
>  When Configuration Manager is upgraded to a newer version, new reports overwrite the predefined reports. If you modify a predefined report, you must back up the report before you install the new version, and then restore the report in Reporting Services. If you are making significant changes to a predefined report, consider creating a new report instead. New reports that you create before you upgrade a site are not overwritten.  

 Use the following procedure to edit the properties for a Configuration Manager report.  

#### To edit report properties  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Reporting**, and then click **Reports** to list the available reports.  

3.  Select the report that you want to modify, and then on the **Home** tab, in the **Report Group** section, click **Edit**. Enter your user account and password if you are prompted, and then click **OK**. If Report Builder is not installed on the computer, you are prompted to install it. Click **Run** to install Report Builder, which is required to modify and create reports.  

4.  In Report Builder, modify the appropriate report settings, and then click **Save** to save the report to the report server.  

###  <a name="BKMK_CreateModelBasedReport"></a> Create a model\-based report  
 A model\-based report lets you interactively select the items you want to include in your report. For more information about creating custom report models, see [Creating custom report models for System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  The user account must have **Site Modify** permission to create a new report. The user can only create a report in folders for which the user has **Modify Report** permissions.  

 Use the following procedure to create a model\-based Configuration Manager report.  

#### To create a model\-based report  

1. In the Configuration Manager console, click **Monitoring**.  

2. In the **Monitoring** workspace, expand **Reporting** and click **Reports**.  

3. On the **Home** tab, in the **Create** section, click **Create Report** to open the **Create Report Wizard**.  

4. On the **Information** page, configure the following settings:  

   - **Type**: Select **Model\-based Report** to create a report in Report Builder by using a Reporting Services model.  

   - **Name**: Specify a name for the report.  

   - **Description**: Specify a description for the report.  

   - **Server**: Displays the name of the report server on which you are creating this report.  

   - **Path**: Click **Browse** to specify a folder in which you want to store the report.  

     Click **Next**.  

5. On the **Model Selection** page, select an available model in the list that you use to create this report. When you select the report model, the **Preview** section displays the SQL Server views and entities that are made available by the selected report model.  

6. On the **Summary** page, review the settings. Click **Previous** to change the settings or click **Next** to create the report in Configuration Manager.  

7. On the **Confirmation** page, click **Close** to exit the wizard, and then open Report Builder to configure the report settings. Enter your user account and password if you are prompted, and then click **OK**. If Report Builder is not installed on the computer, you are prompted to install it. Click **Run** to install Report Builder, which is required to modify and create reports.  

8. In Microsoft Report Builder, create the report layout, select data in the available SQL Server views, add parameters to the report, and so on. For more information about using Report Builder to create a new report, see the Report Builder Help.  

9. Click **Run** to run your report. Verify that the report provides the information that you expect. Click **Design** to return to the Design view to modify the report, if needed.  

10. Click **Save** to save the report to the report server. You can run and modify the new report in the **Reports** node in the **Monitoring** workspace.  

###  <a name="BKMK_CreateSQLBasedReport"></a> Create a SQL\-based report  
 A SQL\-based report lets you retrieve data that is based on a report SQL statement.  

> [!IMPORTANT]  
>  When you create an SQL statement for a custom report, do not directly reference SQL Server tables. Instead, reference reporting SQL Server views \(view names that start with v\_\) from the site database. You can also reference public stored procedures \(stored procedure names that start with sp\_\) from the site database.  

> [!IMPORTANT]  
>  The user account must have **Site Modify** permission to create a new report. The user can only create a report in folders for which the user has **Modify Report** permissions.  

 Use the following procedure to create a SQL\-based Configuration Manager report.  

#### To create a SQL\-based report  

1. In the Configuration Manager console, click **Monitoring**.  

2. In the **Monitoring** workspace, expand **Reporting**, and then click **Reports**.  

3. On the **Home** tab, in the **Create** section, click **Create Report** to open the **Create Report Wizard**.  

4. On the **Information** page, configure the following settings:  

   - **Type**: Select **SQL\-based Report** to create a report in Report Builder by using a SQL statement.  

   - **Name**: Specify a name for the report.  

   - **Description**: Specify a description for the report.  

   - **Server**: Displays the name of the report server on which you are creating this report.  

   - **Path**: Click **Browse** to specify a folder in which you want to store the report.  

     Click **Next**.  

5. On the **Summary** page, review the settings. Click **Previous** to change the settings or click **Next** to create the report in Configuration Manager.  

6. On the **Confirmation** page, click **Close** to exit the wizard and open Report Builder to configure the report settings. Enter your user account and password if you are prompted, and then click **OK**. If Report Builder is not installed on the computer, you are prompted to install it. Click **Run** to install Report Builder, which is required to modify and create reports.  

7. In Microsoft Report Builder, provide the SQL statement for the report or build the SQL statement by using columns in available SQL Server views, add parameters to the report, and so on.  

8. Click **Run** to run your report. Verify that the report provides the information that you expect. Click **Design** to return to the Design view to modify the report, if needed.  

9. Click **Save** to save the report to the report server. You can run the new report in the **Reports** node in the **Monitoring** workspace.  

##  <a name="BKMK_ManageReportSubscriptions"></a> Manage report subscriptions  
 Report subscriptions in SQL Server Reporting Services let you configure the automatic delivery of specified reports by email or to a file share at scheduled intervals. Use the **Create Subscription Wizard** in System Center 2012 Configuration Manager to configure report subscriptions.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a> Create a report subscription to deliver a report to a file share  
 When you create a report subscription to deliver a report to a file share, the report is copied in the specified format to the file share that you specify. You can subscribe to and request delivery for only one report at a time.  

 Unlike reports that are hosted and managed by a report server, reports that are delivered to a shared folder are static files. Interactive features that are defined for the report do not work for reports that are stored as files on the file system. Interaction features are represented as static elements. If the report includes charts, the default presentation is used. If the report links through to another report, the link is rendered as static text. If you want to retain interactive features in a delivered report, use email delivery instead. For more information about email delivery, see the [Create a report subscription to deliver a report by email](#BKMK_ReportSubscriptionEmail) section later in this topic.  

 When you create a subscription that uses file share delivery, you must specify an existing folder as the destination folder. The report server does not create folders on the file system. The folder that you specify must be accessible over a network connection. When you specify the destination folder in a subscription, use a UNC path and do not include trailing backslashes in the folder path. For example, a valid UNC path for the destination folder is: \\\\&lt;servername\>\\reportfiles\\operations\\2011.  

 Reports can be rendered in a variety of file formats, such as MHTML or Excel. To save the report in a specific file format, select that rendering format when creating your subscription. For example, choosing Excel saves the report as a Microsoft Excel file. Although you can select any supported rendering format, some formats work better than others when rendering to a file.  

 Use the following procedure to create a report subscription to deliver a report to a file share.  

#### To create a report subscription to deliver a report to a file share  

1. In the Configuration Manager console, click **Monitoring**.  

2. In the **Monitoring** workspace, expand **Reporting** and click **Reports** to list the available reports. You can select a report folder to list only the reports that are associated with the folder.  

3. Select the report that you want to add to the subscription, and then on the **Home** tab, in the **Report Group** section, click **Create Subscription** to open the **Create Subscription Wizard**.  

4. On the **Subscription Delivery** page, configure the following settings:  

   - Report delivered by: Select **Windows File Share** to deliver the report to a file share.  

   - **File Name**: Specify the file name for the report. By default, the report file does not include a file name extension. Select **Add file extension when created** to automatically add a file name extension to this report based on the render format.  

   - **Path**: Specify a UNC path to an existing folder where you want to deliver this report \(for example, \\\\&lt;server name\>\\&lt;server share\>\\&lt;report folder\>\).  

     > [!NOTE]  
     >  The user name specified later on this page must have access to this server share and have Write permissions on the destination folder.  

   - **Render Format**: Select one of the following formats for the report file:  

     -   **XML file with report data**: Saves the report in Extensible Markup Language format.  

     -   **CSV \(comma delimited\)**: Saves the report in comma\-separated\-value format.  

     -   **TIFF file**: Saves the report in Tagged Image File Format.  

     -   **Acrobat \(PDF\) file**: Saves the report in Acrobat Portable Document Format.  

     -   **HTML 4.0**: Saves the report as a webpage viewable only in browsers that support HTML 4.0. Internet Explorer 5 and later versions support HTML 4.0.  

         > [!NOTE]  
         >  If you have images in your report, the HTML 4.0 format does not include them in the file.  

     -   **MHTML \(web archive\)**: Saves the report in MIME HTML format \(mhtml\), which is viewable in many web browsers.  

     -   **RPL Renderer**: Saves the report in Report Page Layout \(RPL\) format.  

     -   **Excel**: Saves the report as a Microsoft Excel spreadsheet.  

     -   **Word**: Saves the report as a Microsoft Word document.  

   - **User Name**: Specify a Windows user account with permissions to access the destination server share and folder. The user account must have access to this server share and have Write permission on the destination folder.  

   - **Password**: Specify the password for the Windows user account. In **Confirm Password**, re\-enter the password.  

   - Select one of the following options to configure the behavior when a file of the same name exists in the destination folder:  

     -   **Overwrite an existing file with a newer version**: Specifies that when the report file already exists, the new version overwrites it.  

     -   **Do not overwrite an existing file**: Specifies that when the report file already exists, there is no action.  

     -   **Increment file names as newer versions are added**: Specifies that when the report file already exists, a number is added to the new report to the file name to distinguish it from other versions.  

   - **Description**: Specifies the description for the report subscription.  

     Click **Next**.  

5. On the **Subscription Schedule** page, select one of the following delivery schedule options for the report subscription:  

   -   **Use shared schedule**: A shared schedule is a previously defined schedule that can be used by other report subscriptions. Select this check box, and then select a shared schedule in the list if any have been specified.  

   -   **Create new schedule**: Configure the schedule on which this report runs, including the interval, start time and date, and the end date for this subscription.  

6. On the **Subscription Parameters** page, specify the parameters for this report that are used when it is run unattended. When there are no parameters for the report, this page is not displayed.  

7. On the **Summary** page, review the report subscription settings. Click **Previous** to change the settings or click **Next** to create the report subscription.  

8. On the **Completion** page, click **Close** to exit the wizard. Verify that the report subscription was created successfully. You can view and modify report subscriptions in the **Subscriptions** node under **Reporting** in the **Monitoring** workspace.  

###  <a name="BKMK_ReportSubscriptionEmail"></a> Create a report subscription to deliver a report by email  
 When you create a report subscription to deliver a report by email, an email is sent to the recipients that you configure, and the report is included as an attachment. The report server does not validate email addresses or obtain email addresses from an email server. You must know in advance which email addresses you want to use. By default, you can email reports to any valid email account within or outside of your organization. You can select one or both of the following email delivery options:  

-   Send a notification and a hyperlink to the generated report.  

-   Send an embedded or attached report. The rendering format and browser determine whether the report is embedded or attached. If your browser supports HTML 4.0 and MHTML, and you select the MHTML \(web archive\) rendering format, the report is embedded as part of the message. All other rendering formats \(CSV, PDF, Word, and so on\) deliver reports as attachments. Reporting Services does not check the size of the attachment or message before sending the report. If the attachment or message exceeds the maximum limit allowed by your mail server, the report is not delivered.  

> [!IMPORTANT]  
>  You must configure the email settings in Reporting Services for the **Email** delivery option to be available. For more information about configuring the email settings in Reporting Services, see [Configuring a Report Server for Email Delivery](http://go.microsoft.com/fwlink/p/?LinkId=226668) in the SQL Server Books Online.  

 Use the following procedure to create a report subscription to deliver a report by using email.  

#### To create a report subscription to deliver a report by email  

-   In the Configuration Manager console, click **Monitoring**.  

-   In the **Monitoring** workspace, expand **Reporting** and click **Reports** to list the available reports. You can select a report folder to list the only the reports that are associated with the folder.  

-   Select the report that you want to add to the subscription, and then on the **Home** tab, in the **Report Group** section, click **Create Subscription** to open the **Create Subscription Wizard**.  

-   On the **Subscription Delivery** page, configure the following settings:  

    -   **Report delivered by**: Select **E\-mail** to deliver the report as an attachment in an email message.  

    -   **To**: Specify a valid email address to send this report to.  

        > [!NOTE]  
        >  You can enter multiple email recipients by separating each email address with a semicolon.  

    -   **Cc**: Optionally, specify an email address to copy this report to.  

    -   **Bcc**: Optionally, specify an email address to send a blind copy of this report to.  

    -   **Reply To**: Specify the reply address to use if the recipient replies to the email message.  

    -   **Subject**: Specify a subject line for the subscription email message.  

    -   **Priority**: Select the priority flag for this email message. Select **Low**, **Normal**, or **High**. The priority setting is used by Microsoft Exchange to set a flag indicating the importance of the email message.  

    -   **Comment**: Specify text to be added to the body of the subscription email message.  

    -   **Description**: Specify the description for this report subscription.  

    -   **Include Link**: Includes a URL to the subscribed report in the body of the email message.  

    -   **Include Report**: Specify that the report is attached to the e\-mail message. The format in which the report will be attached is specified in the **Render Format** list.  

    -   **Render Format**: Select one of the following formats for the attached report:  

        -   **XML file with report data**: Saves the report in Extensible Markup Language format.  

        -   **CSV \(comma delimited\)**: Saves the report in comma\-separated\-value format.  

        -   **TIFF file**: Saves the report in Tagged Image File Format.  

        -   **Acrobat \(PDF\) file**: Saves the report in Acrobat Portable Document Format.  

        -   **MHTML \(web archive\)**: Saves the report in MIME HTML format \(mhtml\), which is viewable in many web browsers.  

        -   **Excel**: Saves the report as a Microsoft Excel spreadsheet.  

        -   **Word**: Saves the report as a Microsoft Word document.  

-   On the **Subscription Schedule** page, select one of the following delivery schedule options for the report subscription:  

    -   **Use shared schedule**: A shared schedule is a previously defined schedule that can be used by other report subscriptions. Select this check box, and then select a shared schedule in the list if any have been specified.  

    -   **Create new schedule**: Configure the schedule on which this report will run, including the interval, start time and date, and the end date for this subscription.  

-   On the **Subscription Parameters** page, specify the parameters for this report that are used when it is run unattended. When there are no parameters for the report, this page is not displayed.  

-   On the **Summary** page, review the report subscription settings. Click **Previous** to change the settings or click **Next** to create the report subscription.  

-   On the **Completion** page, click **Close** to exit the wizard. Verify that the report subscription was created successfully. You can view and modify report subscriptions in the **Subscriptions** node under **Reporting** in the **Monitoring** workspace.  
