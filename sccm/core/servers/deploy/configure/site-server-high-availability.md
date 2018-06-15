---
title: Site server high availability
titleSuffix: Configuration Manager
description: How to configure high availability for the Configuration Manager site server by adding a passive mode site server.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Site server high availability in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1128774-->

High availability for the site server role is a Configuration Manager-based solution to install an additional site server in *passive* mode. The site server in passive mode is in addition to your existing site server that is in *active* mode. A site server in passive mode is available for immediate use, when needed.

A site server in passive mode:
- Uses the same site database as your site server in active mode.
- Doesn't write data to the site database when it's in passive mode.
- Uses the same content library as your site server in active mode.
- Doesn't support installation or removal of optional site system roles when it's in passive mode.

To make the site server in passive mode become active, you manually *promote* it. This action switches the site server in active mode to be the site server in passive mode. The site system roles that are available on the original active mode server remain available so long as that computer is accessible. Only the site server role is switched between active and passive modes.

To install a site server in passive mode, use the **Create Site System Server Wizard** to configure a new site server with the role **Site server in passive mode**. After checking prerequisites, Configuration Manager runs setup on the specified server to install the new site server in passive mode. When installation is complete, the site server in active mode keeps the site server in passive mode in sync with changes or configurations that you make to the site.



## Prerequisites

- The site server in passive mode can be on-premises or cloud-based in Azure.  

- Both site servers must be joined to the same Active Directory domain.  

- The site can be a standalone primary site, a child primary site, or a central administration site. 

- Both site servers must use the same site database, which must be remote each site server.  

     - Both site servers need **sysadmin** permissions on the instance of SQL Server that hosts the site database.

     - The SQL Server that hosts the site database can use a default instance, named instance, [SQL Server cluster](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database), or a [SQL Server Always On availability group](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

     - The site server in passive mode is configured to use the same site database as the site server in active mode. However, the site server in passive mode doesn't use that database until after it's promoted to active mode.  

- The site content library must be on a remote network share. Both site servers need Full Control permissions to the share and its contents. For more information, see [Manage content library](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library). <!--1357525-->

- The site server in passive mode:  

     - Must meet the [prerequisites for installing a primary site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).  

     - Must have its computer account in the local Administrators group on the site server in active mode.<!--516036-->

     - Installs using source files that match the version of the site server in active mode.  

     - Can't have a site system role from any site prior to installing the site server in passive mode role.  

- Both site servers can run different OS or service pack versions, as long as both are [supported by Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  



## Limitations
- A single site server in passive mode is supported at each primary site.  

- Promotion of the site server in passive mode to active mode is manual. There is no automatic failover.  

- Site system roles can be installed only on the site server that is in active mode.  

     - A site server in active mode supports all site system roles. You can't install site system roles on the server when it's in passive mode.  

     - Site system roles that use a database (like the reporting point) must have that database on a server that's remote from both site servers.  

     - The SMS Provider doesn't install on the site server in passive mode. You must connect to a provider for the site to manually promote the site server in passive mode to active mode. Install at least one additional instance of the provider on another server. For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  



## Add a site server in passive mode

For more information on the general process of adding roles, see [Install site system roles](/sccm/core/servers/deploy/configure/install-site-system-roles).

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, select the **Sites** node, and click **Create Site System Server** in the ribbon.   

2. On the **General** page of the Create Site System Server Wizard, specify the server to host the site server in passive mode. The server you specify can't host any site system roles before installing a site server in passive mode.  

3. On the **System Role Selection** page, select only **Site server in passive mode**.  

4. On the **Site Server In Passive Mode** page, provide the following information that's used to run setup and install the site server role on the specified server:

     - Choose to copy installation files from the site server in active mode to the new site server, or specify a path to a location that contains the contents of the **CD.Latest** folder from the site server in active mode.  

    - Specify the same site database server and database name as used by the site server in active mode.  

5. Complete the wizard. Configuration Manager then installs the site server in passive mode on the specified server.

For detailed installation status, in the console go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. The state for the site server in passive mode displays as **Installing**. For more detailed information, select the server and click **Show Status** in the Summary pane. This action opens the **Site Server Installation Status**.  

For more information on the setup process, see [Flowchart - Set up a site server in passive mode](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

After you add a site server in passive mode, you can see both site servers on the **Nodes** pane in the **Sites** node of the console. 

All Configuration Manager site server components are in standby on the site server in passive mode. The Windows services are still running.



## Promote the site server in passive mode to active mode

This section describes how to change the site server in passive mode to active mode. To access the site and make this change, you need to be able to access an instance of the SMS Provider. For more information, see [Use multiple SMS Providers](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv).  

> [!Tip]  
> When you install multiple SMS Providers at a site, and a connection request is made, the site randomly assigns each new connection request to use an installed SMS Provider. You can't specify the SMS Provider location to use with a specific connection session.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the site, and then switch to the **Nodes** pane. Select the site server in passive mode, and then click **Promote to active** in the ribbon.  

2. The **Status** column for the server you're promoting displays in the **Nodes** pane as **Promoting**.  

3. After the promotion is complete, the **Status** column shows **OK** for both the new site server in active mode, and for the new site server in passive mode.  

4. In the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. The **Server Name** column for the site now displays the name of the new site server in active mode.  

For detailed status, go to the **Monitoring** workspace, and select the **Site Server Status** node. The **Mode** column identifies which server is *Active* or *Passive*. While promoting a server from passive mode to active mode, select the site server that you are promoting to active, and then choose **Show Status** from the ribbon. This action opens the **Site Server Promotion Status** window that displays additional details about the process.

When a site server in active mode switches over to passive mode, only the site system role is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.

After switching site servers, you don't have to perform other tasks as is when recovering a site. For example, you don't need to reset passwords or reconnect your Microsoft Intune subscription. 

For more information on the promotion process, see [Flowchart - Promote site server (planned)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).



## Daily monitoring
When you have a site server in passive mode, monitor it daily. Make sure it remains in sync with the site server in active mode and is ready for use. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Site Server Status** node. View both site servers and their current status.

The **Summary** tab:

- The **Mode** column identifies which server is Active or Passive.  

- The **Status** column shows **OK** when the site server in passive mode is in sync with the site server in active mode.  

- To view additional details about the state of content synchronization, click **Show status** from the Content Sync State. This action opens the Content Library tab where you can try to fix content sync issues.

The **Content Library** tab:  

- View the **State** for content that synchronizes from the site server in active mode to the passive mode site server.
-   You can select content with a State of **Failed**, and then choose **Sync selected items** from the Ribbon. This action tries to resynchronize that content from the content’s source to the passive mode site server. During recovery, the State displays as **In progress**, and when it is in sync, it displays as **Success**.
