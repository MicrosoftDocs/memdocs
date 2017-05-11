---
title: "Technical Preview 1705 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1705 for System Center Configuration Manager."
ms.custom: na
ms.date: 05/19/2017
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
You can use the update reset tool, **CMUpdateReset.exe**, to fix issues when in-console updates have problems downloading or replicating. This tool is included with Technical Preview version 1705. You can find it on the site server of your technical preview site after you install the preview in the ***\cd.latest\SMSSETUP\TOOLS*** folder.

This tool is intended for use with Configuration Manager Technical Preview versions 1606 and later.

You can use this tool when an in-console update has not yet installed and is in a failed state. A failed state can mean the update download remains in progress but is stuck and taking an excessively long time, perhaps hours longer than your historical expectations for update packages of similar size. It can also be a failure to replicate the update to child primary sites.  

When you run the tool, it runs against the update that you specify. By default, the tool does not delete successfully installed or downloaded updates.  

### Prerequisites
The account you use to run the tool requires the following permissions:
-   **SysAdmin** server role on the site database of the central administration site and each primary site in your hierarchy. The tool does not interact with secondary sites.
-  **Full Administrator** security role in the Configuration Manager console.
-   **Local Administrator** on the top-level site of your hierarchy.
-   **Local Administrator** on the computer that hosts the service connection point.

You will need the GUID of the update package that you want to reset. To get the GUID:
-   In the console go to **Administration** > **Updates and Servicing** and then in the display pane, right-click the heading of one of the columns (like **State**), then select **Package Guid**. This adds that column to the display, and the column shows the update package GUID.

> [!TIP]  
> To copy the GUID, select the row for the update package you want to reset, and then use CTRL+C to copy that row. If you paste your copied selection into a text editor, you can then copy only the GUID for use as a command line parameter when you run the tool.

### Run the tool    
You can run the tool from any computer, but will need to have access to the computers noted in the Prerequisites section.

When you run the tool, you use command line parameters to specify the SQL Server at the top-tier site of the hierarchy, the site database name, and the GUID of the update package you want to reset. The tool then identifies the additional servers it needs to access, based on the updates status.   

If the update package is in a *download success* state, the tool does not clean up the package. As an option, you can force the removal of a successfully downloaded update by using the force delete parameter (See command line parameters later in this topic).

After the tool runs:
-   If a package was deleted, you must check for updates to download the package again.
-   If a package was not deleted, you do not need to take action as the update will reinitialize and restart replication or installation.

**Command line parameters:**  

| Parameter        |Description                 |  
|------------------|----------------------------|  
|**-S &lt;FQDN of the SQL Server of your top-tier site>** | *Required* <br> You must specify the FQDN of the SQL Server that hosts the site database for the top-tier site of your hierarchy.    |  
| **-D &lt;Database name>**                        | *Required* <br> You must specify the name of the top-tier sites database.  |  
| **-P &lt;Package GUID>**                         | *Required* <br> You must specify the GUID for the update package you want to reset.   |  
| **-I &lt;SQL Server instance name>**             | *Optional* <br> Use this to identify the instance of SQL Server that hosts the site database. |
| **-FDELETE**                              | *Optional* <br> Use this to force deletion of a successfully downloaded update package. |  
 **Example:**
 You want to force deletion of problematic update package. Your SQL Servers FQDN is *server1.fabrikam.com*, the site datbase is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### Test the tool with the Technical Preview  
You can test this tool on an update package for a technical preview prior to the update completing its prerequisite check. A completed prerequisite check state is identified by the one of the following Status for the package in **Administration** > **Updates and Servicing**:  
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

  -   All software update points in the clients current boundary group are added to the clients pool immediately.

  -   Because a client tries to use its original server for 120 minutes before seeking a new one, no additional servers are contacted until after two hours have elapsed.

  -   If fallback to a neighbor group is configured for the minimum of 120 minutes, software update points from that neighbor boundary group will be part of the client's pool of available servers.

-   After failing to reach its original server for two hours, the client switches to a five-minute cycle for contacting a new software update point.

    This means if a client fails to connect with a new server, after five minutes it selects the next server from its pool of available servers and attempts to contact that one.

  -   This cycle continues until the client connects to a software update point it can use.
  -   Until the client finds a software update point, additional servers are added to pool of available servers when the fallback time for each neighbor boundary group is met.

For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the Boundary Groups topic for the Current Branch.

## Site server high availability
High availability for the System Center Configuration Manager site server is a Configuration Manager based solution to keep your mission critical sites, like a stand-alone primary site, fault tolerant.

With this release, site server high availability is accomplished by installing an additional site as a passive replica backup to the active primary site. Then, you manually failover the active site to the passive primary site to make that replica the new active primary site.

<!--Then you can service the original primary site computer without disruption to your Configuration Manager operations.
-->

To install the passive primary site, you use the **Create Site System Server Wizard** to configure a server with the **Primary site server (Passive)** site system role. The wizard then runs Configuration Manager setup on the specified server to install the passive replica.

The resulting passive replica is a copy of your primary site server with the same local site system roles. The replica is also configured to use the same remote system roles and servers. Additionally, the replica receives a copy of the sites content library.

After installation is complete, the active site keeps the passive replica and its content library in sync with the changes or configurations you make. This ensures that the passive replica is ready for use when its needed.

### Prerequisites and limitations
-   The passive replica is supported only for primary sites.

-   Each site supports only one passive replica.

-   The replica computer must meet the prerequisites for a primary site server.
  -   It installs using source files that match the active primary sites version.

  -   The active primary and replica primary computers can run different operating systems or service pack versions, so long as they both remain supported by your version of Configuration Manager.

-   The active primary site must use a remote site database. This server must also be remote from the computer that will host the passive replica.  

	-		The SQL Server that hosts the databse can use a default instance, named instance, SQL Server cluster, or an Always On Availability Group. 	

	-		The passive replica is configured with the same database as the active primary. It does not use that database until after it is promoted to be the active primary site.

-   The passive primary site server can be on-premises or cloud-based in Azure.  	

<!--  TO BE DETERMINED
-   Co-located site system roles are limited (See  ???)
 -->
-   Failover from the active site to the passive replica is manual. There is no automatic failover to the replica.

<!-- TO BE DETERMINED
- The active primary site must have at least one SMS_Provider installed to a remote computer. This provides a connection point to the site database for the Configuration Manager console to use in the event that the active primary site is not accessible.
 -->

### Add a passive replica
1.	**n the console go to **Administration** > **Site Configuration** > **Sites** and start the [Add Site System Roles Wizard](/sccm/core/servers/deploy/configure/install-site-system-roles). You can also use the **Create Site System Server Wizard**.  
2.	On the **General** page, specify the server that will become the passive replica. This server cannot host any other site system roles at this time.
3.	On the **System Role Selection** page, select only **Primary site server (Passive)**.
4.	To complete the wizard, you must provide the following information that is used to run Setup and install the site on the specified passive replica server:
		-		Choose to copy installation files from the active primary to the new replica, or specify a path to a location that contains the contents of the active primary sites **CD.Latest** folder.
		- 	Specify the same site database server and database name as used by the primary site.
5.  Configuration Manager then installs the passive primary site replica on the specified server.  

For detailed installation status, go to **Administration** > **Site Configuration** > **Sites**:
- The status for the replica server displays as **Installing**.

- Select the server and then click **Show Status** to open **Site Server Installation Status** for more detailed information.

### Promote the passive site server to be active
When you want to change the passive server to be active, you can do so from the **Nodes** pane in **Administration** > **Site Configuration** > **Sites**.
<!-- TO BE DETERMINED
When the active primary site server is not accessible, you can connect a Configuration Manager console to the passive site server to complete the process of failover
-->
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

-   I can install a passive replica of my primary site, and then use the console to fail my site over to using that server.
-   I can confirm that content is synchronized between my active server and the passive replica.
