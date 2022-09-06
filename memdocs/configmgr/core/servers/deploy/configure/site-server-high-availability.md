---
title: Site server high availability
titleSuffix: Configuration Manager
description: How to configure high availability for the Configuration Manager site server by adding a passive mode site server.
ms.date: 04/11/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Site server high availability in Configuration Manager

*Applies to: Configuration Manager (current branch)*

<!--1128774-->

Historically, you could add redundancy to most of the roles in Configuration Manager by having multiple instances of these roles in your environment. Except for the site server itself. High availability for the site server role is a Configuration Manager-based solution to install another site server in *passive* mode. The central administration site (CAS) and child primary sites can have another site server in passive mode. The site server in passive mode can be on-premises or cloud-based in Azure.

This feature brings the following benefits

- Redundancy and high availability to the site server role  
- More easily change the hardware or OS of the site server  
- More easily move your site server to Azure IaaS  

The site server in passive mode is in addition to your existing site server that is in *active* mode. A site server in passive mode is available for immediate use, when needed. Include this other site server as part of your overall design for making the Configuration Manager service [highly available](high-availability-options.md).  

A site server in passive mode:

- Uses the same site database as your site server in active mode.
- Doesn't write data to the site database when it's in passive mode.
- Uses the same content library as your site server in active mode.

To make the site server in passive mode become active, you manually *promote* it. This action switches the site server in active mode to be the site server in passive mode. The site system roles that are available on the original active mode server remain available so long as that computer is accessible. Only the site server role is switched between active and passive modes.

Microsoft Core Services Engineering and Operations used this feature to migrate their CAS to Microsoft Azure. For more information, see the [Microsoft IT Showcase article](https://www.microsoft.com/insidetrack/migrating-system-center-configuration-manager-on-premises-infrastructure-to-microsoft-azure).

## Supported configurations

- Configuration Manager supports site servers in passive mode in a hierarchy. The CAS and child primary sites can have another site server in passive mode.<!-- 3607755 -->  

- The site server in passive mode can be on-premises or cloud-based in Azure.

    > [!NOTE]
    > A cloud-based site server in passive mode uses Azure infrastructure as a service (IaaS). For more information, see the following articles:
    >
    > - [Azure virtual machines (for cloud-based infrastructure)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [FAQ for Configuration Manager on Azure](../../../understand/configuration-manager-on-azure.yml)  

## Prerequisites

### Active Directory

- Both site servers must be joined to the same Active Directory domain.

- If you've [extended the Active Directory schema](../../../plan-design/network/schema-extensions.md) for Configuration Manager, both site servers need **Full Control** permissions to Active Directory's **System - System Management** container and all descendant objects.

### General configurations for both site servers

- Both site servers can run different OS or service pack versions, as long as both are [supported by Configuration Manager](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

- Don't host the service connection point role on either site server configured for high availability. If it's currently on the original site server, remove it, and install it on another site system server. For more information, see [About the service connection point](about-the-service-connection-point.md).

### Configurations for the site server in passive mode

- Must meet the [prerequisites for installing a primary site](../install/prerequisites-for-installing-sites.md#bkmk_PrereqPri).

  - This requirement includes components like .NET Framework, Remote Differential Compression, and the Windows ADK. For the complete list, see [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md).<!-- SCCMDocs issue 765 -->

  > [!NOTE]
  > Make sure to install the SQL Server Native Client. If you don't install it, the prerequisite checker during Configuration Manager setup will report an error about missing SQL Server permissions.<!-- SCCMDocs#2290 -->

- Must have its computer account in the local **Administrators** group on the site server in active mode.<!--516036-->

- Must install using source files that match the version of the site server in active mode.

- Can't have a site system role from any site installed on it before you install the site server in passive mode role.

- Make sure the computer account for the site server in passive mode has the same permissions as the site server in active mode. For example, it may need permission to content source files, such as boot image source directories.<!-- memdocs#1943 -->

### Permissions for the site system installation account

By default, many customers use the site server's computer account to install new site systems. The requirement is then to add the site server's computer account to the local **Administrators** group on the remote site system. If your environment uses this configuration, make sure to add the computer account of the new site server to this local group on all remote site systems. For example, all remote distribution points.

The more secure and recommended configuration is to use a service account for installing the site system. The most secure configuration is to use a local service account. If your environment uses this configuration, no change is needed.

For more information, see [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account) and [Elevated permissions](../../../plan-design/hierarchy/accounts.md#elevated-permissions).

### Content library

The site content library must be on a remote network share. Both site servers need **Full Control** permissions to the share and its contents. For more information, see [Configure a remote content library for the site server](../../../plan-design/hierarchy/remote-content-library.md).<!--1357525-->

- The site server computer account needs **Full control** permissions to the network path to which you're moving the content library. This permission applies to both the share and the file system. No components are installed on the remote system.

- The site server can't have the distribution point role. The distribution point also uses the content library, and this role doesn't support a remote content library. After moving the content library, you can't add the distribution point role to the site server.

### Site database

Both site servers must use the same site database.

- The database can be remote from each site server. The Configuration Manager setup process doesn't block installation of the site server role on a computer with the Windows role for Failover Clustering. SQL Server Always On availability groups require this role, so previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using an availability group and a site server in passive mode. Only an active server can be installed to a node in an Always On availability group. Passive servers must be installed to standalone servers that do not have any existing site roles on them.<!-- SCCMDocs issue 1074 -->

- The SQL Server that hosts the site database can use a default instance, named instance, [failover cluster instance](use-a-sql-server-cluster-for-the-site-database.md), or an [availability group](sql-server-alwayson-for-a-highly-available-site-database.md).

- Both site servers need the **sysadmin** security role on the instance of SQL Server that hosts the site database. The original site server should already have these roles, so add them for the new site server. For example, the following SQL script adds these roles for the new site server **VM2** in the Contoso domain:

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

- Both site servers need access to the site database on the instance of SQL Server. The original site server should already have this access, so add it for the new site server. For example, the following SQL script adds a login to the **CM_ABC** database for the new site server **VM2** in the Contoso domain:  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

- The site server in passive mode is configured to use the same site database as the site server in active mode. The site server in passive mode only reads from the database. It doesn't write to the database until after it's promoted to active mode.

## Limitations

- Only a single site server in passive mode is supported at each site.

- Passive site servers cannot be installed to nodes in the Always On availability group hosting the Configuration Manager database and must be installed on standalone servers. Moving a passive site server into the Always On availability group after installation is not currently supported. 

- A site server in passive mode isn't supported at a secondary site.<!--SCCMDocs issue 680-->

    > [!NOTE]
    > Secondary sites are still supported under a primary site with highly available site servers.

- Promotion of the site server in passive mode to active mode is manual. There's no automatic failover.

- Site system roles can't be installed on the new server before you add the site server in passive mode.

    > [!NOTE]
    > After it installs the site server in passive mode, you can add additional roles as necessary. For example, a management point at a primary site.

- For roles like the reporting point that use a database, host the database on a server that's remote from both site servers.

- The Configuration Manager console doesn't automatically install on the site server in passive mode.

## Add a site server in passive mode

For more information on the general process of adding roles, see [Install site system roles](install-site-system-roles.md).

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, select the **Sites** node, and select **Create Site System Server** in the ribbon.

2. On the **General** page of the Create Site System Server Wizard, specify the server to host the site server in passive mode. The server you specify can't host any site system roles before installing a site server in passive mode.  

3. On the **System Role Selection** page, select only **Site server in passive mode**.  

    > [!NOTE]  
    > The wizard performs the following initial prerequisite checks on this page:
    >
    > - The selected server isn't a secondary site server
    > - The selected server isn't already a site server in passive mode
    > - The site's content library is in a remote location  
    >  
    > If these initial prerequisite checks fails, you can't continue past this page of the wizard.  

4. On the **Site Server In Passive Mode** page, provide the following information that's used to run setup and install the site server role on the specified server:

     - Choose one of the following options:  

         - **Copy installation source files over the network from the site server in active mode**: This option creates a compressed package and sends it to the new site server.  

         - **Use the source files at the following location on the site server in passive mode**: For example, a local path to which you already copied the source files. Make sure this content is the same version as the site server in active mode.  

         - (*Recommended*) **Use the source files at the following network location**: Specify the path directly to the contents of the `CD.Latest` folder from the site server in active mode. For example, `\\Server\SMS_ABC\CD.Latest` where "*Server*" is the name of the site server in active mode, and "*ABC*" is the site code.

     - Specify the local path at which to install Configuration Manager on the new site server. For example: `C:\Program Files\Configuration Manager`  

5. Complete the wizard. Configuration Manager then installs the site server in passive mode on the specified server.

For detailed installation status, in the console go to the **Monitoring** workspace, and select the **Site Server Status** node. The state for the site server in passive mode displays as **Installing**. For more detailed information, select the server and select **Show Status**. This action opens the Site Server Installation Status window. When the process is complete, the state shows **OK** for both servers.

For more information on the setup process, see [Flowchart - Set up a site server in passive mode](passive-site-server-flowchart.md).

After you add a site server in passive mode, see both site servers on the **Nodes** tab in the **Sites** node of the console.

All Configuration Manager site server components are in standby on the site server in passive mode. The Windows services are still running.

## Site server promotion  

Similarly as with backup and recovery, plan and practice your process to change site servers. Consider the following points in your promotion plan:  

- Practice a planned promotion, where both site servers are online. Also practice an unplanned failover, by forcibly disconnecting or shutting down the site server in active mode.  

- Determine your operational processes during failover, and what to communicate with other Configuration Manager administrators.  

- Before a planned promotion:  

  - Check the overall status of the site and site components. Make sure everything is healthy as normal for your environment.  

  - Check content status for any packages actively replicating between sites.  

  - Check secondary site status and site replication.

  - Don't start any new content distribution jobs or maintenance on child or secondary site servers.

    > [!NOTE]
    > If file or database replication between sites is in progress during failover, the new site server may not receive the replicated content. If this happens, redistribute the software content after the new site server is active.<!--515436--> For database replication, you may need to reinitialize a secondary site after failover.<!-- SCCMDocs issue 808 -->

  - Reduce or remove other scheduled activities at the same time. For example, don't plan to promote a site server immediately after updating the site to a new version. Site update includes other tasks that can potentially conflict with the site server promotion.

    > [!TIP]
    > Here's an example of how other activities can conflict with site server promotion:
    >
    > - Monday: Update the site to the latest version. Enable automatic client upgrade with client piloting.
    > - Tuesday: Promote the site server in passive mode to be the active site server.
    >
    > By Wednesday or Thursday, this action may cause *all* clients to upgrade, not just the pilot collection. This behavior can cause significant network usage and unexpected load on the distribution points.<!-- SCCMDocs-pr#4794 -->

  - If you enable the pre-production client, review the known issue with site server high availability. For more information, see [Pre-production client and site server high availability](../../../clients/manage/upgrade/test-client-upgrades.md#pre-production-client-and-site-server-high-availability).<!-- 13846674 -->

### Process to promote the site server in passive mode to active mode

This section describes how to change the site server in passive mode to active mode. To access the site and make this change, you need to be able to access an instance of the SMS Provider. For more information, see [Use multiple SMS Providers](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#use-multiple-sms-providers).

> [!IMPORTANT]  
> If all instances of the SMS Provider are offline, you can't connect to the site as no provider is available. When you add the site server in passive mode, setup installs an instance of the SMS Provider on this server.<!-- SCCMDocs#1613 -->
>
> The Configuration Manager console requests the list of available SMS Providers from WMI on the site server. When you install multiple SMS Providers at a site, the site randomly assigns each new connection request to use an installed SMS Provider. You can't specify the SMS Provider location to use with a specific connection session. If your console is unable to connect to the site because the current site server is offline, specify the other site server in the Site Connection window.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the site, and then switch to the **Nodes** tab. Select the site server in passive mode, and then select **Promote to active** in the ribbon. Select **Yes** to confirm and continue.
  
2. Refresh the console node. The **Status** column for the server you're promoting displays in the **Nodes** tab as **Promoting**.  

3. After the promotion is complete, the **Status** column shows **OK** for both the new site server in active mode, and for the new site server in passive mode. The **Server Name** column for the site now displays the name of the new site server in active mode.

For detailed status, go to the **Monitoring** workspace, and select the **Site Server Status** node. The **Mode** column identifies which server is *Active* or *Passive*. When you promote a server from passive mode to active mode, select the site server that you're promoting to active, and then choose **Show Status** from the ribbon. This action opens the Site Server Promotion Status window that displays more details about the process.

When a site server in active mode switches over to passive mode, only the site system role is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.

For more information on the *planned* promotion process, see [Flowchart - Promote site server (planned)](promote-site-server-flowchart.md).

### Unplanned failover

If the current site server in active mode is offline, the site server for promotion tries to contact the current site server in active mode for 30 minutes. If the offline server comes back before this time, it's successfully notified, and the change proceeds gracefully. Otherwise the site server for promotion forcibly updates the site configuration for it to be active. If the offline server comes back after this time, it first checks the current state in the site database. It then proceeds with demoting itself to the site server in passive mode.

During this 30-minute waiting period, the site has no site server in active mode. Clients still communicate with client-facing roles such as management points, software update points, and distribution points. Users can install software that's already deployed. No site administration is possible in this time period. For more information, see [Site failure impacts](../../manage/site-failure-impacts.md).  

If the offline server is damaged such that it can't return, delete this site server from the console. Then create a new site server in passive mode to restore a highly available service.

For more information on the *unplanned* failover process, see [Flowchart - Promote site server (unplanned)](promote-site-server-unplanned-flowchart.md).

### Other tasks after site server promotion  

After switching site servers, you don't have to do most of the other tasks as are necessary when [recovering a site](../../manage/recover-sites.md#post-recovery-tasks). For example, you don't need to reset passwords or reconnect your Microsoft Intune subscription.

The following steps may be required if necessary in your environment:  

- If you import PKI certificates for distribution points, reimport the certificate for affected servers. For more information, see [Regenerate the certificates for distribution points](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points).  

- If you integrate Configuration Manager with the Microsoft Store for Business, reconfigure that connection. For more information, see [Manage apps from the Microsoft Store for Business](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).  

- Recreate OSD bootable media and prestaged media in non-PKI environments.  

- In non-PKI environments, you may need to update the self-signed certificate on PXE-enabled distribution points. Do this action in the properties of the distribution point on the Communication tab. Make changes to the self-signed certificate date or time.

## Daily monitoring

When you have a site server in passive mode, monitor it daily. Make sure its Status remains OK and is ready for use. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Site Server Status** node. View both site servers and their current status. Also view status in the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node. Select the site, and then switch to the **Nodes** tab.

> [!NOTE]
> When you update the site to a new version of Configuration Manager, it also updates the site server in passive mode. <!-- SCCMDocs-pr#4293 -->

## Remove a site server in passive mode

<!-- 8918311 -->

The process to remove a site server in passive mode is the same as any site system role. Remove the **Site server** role from the server in passive mode. For more information, see [Procedure to remove a site system role](../install/uninstall-sites-and-hierarchies.md#procedure-to-remove-a-site-system-role).

When you remove any other site system role, the site component manager (`sitecomp`) processes the request. When you remove a site server in passive mode, the failover manager processes the request. For status, monitor the **SMS_FAILOVER_MANAGER** component.

## Next steps

[Flowchart - Set up a site server in passive mode](passive-site-server-flowchart.md)
[Flowchart - Promote site server (planned)](promote-site-server-flowchart.md)
[Flowchart - Promote site server (unplanned)](promote-site-server-unplanned-flowchart.md)
