---
title: "Technical Preview 1706 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1706 for System Center Configuration Manager."
ms.custom: na
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1706 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1706. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


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

## Improved boundary groups for software update points
This release includes improvements for how software update points work with boundary groups. The following summarizes the new fallback behavior:
-   Fallback for software update points now uses a configurable time for fallback to neighbor boundary groups, with a minimum time of 120 minutes.

-   Independent of the fallback configuration, a client attempts to reach the last software update point it used for 120 minutes. After failing to reach that server for 120 minutes, the client then checks its pool of available software update points, so it can find a new one.

  -   All software update points in the client's current boundary group are added to the client's pool immediately.

  -   Because a client tries to use its original server for 120 minutes before seeking a new one, no additional servers are contacted until after two hours have elapsed.

  -   If fallback to a neighbor group is configured for the minimum of 120 minutes, software update points from that neighbor boundary group will be part of the client's pool of available servers.

-   After failing to reach its original server for two hours, the client switches to a shorter cycle for contacting a new software update point.

    This means if a client fails to connect with a new server, it quickly selects the next server from its pool of available servers and attempts to contact that one.

  -   This cycle continues until the client connects to a software update point it can use.
  -   Until the client finds a software update point, additional servers are added to pool of available servers when the fallback time for each neighbor boundary group is met.

For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the Boundary Groups topic for the Current Branch.


## Site server role high availability
High availability for the site server role is a Configuration Manager based solution to make a backup of your primary site server that is available for immediate use. This is accomplished by installing an additional site server as a passive replica of the active site server.

The passive replica:
-   Uses the same site database as your active site server.
-   Receives a copy of the sites content library, which is then kept in synch with the content library on the active site server.
-   Does not write data to the site database so long as it is passive.
-   Does not support installation or removal of optional site system roles so long as it is passive.

To make the passive replica your active site server, you manually promote it to be the active site server. This switches the active site server to be the passive site server. The site system roles that were available on the original active site server remain available so long as that computer is accessible. Only the site server role is switched between active and passive.

To install the passive replica site server, you use the **Create Site System Server Wizard** to configure a new site server with a Type of **Primary site server** and a Mode of **Passive**. The wizard then runs Configuration Manager Setup on the specified server to install the passive replica. After installation is complete, the active site server keeps the passive replica site server and its content library in sync with the changes or configurations that you make to the active site server. This ensures that the passive replica is ready for use when needed.

### Prerequisites and limitations
-   The passive replica is supported only for primary site servers.

-   Each site supports only one passive replica.

- 	Both active and passive site servers must be in the same domain.

-   The passive primary site server can be on-premises or cloud-based in Azure.

-   The active site server must use a remote site database. This site database must also be remote from the computer that will host the passive replica.

    -   The SQL Server that hosts the databse can use a default instance, named instance, SQL Server cluster, or an Always On Availability Group.

    -   The passive replica is configured with the same database as the active primary. It does not use that database until after it is promoted to be the active primary site server.

-   The passive replica computer must meet the prerequisites for a primary site server.

    -   It installs using source files that match the active primary site server’s version.

    -   The active and passive site server computers can run different operating systems or service pack versions, so long as they both remain supported by your version of Configuration Manager.

-   Promotion of the passive replica to be the active site server is manual. There is no automatic failover.

-   Site system roles can be installed only on the active site server computer.

    -   The active site server supports all site system roles. You cannot install site system roles on server when it is the passive replica.

    -   Site system roles that use a database (like the reporting point) must have that database on a server that is remote from the active and passive site server computers.

    -   The SMS_Provider does not install on the passive replica. Because you must connect to an SMS_Provider for the site to manually promote the passive replica to be the active site server, we recommend [installing at least one additional instance of the provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) on an additional computer.

### Add a passive replica
1.	In the console go to **Administration** > **Site Configuration** > **Sites** and start the [Add Site System Roles Wizard](/sccm/core/servers/deploy/configure/install-site-system-roles). You can also use the **Create Site System Server Wizard**.

2.	On the **General** page, specify the server that will become the passive replica. The server you specify cannot host any other site system roles when installing the passive replica.

3.	On the **System Role Selection** page, select only **Primary site server in passive mode**.

4.	To complete the wizard, you must provide the following information that is used to run Setup and install the site server role on the specified server:
    -   Choose to copy installation files from the active site server to the new passive replica site server, or specify a path to a location that contains the contents of the active site servers **CD.Latest** folder.

    -   Specify the same site database server and database name as used by the active site server.

5.	Configuration Manager then installs the passive replica of the site server on the specified server.

When an active site server switches over to be the passive site server, only the site system role is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.
For detailed installation status, go to **Administration** > **Site Configuration** > **Sites**.

-   The status for the passive replica site server displays as **Installing**.

-   Select the server and then click **Show Status** to open **Site Server Installation Status** for more detailed information.

### Promote the passive site server to be active
When you want to change the passive replica to be the active site server, you do so from the **Nodes** pane in **Administration** > **Site Configuration** > **Sites**. So long as you can access an instance of the SMS_Provider, you can access the site to make this change.
1.	In the **Nodes** pane of the Configuration Manager console, select the passive site server, and then from the Ribbon, choose **Promote to active**.

2.	The simple **Status** for the server you are promoting displays in the **Nodes** pane as **Promoting**.

3.	After the promotion is complete, the **Status** column shows **OK** for both the new *Active* server, and for the new *Passive* server.

4.	In **Administration** > **Site Configuration** > **Sites**, the name of the primary site server now displays the name of the new *Active* primary site server.
For detailed status, go to **Monitoring** > **Site Server Status**.
    -   The **Mode** column identifies which server is *Active* or *Passive*.

    -   During the act to promote a passive site server to active, select the passive replica site server that you are promoting, and then choose **Show Status** from the ribbon. This opens the **Site Server Promotion Status** window that displays additional details about the process.

### Daily monitoring
When you have a passive replica of your primary site, monitor it daily to ensure it remains in sync with the active site server, and ready to use. To do so, go to **Monitoring** > **Site Server Status**. Here you can view both the active and passive replica site servers.

The **Summary** tab:
-   The **Mode** column identifies which server is Active or Passive.
-   The **Status** column lists **OK** when the passive replica is current.
-   To view additional details about the state of content synchronization, click **Show status** from the Content Sync State. This opens the Content Library tab where you can try to fix content sync issues.

The **Content Library** tab:
-   View the **State** for content that synchronizes from the active site server to the passive replica.
-   You can select content with a State of **Failed**, and then choose **Sync selected items** from the Ribbon. This action tries to resynchronize that content from the content’s source to the passive replica. During recovery, the State displays as **In progress**, and when it is in sync, it displays as **Success**.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
-   I can install a passive replica of my primary site.
-   I can use the console to promote the passive replica to be active, and confirm the change of status for both site servers.
