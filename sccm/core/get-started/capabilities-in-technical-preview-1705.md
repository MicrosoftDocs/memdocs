---
title: "Technical Preview 1705 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1705 for System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1705 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1705. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    

**Known Issues in this Technical Preview:**
-   **Operations Manager Suite connector does not upgrade**. When you upgrade from a previous version of the Technical Preview that had the OMS connector configured, that connector is not upgraded and is no longer available in the console. After upgrade, you must [use the Azure Services wizard](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) and reestablish connection to your OMS workspace.
-   **Surface drivers do not synchronize successfully**. Even though support for surface drivers are listed in **What's New** in the Configuration Manager console for the technical preview, this feature does not yet work as expected.
-   **Unable to create Windows Update for Business deferral policies**. Even though the ability to configure Windows Update for Business deferral policies is listed in **What's New** in the Configuration Manager console for the technical preview, the wizard does not open and you are unable to configure any policies.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**The following are new features you can try out with this version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Update reset tool  
You can use the Configuration Manager Update Reset Tool, **CMUpdateReset.exe**, to fix issues when in-console updates have problems downloading or replicating. This tool is included with Technical Preview version 1705. You can find it on the site server of your technical preview site after you install the preview in the ***\cd.latest\SMSSETUP\TOOLS*** folder.

You can use this tool with Technical Preview versions 1606 or later. This backwards support is provided so the tool can be used with a range of  technical preview update scenarios, and without having to wait until the next technical preview becomes available.

You can use this tool when an in-console update has not yet installed and is in a failed state. A failed state can mean the update download remains in progress but is stuck and taking an excessively long time, perhaps hours longer than your historical expectations for update packages of similar size. It can also be a failure to replicate the update to child primary sites.  

When you run the tool, it runs against the update that you specify. By default, the tool does not delete successfully installed or downloaded updates.  

### Prerequisites
The account you use to run the tool requires the following permissions:
-   **Read** and **Write** permissions to the site database of the central administration site and each primary site in your hierarchy. To set these permissions, you can add the user account as a member of the **db_datawriter** and **db_datareader** [fixed database roles](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) on the Configuration Manager database of each site. The tool does not interact with secondary sites.
-   **Local Administrator** on the top-level site of your hierarchy.
-   **Local Administrator** on the computer that hosts the service connection point.

You will need the GUID of the update package that you want to reset. To get the GUID:
-   In the console go to **Administration** > **Updates and Servicing** and then in the display pane, right-click the heading of one of the columns (like **State**), then select **Package Guid**. This adds that column to the display, and the column shows the update package GUID.

> [!TIP]  
> To copy the GUID, select the row for the update package you want to reset, and then use CTRL+C to copy that row. If you paste your copied selection into a text editor, you can then copy only the GUID for use as a command line parameter when you run the tool.

### Run the tool    
The tool must be run on the top-level site of the hierarchy.

When you run the tool, you use command line parameters to specify the SQL Server at the top-tier site of the hierarchy, the site database name, and the GUID of the update package you want to reset. The tool then identifies the additional servers it needs to access, based on the updates status.   

If the update package is in a *post download* state, the tool does not clean up the package. As an option, you can force the removal of a successfully downloaded update by using the force delete parameter (See command line parameters later in this topic).

After the tool runs:
-   If a package was deleted, restart the top-tier sites SMS_Executive service and then check for updates to download the package again.
-   If a package was not deleted, you do not need to take any action as the update will reinitialize and restart replication or installation.

**Command line parameters:**  

| Parameter        |Description                 |  
|------------------|----------------------------|  
|**-S &lt;FQDN of the SQL Server of your top-tier site>** | *Required* <br> You must specify the FQDN of the SQL Server that hosts the site database for the top-tier site of your hierarchy.    |  
| **-D &lt;Database name>**                        | *Required* <br> You must specify the name of the top-tier sites database.  |  
| **-P &lt;Package GUID>**                         | *Required* <br> You must specify the GUID for the update package you want to reset.   |  
| **-I &lt;SQL Server instance name>**             | *Optional* <br> Use this to identify the instance of SQL Server that hosts the site database. |
| **-FDELETE**                              | *Optional* <br> Use this to force deletion of a successfully downloaded update package. |  
 **Examples:**  
 In a typical scenario, you want to reset an update that has download problems. Your SQL Servers FQDN is *server1.fabrikam.com*, the site database is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 In a more extreme scenario, you want to force deletion of problematic update package. Your SQL Servers FQDN is *server1.fabrikam.com*, the site database is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### Test the tool with the Technical Preview  
You can use this tool with Technical Preview versions 1606 or later. This backwards support is provided so that the tool can be used with a larger number of technical preview update scenarios, without having to wait until the next technical preview version is available.

Run the tool on an update package for a technical preview prior to that update completing its prerequisite check. A completed prerequisite check state is identified by the one of the following Status for the package in **Administration** > **Updates and Servicing**:  
-   **Prerequisite check passed**
-   **Prerequisite check passed with warning**
-   **Prerequisite check failed**


## High DPI console support

With this release, issues with how the Configuration Manager console scales and displays different parts of the UI when viewed on high DPI devices (like a Surface book) should be fixed.


## Peer Cache improvements
Beginning with this technical preview, Peer Cache [no longer uses the Network Access Account](/sccm/core/plan-design/hierarchy/client-peer-cache) to authenticate download requests from peers.


## Improvements for SQL Server Always On Availability Groups  
With this release, you can now use asynchronous commit replicas in the SQL Server Always On availability groups you use with Configuration Manager.  This means you can add additional replicas to your availability groups to use as off-site (remote) backups, and then use them in a disaster recovery scenario.  

-   Configuration Manager supports using the asynchronous commit replica to recover your synchronous replica.  See [site database recovery options](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) in the Backup and Recovery topic for information on how to accomplish this.

-   This release does not support failover to use the asynchronous commit replica as your site database.
> [!CAUTION]  
> Because Configuration Manager does not validate the state of the asynchronous commit replica to confirm it is current, and [by design such a replica can be out of sync](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), use of an asynchronous commit replica as the site database can put the integrity of your site and data at risk.  

-   You can use the same number and type of replicas in an availability group as supported by the version of SQL Server that you use.   (Prior support was limited to two synchronous commit replicas.)

### Configure an asynchronous commit replica
To add an asynchronous replica to an [availability group you use with Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database), you do not need to run the configuration scripts required to configure a synchronous replica. (This is because there is no support to use that asynchronous replica as the site database.) See [the SQL Server documentation](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) for information on how to add secondary replicas to availability groups.

### Use the asynchronous replica to recover your site
Before you use an asynchronous replica to recover your site database, you must stop the active primary site to prevent additional writes to the site database. After you stop the site, you can use an asynchronous replica in place of using a [manually recovered database](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

To stop the site, you can use the [hierarchy maintenance tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) to stop key services on the site server. Use the command line: **Preinst.exe /stopsite**   

Stopping the site is equivalent to stopping the Site Component Manager service (sitecomp) followed by the SMS_Executive service, on the site server.

> [!TIP]  
> If you use a primary passive replica (introduced in this Technical Preview as [Site server role high availability](#site-server-role-high-availability)), you do not need to stop the passive replica. Only the active primary site must be stopped.



## Improved user notifications for Office 365 updates
Improvements have been made to leverage the Office Click-to-Run user experience when a client installs an Office 365 update. This includes pop-up and in-app notifications, and a countdown experience. Prior to this release, when an Office 365 update was sent to a client, Office applications that were open were automatically closed without warning. After this update, Office applications will no longer be closed unexpectedly.

### Prerequisites
This update applies to Office 365 ProPlus clients.

### Known issues
When a client evaluates an Office 365 update assignment for the first time and the update has a deadline scheduled in the past, scheduled immediately, or scheduled within 30 minutes, the Office 365 user experience can be inconsistent. For example, the client might receive a 30 minute countdown dialog for the update, but the actual enforcement could start before the end of the countdown. To avoid this behavior, consider the following:
- Deploy the Office 365 update with a deadline that is scheduled for more than 60 minutes ahead of the current time.
- Configure a maintenance window during non-business hours on the collection or configure an enforcement grace period on the deployment.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
- Deploy to a client an Office 365 update with a deadline set to a time at least 60 minutes ahead of the current time. Observe the new behavior on the client.


## Configure and deploy Windows Defender Application Guard policies

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) is a new Windows feature that helps protect your users by opening untrusted web sites in a secure isolated container that is not accessible by other parts of the operating system. In this technical preview, we’ve added support to configure this feature using Configuration Manager compliance settings which you configure, and then deploy to a collection.
This feature will be released in preview for the 64-bit version of the Windows 10 Creator’s Update (codename: RS2). To test this feature now, you must be using a preview version of this update.


### Before you start

To create and deploy Windows Defender Application Guard policies, the Windows 10 devices to which you deploy the policy must be configured with a network isolation policy. For more details, see the blog post referenced later.
This capability works only with current Windows 10 Insider builds. To test it, your clients must be running a recent Windows 10 Insider Build.

### Try it out!

Ensure you have read the blog post to understand the basics about Windows Defender Application Guard.

To create a policy, and to browse the available settings:

1.	In the Configuration Manager console, choose **Assets and Compliance**.
2.	In the **Assets and Compliance** workspace, choose **Overview** > **Endpoint Protection** > **Windows Defender Application Guard**.
3.	In the **Home** tab, in the **Create** group, click **Create Windows Defender Application Guard Policy**.
4.	Using the blog post as a reference, you can browse and configure the available settings to try the feature out.
5.	When you are finished, complete the wizard, and deploy the policy to one or more Windows 10 devices.

### Further reading

To read more about Windows Defender Application Guard, see [this blog post]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Additionally, to learn more about Windows Defender Application Guard Standalone mode, see [this blog post](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## New capabilities for Azure AD and cloud management

In this release, you can configure cloud services to use Azure AD to support the following scenario:

- Manually install the Configuration Manager client from the internet and have it assign to a Configuration Manager site.
- Use Intune to deploy the Configuration Manager client to devices on the internet.

### Advantages

Using cloud services and Azure AD removes the need to use client authentication certificates.

You can discover Azure AD users into your site to use in collections, and other Configuration Manager operations.

### Before you start

- You must have an Azure AD tenant.
- Your devices must run Windows 10 and be Azure AD joined.  Clients can also be domain joined in addition to Azure AD joined).
- In addition to the [existing prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) for the management point site system role, you must additionally ensure that **ASP.NET 4.5** (and any other options that are automatically selected with this) are enabled on the computer that hosts this site system role.
- To use Microsoft Intune to deploy the Configuration Manager client:
	- You must have a working Intune tenant (Configuration Manager and Intune do not need to be connected).
	- In Intune, you have created and deployed an app containing the Configuration Manager client. For details about how to do this, see How to install clients to Intune MDM-managed Windows devices.
- To use Configuration Manager to deploy the client:
	- At least one management point must be configured for HTTPS mode.
	- You must set up a Cloud Management Gateway.


### Set up the Cloud Management Gateway

Set up the Cloud Management Gateway to let clients access your Configuration Manager site from the internet without using certs.

You'll find help about how to do this in the following topics:

- [Plan for cloud management gateway in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Set up cloud management gateway for Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Monitor cloud management gateway in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

### Set up the Azure Services app in Configuration Manager Cloud Services

This connects your Configuration Manager site to Azure AD and is a prerequisite for all other operations in this section. To do this:

1.	In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and then click **Azure Services**.
2.	On the **Home** tab, in the **Azure Services** group, click **Configure Azure Services**.
3.	On the **Azure Services** page of the Azure Services Wizard, select **Cloud Management** to allow clients to authenticate with the hierarchy using Azure AD.
4.	On the **General** page of the wizard, specify a name, and a description for your Azure service.
5.	On the **App** page of the wizard, select your Azure environment from the list, then click **Browse** to select the server and client apps that will be used to configure the Azure service:
	- In the **Server App** window, select the server app you want to use, and then click **OK**. Server apps are the Azure web apps that contain the configurations for your Azure account, including your Tenant ID, Client ID, and a secret key for clients. If you do not have an available server app, use one of the following:
		- **Create**: To create a new server app, click **Create**. Provide a friendly name for the app and the tenant. Then, after you sign-in to Azure, Configuration Manager creates the web app in Azure for you, including the Client ID and secret key for use with the web app. Later, you can view these from the Azure portal.
		- **Import**: To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you Verify the information, click **OK** to continue. This opton is not currently available in this technical preview.
	- Repeat the same process for the client app.

  You need to grant the *Read directory data* application permission when you use Application Import, to set the correct permissions in the portal. If you use Application Creation the permissions are automatically created with the application, but you still need to give consent to the application in the Azure portal.
6.	On the **Discovery** page of the wizard, optionally **Enable Azure Active Directory User Discovery**, and then click **Settings**.
In the **Azure AD User Discovery Settings** dialog box, configure a schedule for when discovery occurs. You can also enable delta discovery which checks for only new, or changed accounts in Azure AD.
7.	Complete the wizard.

At this point, you have connected your Configuration Manager site to Azure AD.


### Install the CM client from the Internet

Before you start, ensure that the client installation source files are stored locally on the device to which you want to install the client.
Then, use the instructions in [How to deploy clients to Windows computers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) using the following installation command line (replace the values in the example with your own values):

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=<GUID> AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**: If your management point or cloud management gateway uses a non-public server certificate, then the client might not be able to reach the CRL location.
- **/Source**: Local folder:   Location of the client installation files.
- **CCMHOSTNAME**: The name of your Internet management point. You can find this by running **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** from a command prompt on a managed client.
- **SMSMP**: The name of your lookup management point – this can be on your intranet.
- **SMSSiteCode**: The site code of your Configuration Manager site.
- **AADTENANTID**, **AADTENANTNAME**: The ID and name of the Azure AD tenant you linked to Configuration Manager. You can find this by running dsregcmd.exe /status from a command prompt on an Azure AD joined device.
- **AADCLIENTAPPID**: The Azure AD client app ID. For help finding this, see [Use portal to create an Azure Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: The identifier URI of the onboarded Azure AD server app.

## Use Azure Services Wizard to configure a connection to OMS
Beginning with the 1705 technical preview release, you use the **Azure Services Wizard** to configure your connection from Configuration Manager to Operations Management Suite (OMS) cloud service. The wizard replaces previous workflows to configure this connection.

- 	The wizard is used to configure cloud services for Configuration Manager, like OMS, Windows Store for Business (WSfB), and Azure Active Directory (Azure AD).  

-   Configuration Manager connects to OMS for features like [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), or [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### Prerequisites for the OMS Connector
Prerequisites to configure a connection to OMS are unchanged from those [documented for the Current Branch version 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). That information is repeated here:  

- 	Providing Configuration Manager permission to OMS.

- 	The OMS connector must be installed on the computer that hosts a [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) that is in [online mode](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

- 	You must install a Microsoft Monitoring Agent for OMS installed on the service connection point along with the OMS connector. The Agent and the OMS connector must be configured to use the same **OMS Workspace**. To install the agent, see [Download and install the agent](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) in the OMS documentation.
- 	After you install the connector and agent, you must configure OMS to use Configuration Manager data. To do so, in the OMS Portal you [Import Configuration Manager collections](/azure/log-analytics/log-analytics-sccm#import-collections).

### Use the Azure Services Wizard to configure the connection to OMS

1.	In the console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**, and then choose **Configure Azure Services** from the **Home** tab of the ribbon, to start the **Azure Services Wizard**.

2.	On the **Azure Services** page, select the Operation Management Suite cloud service. Provide a friendly name for the **Azure service name** and an optional description, and then click **Next**.

3.	On the **App** page, specify your Azure environment (the technical preview supports only the Public Cloud). Then, click **Browse** to open the Server App window.

4.	Select a web app:

    - 	**Import**: To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you **Verify** the information, click **OK** to continue.   

    > [!NOTE] 	
    > When you configure OMS with this preview, OMS only supports the *import* function for a web app. Creating a new web app is not supported. Similarly, you cannot reuse an existing app for OMS.

5.	If you accomplished all the other procedures successfully, then the information on the **OMS Connection Configuration** screen will automatically appear on this page. Information for the connection settings should appear for your **Azure subscription**, **Azure resource group**, and **Operations Management Suite Workspace**.

6.	The wizard connects to the OMS service using the information you've input. Select the device collections that you want to sync with OMS and then click **Add**.

7.	Verify your connection settings on the **Summary** screen, then select **Next**. The **Progress** screen shows the connection status, then should **Complete**.

8.	After the wizard completes, the Configuration Manager console shows that you have configured **Operation Management Suite** as a **Cloud Service Type**.
