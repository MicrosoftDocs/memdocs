---
title: Site server high availability
titleSuffix: Configuration Manager
description: How to configure high availability for the Configuration Manager site server by adding a passive mode site server.
ms.date: 07/30/2018
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

Starting in Configuration Manager version 1806, high availability for the site server role is a Configuration Manager-based solution to install an additional site server in *passive* mode. The site server in passive mode is in addition to your existing site server that is in *active* mode. A site server in passive mode is available for immediate use, when needed. Include this additional site server as part of your overall design for making the Configuration Manager service [highly available](/sccm/core/servers/deploy/configure/high-availability-options).  

A site server in passive mode:
- Uses the same site database as your site server in active mode.
- Doesn't write data to the site database when it's in passive mode.
- Uses the same content library as your site server in active mode.

To make the site server in passive mode become active, you manually *promote* it. This action switches the site server in active mode to be the site server in passive mode. The site system roles that are available on the original active mode server remain available so long as that computer is accessible. Only the site server role is switched between active and passive modes.

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).



## Prerequisites

- The site server in passive mode can be on-premises or cloud-based in Azure.  
    > [!Note]  
    > A cloud-based site server in passive mode uses Azure infrastructure as a service (IaaS). For more information, see the following articles:  
    > - [Azure virtual machines (for cloud-based infrastructure)](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [FAQ for Configuration Manager on Azure](/sccm/core/understand/configuration-manager-on-azure)  

- Both site servers must be joined to the same Active Directory domain.  

- The site is a standalone primary site. 

- Both site servers must use the same site database, which must be remote each site server.  

     - Both site servers need **sysadmin** permissions on the instance of SQL Server that hosts the site database.

     - The SQL Server that hosts the site database can use a default instance, named instance, [SQL Server cluster](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database), or a [SQL Server Always On availability group](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

     - The site server in passive mode is configured to use the same site database as the site server in active mode. The site server in passive mode only reads from the database. It doesn't write to the database until after it's promoted to active mode.  

- The site content library must be on a remote network share. Both site servers need Full Control permissions to the share and its contents. For more information, see [Manage content library](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library).<!--1357525-->  

    - The site server can't have the distribution point role. The distribution point also uses the content library, and this role doesn't support a remote content library. After moving the content library, you can't add the distribution point role to the site server.  

- The site server in passive mode:  

     - Must meet the [prerequisites for installing a primary site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).  

     - Must have its computer account in the local Administrators group on the site server in active mode.<!--516036-->

     - Installs using source files that match the version of the site server in active mode.  

     - Can't have a site system role from any site prior to installing the site server in passive mode role.  

- Both site servers can run different OS or service pack versions, as long as both are [supported by Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  



## Limitations
- A single site server in passive mode is supported at each primary site.  

- A site server in passive mode isn't supported in a hierarchy. A hierarchy includes a central administration site and a child primary site. Only create a site server in passive mode at a standalone primary site.<!--1358224-->

- A site server in passive mode isn't supported at a secondary site.<!--SCCMDocs issue 680-->  

- Promotion of the site server in passive mode to active mode is manual. There's no automatic failover.  

- Site system roles can't be installed on the new server before you add the site server in passive mode.  

    > [!Note]  
    > After it installs the site server in passive mode, you can add additional roles as necessary. For example, the SMS Provider, or a management point at a primary site.  

- For roles like the reporting point that use a database, host the database on a server that's remote from both site servers.  

- The SMS Provider doesn't install on the site server in passive mode. Connect to a provider for the site to manually promote the site server in passive mode to active mode. Install at least one additional instance of the provider on another server. For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- The Configuration Manager console doesn't automatically install on the site server in passive mode.  



## Add a site server in passive mode

For more information on the general process of adding roles, see [Install site system roles](/sccm/core/servers/deploy/configure/install-site-system-roles).

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, select the **Sites** node, and click **Create Site System Server** in the ribbon.   

2. On the **General** page of the Create Site System Server Wizard, specify the server to host the site server in passive mode. The server you specify can't host any site system roles before installing a site server in passive mode.  

3. On the **System Role Selection** page, select only **Site server in passive mode**.  

    > [!Note]  
    > The wizard performs the following initial prerequisite checks on this page:  
    > - The selected server isn't a secondary site server
    > - The selected server isn't already a site server in passive mode
    > - The site's content library is in a remote location  
    >  
    > If these initial prerequisite checks fails, you can't continue past this page of the wizard.  

4. On the **Site Server In Passive Mode** page, provide the following information that's used to run setup and install the site server role on the specified server:

     - Choose one of the following options:  

         - **Copy installation source files over the network from the site server in active mode**: This option creates a compressed package and sends it to the new site server.  

         - **Use the source files at the following location on the site server in passive mode**: For example, a local path to which you already copied the source files. Make sure this content is the same version as the site server in active mode.  

         - (*Recommended*) **Use the source files at the following network location**: Specify the path directly to the contents of the **CD.Latest** folder from the site server in active mode. For example, `\\Server\SMS_ABC\CD.Latest` where "*Server*" is the name of the site server in active mode, and "*ABC*" is the site code.  

     - Specify the local path at which to install Configuration Manager on the new site server. For example: `C:\Program Files\Configuration Manager`  

5. Complete the wizard. Configuration Manager then installs the site server in passive mode on the specified server.

For detailed installation status, in the console go to the **Monitoring** workspace, and select the **Site Server Status** node. The state for the site server in passive mode displays as **Installing**. For more detailed information, select the server and click **Show Status**. This action opens the Site Server Installation Status window. When the process is complete, the state shows **OK** for both servers.   

For more information on the setup process, see [Flowchart - Set up a site server in passive mode](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

After you add a site server in passive mode, see both site servers on the **Nodes** tab in the **Sites** node of the console. 

All Configuration Manager site server components are in standby on the site server in passive mode. The Windows services are still running.



## Site server promotion  

Similarly as with backup and recovery, plan and practice your process to change site servers. Consider the following points in your promotion plan:  

- Practice a planned promotion, where both site servers are online. Also practice an unplanned failover, by forcibly disconnecting or shutting down the site server in active mode.  

- Determine your operational processes during failover, and what to communicate with other Configuration Manager administrators.  

- Before a planned promotion:  

    - Check the overall status of the site and site components. Make sure everything is healthy as normal for your environment.  

    - Check content status for any packages actively replicating between sites.  

    - Don't start any new content distribution jobs. 

        > [!Note]  
        > If file replication between sites is in progress during failover, the new site server may not receive the replicated file. If this happens, redistribute the software content after the new site server is active.<!--515436-->  


### Process to promote the site server in passive mode to active mode

This section describes how to change the site server in passive mode to active mode. To access the site and make this change, you need to be able to access an instance of the SMS Provider. For more information, see [Use multiple SMS Providers](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv).  

> [!Important]  
> By default, only the original site server has the SMS Provider role. If this server is offline, you can't connect to the site as no provider is available. When you add the site server in passive mode, the SMS Provider isn't automatically added. Add at least one additional SMS Provider role to your site for a highly available service.  

> [!Tip]  
> The Configuration Manager console requests the list of available SMS Providers from WMI on the site server. When you install multiple SMS Providers at a site, the site randomly assigns each new connection request to use an installed SMS Provider. You can't specify the SMS Provider location to use with a specific connection session. If your console is unable to connect to the site because the current site server is offline, specify the other site server in the Site Connection window.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the site, and then switch to the **Nodes** tab. Select the site server in passive mode, and then click **Promote to active** in the ribbon. Click **Yes** to confirm and continue.   
  
2. Refresh the console node. The **Status** column for the server you're promoting displays in the **Nodes** tab as **Promoting**.  

3. After the promotion is complete, the **Status** column shows **OK** for both the new site server in active mode, and for the new site server in passive mode. The **Server Name** column for the site now displays the name of the new site server in active mode.

For detailed status, go to the **Monitoring** workspace, and select the **Site Server Status** node. The **Mode** column identifies which server is *Active* or *Passive*. When you promote a server from passive mode to active mode, select the site server that you're promoting to active, and then choose **Show Status** from the ribbon. This action opens the Site Server Promotion Status window that displays additional details about the process.

When a site server in active mode switches over to passive mode, only the site system role is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.

For more information on the *planned* promotion process, see [Flowchart - Promote site server (planned)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).


### Unplanned failover

If the current site server in active mode is offline, the site server for promotion tries to contact the current site server in active mode for 30 minutes. If the offline server comes back before this time, it's successfully notified, and the change proceeds gracefully. Otherwise the site server for promotion forcibly updates the site configuration for it to be active. If the offline server comes back after this time, it first checks the current state in the site database. It then proceeds with demoting itself to the site server in passive mode.

During this 30 minute waiting period, the site has no site server in active mode. Clients still communicate with client-facing roles such as management points, software update points, and distribution points. Users can install software that's already deployed. No site administration is possible in this time period. For more information, see [Site failure impacts](/sccm/core/servers/manage/site-failure-impacts).  

If the offline server is damaged such that it can't return, delete this site server from the console. Then create a new site server in passive mode to restore a highly available service. 

For more information on the *unplanned* failover process, see [Flowchart - Promote site server (unplanned)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart).


### Additional tasks after site server promotion  

After switching site servers, you don't have to perform most of the other tasks as are necessary when [recovering a site](/sccm/core/servers/manage/recover-sites#post-recovery-tasks). For example, you don't need to reset passwords or reconnect your Microsoft Intune subscription.

The following steps may be required if necessary in your environment:  

- If you import PKI certificates for distribution points, reimport the certificate for affected servers. For more information, see [Regenerate the certificates for distribution points](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points).  

- If you integrate Confguration Manager with the Microsoft Store for Business, reconfigure that connection. For more information, see [Manage apps from the Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).  



## Daily monitoring

When you have a site server in passive mode, monitor it daily. Make sure its Status remains OK and is ready for use. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Site Server Status** node. View both site servers and their current status. Also view status in the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node. Select the site, and then switch to the **Nodes** tab. 
