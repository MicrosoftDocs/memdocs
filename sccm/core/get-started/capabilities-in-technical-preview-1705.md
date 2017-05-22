---
title: "Technical Preview 1705 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1705 for System Center Configuration Manager."
ms.custom: na
ms.date: 05/23/2017
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
 In a typical scenario, you want to reset an update that has download problems. Your SQL Servers FQDN is *server1.fabrikam.com*, the site datbase is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 In a more extreme scenario, you want to force deletion of problematic update package. Your SQL Servers FQDN is *server1.fabrikam.com*, the site datbase is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

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


## Improved boundary groups for software update points
This release includes improvements for how software update points work with boundary groups. The following summarizes the new fallback behavior:
-   Fallback for software update points now uses a configurable time for fallback to neighbor boundary groups, with a minimum time of 120 minutes.

-   Independent of the fallback configuration, a client attempts to reach the last software update point it used for 120 minutes. After failing to reach that server for 120 minutes, the client then checks its pool of available software update points, so it can find a new one.

  -   All software update points in the client's current boundary group are added to the clients pool immediately.

  -   Because a client tries to use its original server for 120 minutes before seeking a new one, no additional servers are contacted until after two hours have elapsed.

  -   If fallback to a neighbor group is configured for the minimum of 120 minutes, software update points from that neighbor boundary group will be part of the client's pool of available servers.

-   After failing to reach its original server for two hours, the client switches to a shorter cycle for contacting a new software update point.

    This means if a client fails to connect with a new server, it quickly selects the next server from its pool of available servers and attempts to contact that one.

  -   This cycle continues until the client connects to a software update point it can use.
  -   Until the client finds a software update point, additional servers are added to pool of available servers when the fallback time for each neighbor boundary group is met.

For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the Boundary Groups topic for the Current Branch.

## Site server role high availability
High availability for the site server role is a Configuration Manager based solution to make a backup of your primary site server available for immediate use.

Site server role high availability is accomplished by installing an additional site as a passive replica of the active primary site.

The passive replica installs as a new primary site that uses the same site database as your active site. Because it is passive, it does not actively write data to the site database so long as it is the passive primary site. The passive primary site does not support installation of optional site system roles while it is passive, but does receive a copy of the sites content library.

To make the passive replica your active site, you manually promote the passive site to be the active site. This switches the active site to be the passive primary site. The site system roles that were available on the original active primary site remain available so long as that computer is accessible. Only the site server role is switched.

To install the passive primary site, you use the **Create Site System Server Wizard** to configure a server with the **Primary site server (Passive)** site system role. The wizard then runs Configuration Manager setup on the specified server to install the passive replica.


After installation is complete, the active site keeps the passive replica and its content library in sync with the changes or configurations you make. This ensures that the passive replica is ready for use when its needed.


### Prerequisites and limitations
-   The passive replica is supported only for primary sites.

-   Each site supports only one passive replica, and the both servers must be in the same domain.   

-   The replica computer must meet the prerequisites for a primary site server.
  -   It installs using source files that match the active primary sites version.

  -   The active primary and replica primary computers can run different operating systems or service pack versions, so long as they both remain supported by your version of Configuration Manager.

-   The active primary site must use a remote site database. This server must also be remote from the computer that will host the passive replica.

	-		The SQL Server that hosts the databse can use a default instance, named instance, SQL Server cluster, or an Always On Availability Group. 	

	-		The passive replica is configured with the same database as the active primary. It does not use that database until after it is promoted to be the active primary site.

-   The passive primary site server can be on-premises or cloud-based in Azure.  	

-   Promotion of the passive primary to be the active primary site is manual. There is no automatic failover to the passive replica.

- All site system roles can be installed on the active primary site server computer.

  -   No optional site system roles install on the passive primary. Although the active site supports all site system roles, those that use a database (like the reporting point) must have that database on a server that is remote from the active and passive primary site computers.

  -   The SMS_Provider is not installed on the passive replica. Because you must connect to an SMS_Provider for the site to promote the passive replica to be active, we recommend [installing at least one additional instance of the provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) on an additional computer.

### Add a passive replica
1.	In the console go to **Administration** > **Site Configuration** > **Sites** and start the [Add Site System Roles Wizard](/sccm/core/servers/deploy/configure/install-site-system-roles). You can also use the **Create Site System Server Wizard**.  
2.	On the **General** page, specify the server that will become the passive replica. The server you specify cannot host any other site system roles when installing the passive replica.
3.	On the **System Role Selection** page, select only **Primary site server (Passive)**.
4.	To complete the wizard, you must provide the following information that is used to run Setup and install the site on the specified passive replica server:
		-		Choose to copy installation files from the active primary to the new replica, or specify a path to a location that contains the contents of the active primary sites **CD.Latest** folder.
		- 	Specify the same site database server and database name as used by the primary site.
5.  Configuration Manager then installs the passive primary site replica on the specified server.  

When an active server is switched to be the passive server, only the *site system role* is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.   

For detailed installation status, go to **Administration** > **Site Configuration** > **Sites**:
- The status for the replica server displays as **Installing**.

- Select the server and then click **Show Status** to open **Site Server Installation Status** for more detailed information.

### Promote the passive site server to be active
When you want to change the passive server to be active, you do so from the **Nodes** pane in **Administration** > **Site Configuration** > **Sites**. So long as you can access an instance of the SMS_Provider, you can access the site to make this change.

1.	In the **Nodes** pane of the Configuration Manager console, select the passive site server, and then from the Ribbon, choose **Make active**.
2.	The simple **Status** for the server you are promoting displays in the **Nodes** pane as **Promoting**. After the promotion is complete, the **Status** column shows **OK** for both the new *Active* server, and for the new *Passive* server.
4.	After the promotion is complete, the status for both servers displays as **OK**.
5.	In **Administration** > **Site Configuration** > **Sites**, the name of the primary site server now displays the name of the new *Active* primary site server.  

For detailed status, go to **Monitoring** > **Site Server Status**:
-   The **Mode** column identifies which server is *Active* or *Passive*.

-   During the act to promote a passive server to active, select the primary site server that you are promoting, and then choose **Show Status** from the ribbon. This opens the **Site Server Promotion Status** window that displays additional details about the process.

### Daily monitoring
When you have a passive replica of your primary site, monitor it daily to ensure it remains in sync with the active primary site, and ready to use.  To do so, go to **Monitoring** > **Site Server Status**. Here you can view both the active and replica primary site servers.  

The **Summary** tab:
-   The **Mode** column identifies which server is *Active* or *Passive*.
-   The **Status** column lists **OK** when the server replicas are current.
-   View additional details about the state of content synchronization. Clicking **Show status** from the Content Sync State, opens the Content Library tab where you can try to fix content sync issues.

The **Content Library** tab:
-   View the **State** for content that synchronizes from the active server to the passive replica.  
-   You can select content with a State of **Failed**, and then choose **Recover selected items** from the Ribbon. This action tries to resynchronize that content from the contents source to the passive replica. During recovery, the State displays as **Restoring**, and when it is in sync, it displays as **Success**.


### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:

-   I can install a passive replica of my primary site.
-   I can use the console to promote the passive replica to be active, and confirm the change of status for both site servers.


## Improvements for SQL Server Always On Availability Groups  
With this release, you can now use asynchronous commit replicas in the SQL Server Always On availability groups you use with Configuration Manager.  This means you can add additional replicas to your availability groups to use as off-site (remote) backups, and then use them in a disaster recovery scenario.  

-   Configuration Manager supports using the asynchronous commit replica to recover your synchronous replica.  For steps on how to accomplish this, see the SQL Server documentation.

-   This release does not support failover to use the asynchronous commit replica as your site database.
> [!CAUTION]  
> Because Configuration Manager does not validate the state of the asynchronous commit replica to confirm it is current, and [by design such a replica can be out of sync](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), use of an asynchronous commit replica as the site database can put the integrity of your site and data at risk.  

-   You can use the same number and type of replicas in an availability group as supported by the version of SQL Server that you use.   (Prior support was limited to two synchronous commit replicas.)

### Configure an asynchronous commit replica
To add an asynchronous replica to an availability group you use with Configuration Manager, you do not need to run the configuration scripts required to configure a synchronous replica. (This is because there is no support to use that asynchronous replica as the site database.)

### Use the asynchronous replica to recover your site
Before you use an asynchronous replica to recover your site database, you must stop the active primary site to prevent additional writes to the site database.  

To stop the site, you can use the [hierarchy maintenance tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) to stop key services on the site server. Use the command line: **Preinst.exe /stopsite**   

Stopping the site is equivalent to stopping the Site Component Manager service (sitecomp) followed by the SMS_Executive service, on the site server.

> [!TIP]  
> If you use a primary passive replica (introduced in this Technical Preview as [Site server role high availability](#site-server-role-high-availability)), you do not need to stop the passive replica. Only the active primary site must be stopped.

After you stop the site, you can use an asynchronous replica in place of using a [manually recovered database](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

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


## Manage Microsoft Surface driver updates
You can now use Configuration Manager to manage Microsoft Surface driver updates.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
1. Enable Synchronization for Microsoft Surface drivers
2. Synchronize Microsoft Surface drivers
3. Deploy synchronized Microsoft Surface drivers

#### To manage Microsoft Surface drivers
1. Enable the Microsoft Surface drivers. Using the procedure in [Configure classification and products](/sccm/sum/get-started/configure-classifications-and-products), select the checkbox on the **Classifications** tab to enable Surface drivers.
2. [Synchronize software updates](/sccm/sum/get-started/configure-classifications-and-products).
3. [Deploy the updates](/sccm/sum/deploy-use/deploy-software-updates).

## Configure Windows Update for Business deferral policies
You can now configure deferral policies for Windows 10 Feature Updates or Quality Updates for Windows 10 devices managed directly by Windows Update for Business. You can manage the deferral policies in the new **Windows Update for Business Policies** node under **Software Library** > **Windows 10 Servicing**.

### Prerequisites
Windows 10 devices managed by Windows Update for Business must have Internet connectivity.

#### To create a Windows Update for Business deferral policy
1. In **Software Library** > **Windows 10 Servicing** > **Windows Update for Business Policies**
2. On the **Home** tab, in the **Create** group, select **Create Windows Update for Business Policy** to open the Create Windows Update for Business Policy Wizard.
3. On the **General** page, provide a name and description for the policy.
4. On the **Deferral Policies** page, configure whether to defer or pause Feature Updates.    
    Feature Updates are generally new features for Windows. After you configure the **Branch readiness level** setting, you can then define if, and for how long, you would like to defer receiving Feature Updates following their availability from Microsoft.
    - **Branch readiness level**: Set the branch for which the device will receive Windows updates (Current Branch or Current Branch for Business).
    - **Deferral period (days)**:  Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for a period of 180 days from their release.
    - **Pause Features Updates starting:**: Select whether to pause devices from receiving Feature Updates for a period of up to 60 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You an unpause Feature Updates by clearing the checkbox.   
5. Choose whether to defer or pause Quality Updates.     
    Quality Updates are generally fixes and improvements to existing Windows functionality and are typically published the first Tuesday of every month, though can be released at any time by Microsoft. You can define if, and for how long, you would like to defer receiving Quality Updates following their availability.
    - **Deferral period (days)**: Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for a period of 180 days from their release.
    - **Pause Quality Updates starting:**: Select whether to pause devices from receiving Quality Updates for a period of up to 35 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You an unpause Quality Updates by clearing the checkbox.
6. Choose whether to exclude Windows Update drivers during updates.
7. Complete the wizard to create the new deferral policy.

#### To deploy a Windows Update for Business deferral policy
1. In **Software Library** > **Windows 10 Servicing** > **Windows Update for Business Policies**
2. On the **Home** tab, in the **Deployment** group, select **Deploy Windows Update for Business Policy**.
3. Configure the following settings:
    - **Configuration policy to deploy**: Select the Windows Update for Business policy that you would like to deploy.
    - **Collection**: Click **Browse** to select the collection where you want to deploy the configuration baseline.
    - **Remediate noncompliant rules when supported**: Select to automatically remediate any rules that are noncompliant for Windows Management Instrumentation (WMI), the registry, scripts, and all settings for mobile devices that are enrolled by Configuration Manager.
    - **Allow remediation outside the maintenance window**: If a maintenance window has been configured for the collection to which you are deploying the policy, enable this option to let compliance settings remediate the value outside of the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Generate an alert**: Configures an alert that is generated if the configuration baseline compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.
    - **Random delay (hours)**: Specifies a delay window to avoid excessive processing on the Network Device Enrollment Service. The default value is 64 hours.
    - **Schedule**: Specify the compliance evaluation schedule by which the deployed profile is evaluated on client computers. The schedule can be either a simple or a custom schedule. The profile is evaluated by client computers when the user logs on.
4.  Complete the wizard to deploy the profile.
