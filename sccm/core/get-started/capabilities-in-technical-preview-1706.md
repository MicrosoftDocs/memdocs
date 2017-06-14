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
High availability for the site server role is a Configuration Manager based solution to install an additional primary site server in *Passive* mode. The passive mode site server is in addition to your existing primary site server that is in *Active* mode. A passive mode site server is available for immediate use, when needed.

A primary site server in passive mode:
-   Uses the same site database as your active site server.
-   Receives a copy of the active site servers content library, which is then kept in synch.
-   Does not write data to the site database so long as it is in passive mode.
-   Does not support installation or removal of optional site system roles so long as it is in passive mode.

To make the passive mode site server your active mode site server, you manually promote it. This switches the active site server to be the passive site server. The site system roles that are available on the original active mode server remain available so long as that computer is accessible. Only the site server role is switched between active and passive mode.

To install a passive mode site server, you use the **Create Site System Server Wizard** to configure a new site server with a Type of **Primary site server** and a Mode of **Passive**. The wizard then runs Configuration Manager Setup on the specified server to install the new site server in passive mode. After installation is complete, the active mode site server keeps the passive mode site server and its content library in sync with changes or configurations that you make to the active site server.

### Prerequisites and limitations
-   A single site server in passive mode is supported at each primary site.

-   The site server in passive mode  can be on-premises or cloud-based in Azure.

- 	Both the active mode and passive mode site servers must be in the same domain.

-   Both the active mode and passive mode site servers must use the same site database, which must be remote from the computers of each site server.

    -   The SQL Server that hosts the database can use a default instance, named instance, SQL Server cluster, or an Always On Availability Group.

    -   The site server in passive mode is configured to use the same site database as the active mode site server. However, the passive mode site server does not use that database until after it is promoted to active mode.

-   The computer that will run the passive mode site server must meet the prerequisites for a primary site server.

    -   It installs using source files that match the version of the active mode site server.

    -   The active and passive mode site server computers can run different operating systems or service pack versions, so long as they both remain supported by your version of Configuration Manager.

-   Promotion of the passive mode site server to active mode server is manual. There is no automatic failover.

-   Site system roles can be installed only on the site server that is in active mode.

    -   A site server in active mode supports all site system roles. You cannot install site system roles on server when it is in passive mode.

    -   Site system roles that use a database (like the reporting point) must have that database on a server that is remote from both the active mode and passive mode site servers.

    -   The SMS_Provider does not install on the site server in passive mode. Because you must connect to an SMS_Provider for the site to manually promote the passive mode site server to active mode, we recommend [installing at least one additional instance of the provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) on an additional computer.

### Add a site server in passive mode
1.	In the console go to **Administration** > **Site Configuration** > **Sites** and start the [Add Site System Roles Wizard](/sccm/core/servers/deploy/configure/install-site-system-roles). You can also use the **Create Site System Server Wizard**.

2.	On the **General** page, specify the server that will host the passive mode site server. The server you specify cannot host any site system roles before installing a site server in passive mode.

3.	On the **System Role Selection** page, select only **Primary site server in passive mode**.

4.	To complete the wizard, you must provide the following information that is used to run Setup and install the site server role on the specified server:
    -   Choose to copy installation files from the active site server to the new passive mode site server, or specify a path to a location that contains the contents of the active site servers **CD.Latest** folder.

    -   Specify the same site database server and database name as used by the active mode site server.

5.	Configuration Manager then installs the site server in passive mode on the specified server.

For detailed installation status, go to **Administration** > **Site Configuration** > **Sites**.
-   The status for the site server in passive mode displays as **Installing**.

-   Select the server and then click **Show Status** to open **Site Server Installation Status** for more detailed information.

### Promote the passive mode site server to active mode
When you want to change the passive mode site server to active mode, you do so from the **Nodes** pane in **Administration** > **Site Configuration** > **Sites**. So long as you can access an instance of the SMS_Provider, you can access the site to make this change.
1.	In the **Nodes** pane of the Configuration Manager console, select the site server in passive mode, and then from the Ribbon, choose **Promote to active**.

2.	The simple **Status** for the server you are promoting displays in the **Nodes** pane as **Promoting**.

3.	After the promotion is complete, the **Status** column shows **OK** for both the new *Active* mode site server, and for the new *Passive* mode site server.

4.	In **Administration** > **Site Configuration** > **Sites**, the name of the primary site server now displays the name of the new *Active* mode site server.
For detailed status, go to **Monitoring** > **Site Server Status**.
    -   The **Mode** column identifies which server is *Active* or *Passive*.

    -   While promoting a server from passive mode to active mode, select the site server that you are promoting to active, and then choose **Show Status** from the ribbon. This opens the **Site Server Promotion Status** window that displays additional details about the process.

When an site server in active mode switches over to passive mode, only the site system role is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.



### Daily monitoring
When you have a primary site in passive mode, monitor it daily to ensure it remains in sync with the active mode site server, and ready to use. To do so, go to **Monitoring** > **Site Server Status**. Here you can view both the active mode and passive mode site servers.

The **Summary** tab:
-   The **Mode** column identifies which server is Active or Passive.
-   The **Status** column lists **OK** when the passive mode server is in sync with the active mode server.
-   To view additional details about the state of content synchronization, click **Show status** from the Content Sync State. This opens the Content Library tab where you can try to fix content sync issues.

The **Content Library** tab:
-   View the **State** for content that synchronizes from the active site server to the passive mode site server.
-   You can select content with a State of **Failed**, and then choose **Sync selected items** from the Ribbon. This action tries to resynchronize that content from the content’s source to the passive mode site server. During recovery, the State displays as **In progress**, and when it is in sync, it displays as **Success**.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
-   I can install a primary site in passive mode.
-   I can use the console to promote the passive mode site server to make it the active mode site server, and confirm the change of status for both site servers.


## Include trust for specific files and folders in a Device Guard policy

In this release, we’ve added further capabilities to [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) policy management

You can now optionally add trust for specific files for folders in a Device Guard policy. This lets you:

1.	Overcome issues with managed installer behaviors
2.	Trust line-of-business apps that cannot be deployed with Configuration Manager
3.	Trust apps that are included in an operating system deployment image.

### Try it out!

1.	While you are creating a Device Guard policy, on the Inclusions tab of the Create Device Guard policy wizard, click **Add**.
2.	In the **Add Trusted File or Folder** dialog box, specify information about the file or folder that you want to trust. You can either specify a local file or folder path or connect to a remote device to which you have permission to connect and specify a file or folder path on that device.
3.	Complete the wizard.
