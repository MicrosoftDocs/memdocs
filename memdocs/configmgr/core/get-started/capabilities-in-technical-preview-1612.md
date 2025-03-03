---
title: Capabilities in Technical Preview 1612
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview for Configuration Manager, version 1612.
ms.date: 01/23/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1612 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*



This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1612. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## The Data Warehouse Service point
Beginning with the Technical Preview version 1612, the Data Warehouse Service point enables you to store and report on long-term historical data for your Configuration Manager deployment. This is accomplished by automated synchronizations from the Configuration Manager site database to a data warehouse database. This information is then accessible from your Reporting services point.

By default, when you install the new site system role, Configuration Manager creates the data warehouse database for you on a SQL Server instance that you specify. The data warehouse supports up to 2 TB of data, with timestamps for change tracking.  By default, the data that is synchronized from the site database includes the data groups for Global Data, Site Data, Global_Proxy, Cloud Data, and Database Views. You can also modify what is synchronized to include more tables, or exclude specific tables from the default replication sets.
The default data that is synchronized includes information about:
- Infrastructure health
- Security
- Compliance
- Malware   
- Software deployments
- Inventory details (however, inventory history isn't synchronized)

In addition to installing and configuring the data warehouse database, several new reports are installed so you can easily search for and report on this data.

### Data Warehouse Dataflow   
![Datawarehouse_flow](./media/datawarehouse.png)

| Step         | Details  |
|:------:|-----------|  
| **1** | The site server transfers and stores data in the site database.  |  
| **2** | Based on its schedule and configuration, the Data Warehouse Service point gets data from the site database.  |  
| **3** | The Data Warehouse Service point transfers and stores a copy of the synchronized data in the Data Warehouse database. |  
| **A** | Using built-in reports, a request for data is made which is passed to the Reporting Services point using SQL Server Reporting Services. |  
| **B** | Most reports are for current information, and these requests are run against the site database. |  
| **C** | When a report requests historical data, by using one of the reports with a *Category* of **Data Warehouse**, the request is run against the Data Warehouse database.   |  

### Prerequisites for the Data Warehouse Service point and database
- Your hierarchy must have a Reporting services point site system role installed.
- The computer where you install the site system role requires .NET Framework 4.5.2 or later.
- The computer account of the computer where you install the site system role must have local admin permissions to the computer that will host the data warehouse database.
- The administrative account you use to install the site system role must be a DBO on the instance of SQL Server that will host the data warehouse database.  
- The database is supported:
  - With SQL Server 2012 or later, Enterprise or Datacenter edition.
  - On a default or named instance
  - On a *SQL Server Cluster*. Although this configuration should work, it hasn't been tested and support is best effort.
  - When co-located with either the site database or Reporting services point database. However, we recommend it be installed on a separate server.  
- The account that is used as the *Reporting Services Point Account* must have the **db_datareader** permission to the data warehouse database.  
- The database isn't supported on a *SQL Server AlwaysOn availability group*.

### Install the Data Warehouse
You install the Data Warehouse site system role on a central administration site or primary site by using the **Add Site System Roles Wizard** or the **Create Site System Server Wizard**. See [Install site system roles](../servers/deploy/configure/install-site-system-roles.md) for more information. A hierarchy supports multiple instances of this role, but only one instance is supported at each site.  

When you install the role, Configuration Manager creates the data warehouse database for you on the instance of SQL Server that you specify. If you specify the name of an existing database (as you would do if you [move the data warehouse database to a new SQL Server](#move-the-data-warehouse-database)), Configuration Manager doesn't create a new database but instead uses the one you specify.

#### Configurations used during installation
Use the following information to complete installation of the site system role:

**System Role Selection** page:  
Before the Wizard displays an option to select and install the Data Warehouse Service point, you must have installed a Reporting services point.

**General** page: The following general information is required:
- **Configuration Manager database settings:**   
  - **Server Name** - Specify the FQDN of the server that hosts the site database. If you don't use a default instance of SQL Server, you must specify the instance after the FQDN in the following format: ***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Database name** - Specify the name of the site database.
  - **Verify** - Click **Verify** to make sure that the connection to the site database is successful.
</br></br>
- **Data Warehouse database settings:**
  - **Server name** - Specify the FQDN of the server that hosts the Data Warehouse Service point and database. If you don't use a default instance of SQL Server, you must specify the instance after the FQDN in the following format: ***&lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Database name** - Specify the FQDN for the data warehouse database.  Configuration Manager will create the database with this name. If you specify a database name that already exists on the instance of SQL Server, Configuration Manager will use that database.
  - **Verify** - Click **Verify** to make sure that the connection to the site database is successful.

**Synchronization settings** page:   
- **Data settings:**
  - **Replication groups to synchronize** – Select the data groups you want to synchronize. For information about the different types of data groups, see [Database replication](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) and **Distributed views** in [Data transfers between sites](../plan-design/hierarchy/data-transfers-between-sites.md).
  - **Tables included to synchronize** – Specify the name of each extra table you want to synchronize. Separate multiple tables by using a comma. These tables will be synchronized from the site database in addition to the replication groups you select.
  - **Tables excluded to synchronize** - Specify the name of individual tables from replication groups you synchronize. Tables you specify will be excluded from. Separate multiple tables by using a comma.
- **Synchronization settings:**
  - **Synchronization interval (minutes)** - Specify a value in minutes. After the interval is reached, a new synchronization starts. This supports a range from 60 to 1440 minutes (24 hours).
  - **Schedule** - Specify the days that you want synchronization to run.

**Reporting point access**:   
After the data warehouse role is installed, ensure the account that is used as the *Reporting Services Point Account* has the **db_datareader** permission to the data warehouse database.

#### Troubleshoot installation and data synchronization
Use the following logs to investigate problems with the installation of the Data Warehouse Service point, or synchronization of data:
- **DWSSMSI.log** and **DWSSSetup.log**  - Use these logs to investigate errors when installing the Data warehouse service point.
- **Microsoft.ConfigMgrDataWarehouse.log** – Use this log to investigate data synchronization between the site database to the data warehouse database.

### Reporting
After you install a Data Warehouse site system role, the following reports are available on your Reporting services point with a *Category* of **Data Warehouse:**

|Report                   | Details                                  |
|-------------------------|------------------------------------------|
| **Application Deployment Report** | View details for application deployment for a specific application and machine.|
| **Endpoint Protection and Software Update Compliance Report**   | View computers that are missing software updates.|
| **General Hardware Inventory Report**  | View all hardware inventory for a specific machine.|
| **General Software Inventory Report**  | View all software inventory for a specific machine.|
| **Infrastructure Health Overview**  |Displays an overview of the health of your Configuration Manager infrastructure.|
| **List of Malware Detected**  |View malware that has been detected in the organization.|
| **Software Distribution Summary Report** | A summary of software distribution for a specific advertisement and machine.|

### Move the Data Warehouse database
Use the following steps to move the data warehouse database to a new SQL Server:

1. Review the current database configuration and record the configuration details, including:  
   - The data groups you synchronize
   - Tables you include or exclude from synchronization       

   You'll reconfigure these data groups and tables after you restore the database to a new server and reinstall the site system role.  

2. Use SQL Server Management Studio to backup the data warehouse database, and then again to restore that database to a SQL Server on the new computer that will host the data warehouse.

   After you restore the database to the new server, ensure that the database access permissions are the same on the new data warehouse database as they were on the original data warehouse database.

3. Use the Configuration Manager console to remove the Data Warehouse Service point site system role from the current server.

4. Install a new Data Warehouse Service point and specify the name of the new SQL Server and instance that hosts the Data Warehouse database you restored.

5. After the site system role installs, the move is complete.

You can review the following Configuration Manager logs to confirm the site system role has successfully reinstalled:  
- **DWSSMSI.log** and **DWSSSetup.log**  - Use these logs to investigate errors when installing the Data warehouse service point.
- **Microsoft.ConfigMgrDataWarehouse.log** – Use this log to investigate data synchronization between the site database to the data warehouse database.


## Content Library Cleanup Tool
Beginning with Technical Preview version 1612, you can use a new command line tool (**ContentLibraryCleanup.exe**) to remove content that is no-longer associated with any package or application from a distribution point (orphaned content). This tool is called the content library cleanup tool.

This tool only affects the content on the distribution point you specify when you run the tool and can't remove content from the content library on the site server.

After you install Technical Preview 1612, you can find **ContentLibraryCleanup.exe** in the *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* folder on the Technical Preview site server.

The tool released with this Technical Preview is intended to replace older versions of similar tools released for past Configuration Manager products. Although this tool version will cease to function after March 1st, 2017, new versions will release with future Technical Previews until such time as this tool is released as part of the Current Branch, or a production ready out-of-band release.

### Requirements  
- The tool can be run directly on the computer that hosts the distribution point, or remotely from another server. The tool can only be run against a single distribution point at a time.
- The user account that runs the tool must directly have role-based administration permissions that are equal to a Full Administrator on the Configuration Manager hierarchy.  The tool doesn't function when user account is granted permissions as a member of a Windows security group that has the Full Administrator permissions.

### Modes of operation
The tool can be run in two modes:
1. **What-If mode**:   
   When you don't specify the **/delete** switch, the tool runs in What-If mode and identifies the content that would be deleted from the distribution point but doesn't actually delete any data.

   - When the tool runs in this mode, information about the content that would be deleted is automatically written to the tools log file. The user isn't prompted to confirm each potential deletion.
   - By default, the log file is written to the users temp folder on the computer where you run the tool, however you can use the /log switch to redirect the log file to another location.  
   </br>

   We recommend you run the tool in this mode and review the resulting log file before you run the tool with the /delete switch.  

2. **Delete mode**:
   When you run the tool with the **/delete** switch, the tool runs in delete mode.

   - When the tool runs in this mode, orphaned content that is found on the specified distribution point can be deleted from the distribution point's content library.
   -  Before deleting each file, the user is prompted to confirm that the file should be deleted.  You can select, **Y** for yes, **N** for no, or **Yes to all** to skip further prompts and delete all orphaned content.  
   </br>

   We recommend you run the tool in What-If mode and review the resulting log file before you run the tool with the /delete switch.  

When the content library cleanup tool runs in either mode, it automatically creates a log with a name that includes the mode the tool runs in, distribution point name, date, and time of operation. The log file automatically opens when the tool finishes. By default, this log is written to the users **temp** folder on the computer where you run the tool., However, you can use a command line switch to redirect the log file to another location, including a network share.   


### Run the tool
To run the tool:
1. Open an administrative command prompt to a folder that contains **ContentLibraryCleanup.exe**.  
2. Next, enter a command line that includes the required command line switches, and optional switches you want to use.

**Known issue**
When the tool is run, an error like the following might be returned when any package or deployment has failed, or is in progress:
-  *System.InvalidOperationException: This content library can't be cleaned up right now because package \<packageID> isn't fully installed.*

**Workaround:** None. The tool can't reliable identify orphaned files when content is in progress or has failed to deploy. Therefore, the tool won't allow you to clean-up content until that issue is resolved.



### Command line switches  
The following command line switches can be used in any order.   

|Switch|Details|
|---------|-------|
|**/delete**  |**Optional** </br> Use this switch when you want to delete content from the distribution point. You're prompted before content is deleted. </br></br> When this switch isn't used, the tool logs results about what content would be deleted, but doesn't delete any content from the distribution point. </br></br> Example: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Optional** </br> Run the tool in quiet mode that suppresses all prompts (like prompts when you're deleting content), and don't automatically open the log file. </br></br> Example: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;distribution point FQDN>**  | **Required** </br> Specify the fully qualified domain name (FQDN) of the distribution point that you want to clean. </br></br> Example:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;primary site FQDN>**       | **Optional** when cleaning content from a distribution point at a primary site.</br>**Required** when cleaning content from a distribution point at a secondary site. </br></br> Specify the FQDN of the primary site the distribution point belongs to, or of the parent primary parent when the distribution point is at a secondary site. </br></br> Example: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;primary site code>**  | **Optional** when cleaning content from a distribution point at a primary site.</br>**Required** when cleaning content from a distribution point at a secondary site. </br></br> Specify the site code of the primary site that the distribution point belongs to, or of the parent primary site when the distribution point is at a secondary site.</br></br> Example: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log \<log file directory>**       |**Optional** </br> Specify a directory to place log files in. This can be a local drive, or on a network share.</br></br> When this switch isn't used, log files are automatically placed in the users temp folder.</br></br> Example of local drive: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Example of network share: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|


## Improvements for in-console search
Based on your feedback, we have added the following improvements to in-console search:
- **Object Path:**  
  Many objects now support a new column named **Object Path**.  When you search and include this column in your display results, you can view the path to each object. For example, if you run a search for apps in the Applications node and are also searching sub-nodes, the *Object Path* column in the results pane will show you the path to each object returned.   

- **Preservation of search text:**  
  When you enter text in the search text box, and then switch between searching a sub-node and the current node, the text you typed will now persist and remain available for a new search without having to retype it.

- **Preservation of your decision to search sub-nodes:**  
  The option you select for either searching the *current node* or *all sub-nodes* now persists when you change the node you're working in.   This new behavior means you don't need to constantly reset the decision as you move around the console.  By default, when you open the console the option is to only search the current node.

## Prevent installation of an application if a specified program is running.
You can now configure a list of executable files (with the extension .exe) in deployment type properties which, if running, will block installation of an application. After installation is attempted, users will see a dialog box asking them to close the processes that are blocking installation.

### Try it out
To configure a list of executable files
1. On the properties page of any deployment type, choose the **Installer Handling** tab.
2. Click **Add**, to add one of more executable files to the list (for example **Edge.exe**)
3. Click **OK** to close the deployment type properties dialog box.

Now, when you deploy this application to a user or a device, and one of executables you added is running, the end user will see a Software Center dialog box telling them that the installation failed because an application is running.

## New Windows Hello for Business notification for end users

A new Windows 10 notification informs end users that they must take additional actions to complete Windows Hello for Business setup (for example, setting up a PIN).

## Windows Store for Business support in Configuration Manager

You can now deploy online licensed apps with a deployment purpose of **Available** from the Windows Store for Business to PCs running the Configuration Manager client.
For more information, see [Manage apps from the Windows Store for Business with Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

Support for this feature is currently only available to PCs running the Windows 10 RS2 preview build.

## Return to previous page when a task sequence fails
You can now return to a previous page when you run a task sequence and there's a failure. Prior to this release, you had to restart the task sequence when there was a failure. For example, you can use the **Previous** button in the following scenarios:

- When a computer starts in Windows PE, the task sequence bootstrap dialog might display before the task sequence is available. When you click Next in this scenario, the final page of the task sequence displays with a message that there are no task sequences available. Now, you can click **Previous** to search again for available task sequences. You can repeat this process until the task sequence is available.
- When you run a task sequence, but dependent content packages are not yet available on distribution points, the task sequence fails. You can now distribute the missing content (if it wasn't distributed yet) or wait for the content to be available on distribution points, and then click **Previous** to have the task sequence search again for the content.

## Express installation files support for Windows 10 updates
We have added express installation files support in Configuration Manager for Windows 10 updates. When you use a supported version of Windows 10, you can now use Configuration Manager settings to download only the delta between the current month's Windows 10 Cumulative Update and the previous month's update. Currently in Configuration Manager Current Branch, the full Windows 10 Cumulative Update (including all updates from previous months) are downloaded each month. Using express installation files provides for smaller downloads and faster installation times on clients.

> [!IMPORTANT]
> While the settings to support the use of express installation files is available in Configuration Manager, this functionality is only supported in Windows 10 version 1607 with a Windows Update Agent update included with the updates released on January 10, 2017 (Patch Tuesday). For more information about these updates, see [support article 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). You can take advantage of express installation files when the next set of updates are released on February 14, 2017. Windows 10 version 1607 without the update and prior versions do not support express installation files.


### To enable the download of express installation files for Windows 10 updates on the server
To start synchronizing the metadata for Windows 10 express installation files, you must enable it in the Software Update Point Properties.
1. In the Configuration Manager console, navigate to **Administration** > **Site Configuration** > **Sites**.
2. Select the central administration site or the stand-alone primary site.
3. On the **Home** tab, in the **Settings** group, click **Configure Site Components**, and then click **Software Update Point**. On the **Update Files** tab, select **Download full files for all approved updates and express installation files for Windows 10**.

### To enable support for clients to download and install express installation files
To enable express installation files support on clients, you must enable express installation files on clients in the Software Updates section of client settings. This creates a new HTTP listener that listens for requests to download express installation files on the port that you specify. Once you deploy client settings to enable this functionality on the client, it will attempt to download the delta between the current month's Windows 10 Cumulative Update and the previous month's update (clients must run a version of Windows 10 that supports express installation files).
1. Enable support for express installation files in the Software Update Point Component properties (previous procedure).
2. In the Configuration Manager console, navigate to **Administration** > **Client Settings**.
3. Select the appropriate client settings, then on the **Home** tab, click **Properties**.
4. Select the **Software Updates** page, configure **Yes** for the **Enable installation of Express Updates on clients** setting and configure the port used by the HTTP listener on the client for the **Port used to download content for Express Updates** setting.


## OData endpoint data access

 Configuration Manager now provides a RESTful OData endpoint for accessing Configuration Manager data. The endpoint is compatible with Odata version 4, which enables tools such as Excel and Power BI to easily access Configuration Manager data through a single endpoint. Technical Preview 1612 only supports read access to objects in Configuration Manager.  

Data that is currently available in the [Configuration Manager WMI Provider](../../develop/reference/configuration-manager-reference.md) is now also accessible with the new OData RESTful endpoint. The entity sets exposed by the OData endpoint enable you to enumerate over the same data you can query with the WMI provider.

### Try it out

Before you can use the OData endpoint, you must enable it for the site.

1.  Go to **Administration** > **Site Configuration** > **Sites**.
2.  Select the primary site and click **Properties**.
3.  On the General tab of the primary site properties sheet, click **Enable REST endpoint for all providers on this site**, and then click **OK**.

In your favorite OData query viewer, try queries similar to the following examples to return various objects in Configuration Manager:

| Purpose | OData query |
|---|---|
| Get all collections | `http://localhost/CMRestProvider/Collection` |
| Get a collection | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Get the top 100 devices in the collection | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Get a device with a resource ID in the collection | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Get operating system of the device in the collection | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Get users in the collection | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> The example queries shown in the table use *localhost* as the host name in the URL and can be used on the computer running the SMS Provider. If you're running your queries from a different computer, replace localhost with the FQDN of the server with the SMS Provider installed.

<a name='azure-active-directory-onboarding'></a>

## Microsoft Entra onboarding

Microsoft Entra onboarding creates a connection between Configuration Manager and Microsoft Entra ID to be used by other cloud services. This can currently be used for creating the connection needed for the Cloud Management Gateway.

Perform this task with an Azure admin, as you will need Azure admin credentials.

#### To create the connection:

2. In the **Administration** workspace, choose **Cloud Services** > **Microsoft Entra ID** > **Add Microsoft Entra ID**.
2. Choose **Sign In** to create the connection with Microsoft Entra ID.

#### Configuration Manager client requirements

There are several requirements for enabling the creation of user policy in the Cloud Management Gateway.

- The Microsoft Entra onboarding process must be complete, and the client has to be initially connected to the corporate network to get the connection information.
- Clients must be both domain-joined (registered in Active Directory) and cloud-domain-joined (registered in Microsoft Entra ID).
- You must run [Active Directory User Discovery](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- You must modify the Configuration Manager client to allow user policy requests over the Internet, and deploy the change to the client. Because this change to the client takes place *on the client device*, it can be deployed through the Cloud Management Gateway although you haven't completed the configuration changes needed for user policy.
- Your management point must be configured to use HTTPS to secure the token on the network, and must have .Net 4.5 installed.

After you make these configuration changes, you can create a user policy and move clients to the Internet to test the policy. User policy requests through the Cloud Management Gateway will be authenticated with Microsoft Entra token-based authentication.

## Change to configuring multi-factor authentication for device enrollment

Now that you can set up multi-factor authentication (MFA) for device enrollment in the Azure portal, the MFA option has been removed in the Configuration Manager console. You can find more information on setting up MFA for enrollment [in this Microsoft Intune topic](../../../intune/enrollment/multi-factor-authentication.md).
